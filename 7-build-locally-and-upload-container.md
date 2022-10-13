**<h3 class="text-center ">Exporting the container</h3>**
<br>

Another option to get your Algorithm running on Grand Challenge, is to build and export your container to a zip file and upload the zipped file to Grand Challenge. This not the recommended option anymore, for reasons related to maintainability.

If haven't already, run `.build.sh`.To export the container, run `./export.sh` and wait for a few minutes until the container gets created and zipped into a single file. 

#### **Uploading to grand-challenge.org** 

To create an Algorithm in grand-challenge.org, go to [this page](https://grand-challenge.org/algorithms/) and click on **+ Add a new algorithm** to create your algorithm page.  

We restrict access to this feature of Grand Challenge. If you do not see this button, write to us and explain your use case and funding possibilities. **Algorithms for challenges are handled differently. If you need to create an algorithm for a challenge, you can do so on the challenge submission page.** 

![](https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/04/01/51b86c8e-69d7-4342-b281-4925d9b58a0d.png) 

Create the basic page by answering the questionnaire about your algorithm. 

1. Prepare a Title and Logo
2. Set Flexible inputs to True if necessary
3. Select specific Inputs and Outputs interfaces
4. Choose CIRRUS Core as the default viewer
5. Set credits per job to ~10 to prevent abuse by approved users
6. Set GPU memory correctly
7. Set hanging protocol and view content to control how the results will be displayed in the viewer, see [here](https://grand-challenge.org/documentation/viewer-layout/).

Once the page is created, you can upload the `.tar.gz` file by clicking **Containers → Upload a Container**. 

![](https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/03/30/473dbaf9-3579-417f-a176-7e49cbb2d307.PNG)

 Wait for your Algorithm container to be active (usually &lt; 1 hour). If your new container is not active by then, please reach out to us.

💡 You do not have to create a new algorithm page for every update to your algorithm. You can simply upload your new container by going to **Containers → Upload a Container**.