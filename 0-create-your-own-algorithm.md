**<h3 class="text-center">Create your own algorithm</h3>**

![](https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/03/22/faffee96-08e2-4447-a759-813e5996489b.PNG) 

This tutorial takes you through the steps to serve your algorithm in a [Docker container](https://www.docker.com/resources/what-container) compatible with the requirements of [grand-challenge.org](https://grand-challenge.org). Wrapping your algorithm in a container ensures that the environments necessary for reproducing your algorithm are packaged along with the algorithm. We focus on creating a Docker container to perform _inference_ with your algorithm on test data, but most instructions apply to any algorithm.  

If you want to share an Algorithm on Grand Challenge, you will likely recognize yourself in one of the following roles:

1. A *researcher* who intends to share their algorithm on the Algorithms page of Grand-Challenge.org.
2. A Type 2 Challenge *organizer* who is looking to create a baseline algorithm, to help participants with submitting their algorithms.
3. A Type 2 Challenge *participant* who wants to submit their algorithm.

 <!-- 1. Test and build locally, which requires a local installation of Docker Engine and python with evalutils installed, in a (virtual) Linux environment.
 2. Link a Github repository to Grand Challenge, and let us build the container for you. This is the easiest way if you are participating in a Type II challenge, and doesn't require a local development environment as in option 1. -->
Depending on your role, the development process may be slightly different, but in general, we provide two options for developing algorithm containers:

1. Develop locally, build locally, and upload the resulting container to Grand Challenge.
1. Develop locally, push code to a (private) GitHub repo, and build in the cloud on Grand Challenge. (Recommended)

Within this context, 'building' an algorithm means that Docker Engine converts your code to a container that runs your algorithm. Through the feedback that the GC support team received, we found out that many users got stuck installing Docker. Therefore, we generally recommend the second option: to develop locally, and let us build the Algorithm from a GitHub repo. This does not require a Docker installation. An additional benefit of this, is that any algorithm update will be tracked by Github's version control system. This makes it easy to revert a faulty update, and it keeps your code maintainable long after you've moved on in your career.

##### **Testing and debugging locally vs on the Cloud**

A major advantage of having Docker installed locally, is that you can debug and develop a test suite. It's faster than testing by letting Grand Challenge build your Algorithm in the cloud. Therefore, we do not want to discourage a user from installing Docker locally, we simply indicate that failing to install Docker, does not mean end of story. Algorithms on Grand Challenge can be developed without it.

For example, if you are participating in a Type II challenge, the challenge organizer may have published a baseline algorithm repository. It may need only minor adjustment for you to bring your own algorithm into this. 

Therefore, it is recommended to simply clone that repository; adjust the code; and link your repository, as is explained in the next subtabs. Hopefully, it will be as easy as swapping out a few lines of code, without the need to test and debug.

##### **Setting up local environment**

If you do choose to install Docker locally, you will need to do so on a Linux environment, or set up [Windows subsystem for Linux (WSL) 2](https://docs.microsoft.com/en-us/windows/wsl/install) to work with Docker on a Linux environment within Windows. In the video tutorial below, we have used WSL 2 with Ubuntu 18.04 LTS. Currently, the latest version of WSL2 on Windows 11 comes with GPU support. If you are using Windows 11, make sure to follow [our guide](https://grand-challenge.org/documentation/setting-up-wsl-with-gpu-support-for-windows-11/)  for setting up WSL with GPU support. 

Whether you want to install Docker is up to you, but we recommend you install the following software packages to develop an Algorithm:

- [evalutils](https://comic.github.io/evalutils/installation.html) 
- [git-bash](https://git-scm.com/downloads)
- [git-lfs](https://github.com/git-lfs/git-lfs/wiki/Installation) (for pulling the model weights in the walkthrough) 


#####  **Video tutorial** 

Apart from reading through the tutorial in the sub-tabs of this section, you can also watch the corresponding video tutorial. It provides a walkthrough of the entire process for creating an algorithm container for the DRIVE Challenge using evalutils. __NOTE:__ This video is slightly outdated, and was made with `evalutils v0.2.4`. The rest of the written documentation here is based on `evalutils v0.3`.

This video also requires a local installation of [Docker Engine](https://docs.docker.com/engine/), which is not required in general.

Clone the repository containing the U-Net that segments retinal blood vessels from the DRIVE Challenge and then watch the video. 
``` 
$ git clone https://github.com/DIAGNijmegen/drive-vessels-unet.git 
``` 
<br>
<video class="w-100" controls src="https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/03/25/evalutils-algo-container-drive.mp4#t=118"></video>
<br>

##### **Contact**

For contact and support, please email [**kiranvaidhya.venkadesh@radboudumc.nl**](mailto:kiranvaidhya.venkadesh@radboudumc.nl) and cc [**support@grand-challenge.org**](mailto:support@grand-challenge.org). <br>

##### **Disclaimer**
<div>Icons made by <a href="https://www.freepik.com" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a></div><br>
