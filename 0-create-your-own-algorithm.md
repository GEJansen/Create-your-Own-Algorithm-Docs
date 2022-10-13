**<h3 class="text-center">Create your own algorithm</h3>**

![](https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/03/22/faffee96-08e2-4447-a759-813e5996489b.PNG) 

This tutorial takes you through the steps to serve your algorithm in a [Docker container](https://www.docker.com/resources/what-container) compatible with the requirements of [grand-challenge.org](https://grand-challenge.org). We focus on creating a Docker container to perform _inference_ with your algorithm on test data, but most instructions apply to any algorithm.  

Wrapping your algorithm in a container ensures that the environments necessary for reproducing your algorithm are packaged along with the algorithm. This is the fastest and the most reliable way to reproduce algorithms.  We chose Docker as this is the most popular and widely used technology for creating containers. 

#####  **Before you start ** 

To follow the video tutorial, make sure you have the following software packages installed on your computer: 

- [Docker](https://www.docker.com/get-started) 
- [evalutils](https://comic.github.io/evalutils/installation.html) 
- [git-lfs](https://github.com/git-lfs/git-lfs/wiki/Installation) (for pulling the model weights in this walkthrough) 

##### **Environment**

It is highly recommended to install [Windows subsystem for Linux (WSL)](https://docs.microsoft.com/en-us/windows/wsl/install) to work with Docker on a Linux environment within Windows. In the video tutorial below, we have used WSL 2 with Ubuntu 18.04 LTS. Currently, the latest version of WSL2 on Windows 11 comes with GPU support. If you are using Windows 11, make sure to follow [our guide](https://grand-challenge.org/documentation/setting-up-wsl-with-gpu-support-for-windows-11/)  for setting up WSL with GPU support. 

#####  **Video tutorial** 

Apart from reading through the tutorial in the sub-tabs of this section, you can also watch the corresponding video tutorial. It provides a walkthrough of the entire process for creating an algorithm container for the DRIVE Challenge using evalutils.  However, note that this video tutorial was made with `evalutils v0.2.4`. The rest of the written documentation here is based on `evalutils v0.3`, including updated documentation for testing your containers locally!

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