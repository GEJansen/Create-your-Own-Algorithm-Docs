**<h3 class="text-center text-bold">Setting up WSL with GPU support for Windows</h3>**
<br>
In this tutorial we will show you how to  set up WSL with GPU support. This tutorial assumes that you do not yet have WSL or Docker desktop installed. 

1. Install the Nvidia driver. The required driver depends on your GPU. You can install the driver for your specific GPU [here](https://www.nvidia.com/Download/index.aspx?lang=en-us). 

2. Install WSL. Open the command window and execute the lines below, this will install WSL with Ubuntu. Although we are using Ubuntu in this tutorial, any flavor of Linux can be installed in this step. 

	``` 
	wsl.exe –-install -d Ubuntu 
	``` 

	``` 
	wsl.exe –-update
	``` 				

	After installation, make sure to run the commands from the following steps through the Ubuntu terminal. 

3. Install Docker. If you have previously installed Docker, make sure to first remove your current version before installing the new version. If this is the first time that you're installing Docker, you can skip this first line.

	```
	$ sudo apt-get remove docker docker-engine docker.io containerd runc
	```		

	We will install Docker by setting up the repository. This is the recommended way of installing Docker on Linux according to the [Docker docs](https://docs.docker.com/engine/install/ubuntu/).

	```
	$  sudo apt-get update
	```

	```
	$ sudo apt-get install ca-certificates curl gnupg lsb-release
	```

	Now we have to add Docker's official GPG key and set up the stable repository.

	```
	$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
	```

	```
	$ echo \
	  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
	  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list &gt; /dev/null
	```
	
	We can now perform the actual install of Docker with the following lines. 
	
	```
	$  sudo apt-get update
	```
	
	```
	$ sudo apt-get install docker-ce docker-ce-cli containerd.io
	```

	After installation we should verify that Docker has been installed correctly. Let's start Docker and run an example hello world container. 
	
	```
	$ sudo service docker start
	```

	```
	$ sudo docker run hello-world
	```

4. Post-installation steps. By default we can now only run Docker commands as root user. In order to run Docker without the sudo prefix we need to perform the following steps. Note that although these steps are recommended, they are not obligatory for running Docker on Linux.


	First we create a Docker group. 
	
	```
	$  sudo groupadd docker
	```
	
	Next, we  add our username to the group. Make sure to replace $USER by your own username. 
	
	```
	$ sudo usermod -aG docker $USER
	```

	Now we have to activate these changes to our group and verify that we can use the Docker command without the sudo prefix.
	
	```
	$ newgrp docker
	```
	
	```
	$ docker run hello-world
	```
	
	You should now see a message in your terminal that your installation works correctly. If you obtain any errors, make sure to check out the [troubleshooting guide](https://docs.docker.com/engine/install/linux-postinstall/#troubleshooting) in the Docker docs.  

5. Get the Nvidia container toolkit. This toolkit is required to ensure compatibility between your Nvidia driver and Docker. Run the following commands in your newly installed Ubuntu terminal.

	```
	$ distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
	```

	```
	$ curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add
	``` 

	```
	$ curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
	```	

6. You can now install the toolkit through the following lines. 

	```
	$ sudo apt-get update
	```

	```
	$ sudo apt-get install -y nvidia-docker2
	```

	After installation it may be a good idea to restart your computer to finalize all installations. 

7. Test a benchmark Docker container.  First, start Docker desktop by running the Docker desktop app. To verify that the installation has been successful we will run a benchmark test with a Nvidia Docker image that requires a GPU. When this test is successful, you should see that your GPU is displayed in the output. 

	```
	$ docker run --gpus all nvcr.io/nvidia/k8s/cuda-sample:nbody nbody -gpu -benchmark               
	```
<br>