**<h3 class="text-center ">Flexible inputs and outputs</h3>**
<br>
Evalutils currently supports the creation of only three types of algorithms out of the box: classification, segmentation, and detection.  However, it is very much possible to use the automatically generated repository for a classification algorithm and adapt it for a registration algorithm. 

It is also possible to customize the repository to support flexible inputs and outputs. For example, you may want to register a moving image to a fixed image, in which case you will need two inputs. Or you may want to write a binary mask and another image file containing the predicted probabilities. This is possible by inheriting and overriding the [`process`](https://github.com/comic/evalutils/blob/master/evalutils/evalutils.py#L180-L184) function of evalutils. 

The general principle here is that your Algorithm container will process only one job at a time, and each job will process only one set of inputs. You will have to write your scripts to read that one set of inputs from `/input` and write your algorithm's outputs to `/output`. For the default algorithms, evalutils automatically does this in the background. But for algorithms that require flexibility, you will have to write your own `load_inputs` and `write_outputs` functions. Please look at our [Interfaces](https://grand-challenge.org/algorithms/interfaces/) to understand what to read from `/input` and what to write to `/output` depending on the needs of your algorithm. In case the required interfaces are not available, then please reach out to us. Check the snippets below for an example. The automatically generated code for a `CustomAlgorithm` would look like the following:

```python
import SimpleITK
import numpy as np

from evalutils import SegmentationAlgorithm
from evalutils.validators import (
    UniquePathIndicesValidator,
    UniqueImagesValidator,
)

class Customalgorithm(SegmentationAlgorithm):
    def __init__(self):
        super().__init__(
            validators=dict(
                input_image=(
                    UniqueImagesValidator(),
                    UniquePathIndicesValidator(),
                )
            ),
        )

    def predict(self, *, input_image: SimpleITK.Image) -&gt; SimpleITK.Image:
        # Segment all values greater than 2 in the input image
        return SimpleITK.BinaryThreshold(
            image1=input_image, lowerThreshold=2, insideValue=1, outsideValue=0
        )

if __name__ == "__main__":
    Customalgorithm().process()
```
<br>
This can be modified to support flexible inputs and outputs with the following example:

```python
import SimpleITK
import numpy as np

class Customalgorithm():  # SegmentationAlgorithm is not inherited in this class anymore
    def __init__(self):
        """
        Write your own input validators here
        Initialize your model etc.
        """
        pass

    def load_inputs(self):
        """
        Read from /input/
        Check https://grand-challenge.org/algorithms/interfaces/
        """
        return inputs

    def write_outputs(self, outputs):
        """
        Write to /output/
        Check https://grand-challenge.org/algorithms/interfaces/
        """
        pass
    
    def predict(self, inputs):
        """
        Your algorithm goes here
        """        
        return outputs

    def process(self):
        """
        Read inputs from /input, process with your algorithm and write to /output
        """
        inputs = self.load_inputs()
        outputs = self.predict(inputs)
        self.write_outputs(outputs)

if __name__ == "__main__":
    Customalgorithm().process()
```
<br>