**<h3 class="text-center ">🔨Building and 🧪testing the container</h3>**
<br>
#### **Building**
Once your scripts are ready, you can build the container by calling `./build.sh`. The recommendation is for your containers to be tested locally before they are uploaded to grand-challenge.org. Uploading a container always takes time and it's best to keep grand-challenge.org out of your development loop.

#### **Testing**

The templated repository made by evalutils provides a testing script (`test.sh`). You can extend this template to build your own test suite. 

In our example, we restructured the `test` folder by placing the first retinal fundus image from the test set of the DRIVE challenge. The `./test/input/` folder contains the raw image and the `./test/expected_output/` folder contains the outputs our algorithm would have to write for the test to pass.

```
test
├── expected_output
│   ├── images
│   │   └── 01_test.tif
│   └── results.json
└── input
    └── 01_test.tif
``` 
<br>
We further modified the automatically created test script `test.sh` to customize it for our use case. The customized snippet now has two major steps:

1. Mount a temporary Docker volume to `/output/` and write the algorithm's outputs there
2. Mount the temporary Docker volume and check if the outputs there match the outputs in `./test/expected_output/`. Here, we have used `biocontainers/simpleitk:v1.0.1-3-deb-py3_cv1` to access SimpleITK within a Docker.

```bash
#!/usr/bin/env bash

SCRIPTPATH="$( cd "$(dirname "$0")" ; pwd -P )"

./build.sh

VOLUME_SUFFIX=$(cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 8 | head -n 1)

docker volume create vesselsegmentation-output-$VOLUME_SUFFIX

# run the forward pass and store the outputs in a temporary Docker volume
docker run --rm \
        --gpus=all \
        -v $SCRIPTPATH/test/input/:/input/ \
        -v vesselsegmentation-output-$VOLUME_SUFFIX:/output/ \
        vesselsegmentation

# compare the outputs in the Docker volume with the outputs in ./test/expected_output/
docker run --rm \
        -v vesselsegmentation-output-$VOLUME_SUFFIX:/output/ \
        -v $SCRIPTPATH/test/expected_output/:/expected_output/ \
        biocontainers/simpleitk:v1.0.1-3-deb-py3_cv1 python3 -c """
import SimpleITK as sitk

output = sitk.ReadImage('/output/images/01_test.tif')
expected_output = sitk.ReadImage('/expected_output/images/01_test.tif')

label_filter = sitk.LabelOverlapMeasuresImageFilter()
label_filter.Execute(output, expected_output)
dice_score = label_filter.GetDiceCoefficient()

if dice_score == 1.0:
    print('Test passed!')
else:
    print('Test failed!')
"""

docker volume rm vesselsegmentation-output-$VOLUME_SUFFIX

```
<br>
You can invoke the testing script by calling `./test.sh` 

💡 If you already have exported containers in your working directory, you can add `*.tar.gz` files into a `.dockerignore` file to make your builds much faster. This speeds up your development and testing processes.

⚠️Docker Desktop for Windows 10 does not have GPU support. You would need Windows 11 and WSL2 with Ubuntu 18.04 for GPU support with Docker. Note that this does not compromise your building and exporting processes. It only hampers your testing process. You can avoid this by testing with CPU-only mode if possible. Make sure to remove the `--gpus=all` flag. Otherwise, you will have to test your container by running it on an Ubuntu environment if you need GPU access.

💡 Our modifications from the templated repository generated by evalutils can be found here: [https://github.com/DIAGNijmegen/drive-vessels-unet/tree/master/VesselSegmentation](https://github.com/DIAGNijmegen/drive-vessels-unet/tree/master/VesselSegmentation)