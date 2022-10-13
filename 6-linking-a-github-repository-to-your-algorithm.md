

**<h3 class="text-center ">Linking a GitHub repository</h3>**

<br>
Instead of building a container image for your algorithm locally and uploading it to Grand Challenge, we recommend to link a GitHub repository to your Algorithm page. When a repository is linked to an algorithm, a new container image will be built automatically each time the repository is [tagged](https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/managing-commits/managing-tags#creating-a-tag). The following requirements need to be met for this workflow to properly work:

- There needs to be a Dockerfile in the repository's root. This Dockerfile will be used to build the image.
- The repository needs to have an open-source license. To ensure your license is valid, you can check if the license is listed in your repository's 'about' section: <br><img src="https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/11/24/8a258b0f-0e29-4101-9c1c-2484a5aeb1e4.png" width="300">
- The Grand Challenge GitHub app needs to be installed in the repository

The following licenses are currently recognized by Grand Challenge: Apache License 2.0, MIT License, GNU GPLv3, GNU AGPLv3, Mozilla Public License 2.0, Boost Software License 1.0, The Unlicense. If your open-source license is not listed here, please contact us at [support@grand-challenge.org](mailto:support@grand-challenge.org). 
<br>

#### **Add a new Algorithm on grand-challenge.org** 

To create an Algorithm in grand-challenge.org, go to [this page](https://grand-challenge.org/algorithms/) and click on **+ Add a new algorithm** to create your algorithm page.  

We restrict access to this feature of Grand Challenge. If you do not see this button, write to us and explain your use case and funding possibilities. **Algorithms for challenges are handled differently. If you need to create an algorithm for a challenge, you can do so on the challenge submission page.** 

![](https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/04/01/51b86c8e-69d7-4342-b281-4925d9b58a0d.png) 

Create the basic page by answering the questionnaire about your algorithm.

#### **Install Grand Challenge GitHub app** 

To install the Grand Challenge GitHub app, navigate to the `Containers` menu item on your algorithm's page and click the `Link GitHub Repo` button: 
<img src="https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/11/24/28caebdf-e39b-4437-aa18-e143d7b9e8ff.png" width="600"><br><br>

You will be shown a dropdown menu with repositories that already have the app installed. The dropdown will initially be empty. Click `link a new GitHub repo here` to link a new repository: 

<img src="https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/11/24/a907d052-662c-408d-8a62-6cc67daffc25.png" width="700">

You will now be redirected to GitHub. 

Complete the steps to install the app for the proper repository. You must have admin rights to the repository so that you can give permission for Grand Challenge to install an app there. 

**1. Select your GitHub account**

<img src="https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/12/23/e01dc310-565f-487c-8f9b-536ce51297cc.png" width="450">

**2. Select the GitHub repository you want to link to your algorithm**

<img src="https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/12/23/0138da70-3e0f-4da9-a5e4-6ecc21ab5e0b.png" width="450">

If you see a `request` badge, please see **Link a GitHub repository without admin access**. Click `Install and Authorize` after making your selection. You will now be redirected back to Grand Challenge, where you can select your repository in the dropdown menu. Click `Save` to link the repository to your algorithm. 

<img src="https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/12/23/1ee98bbf-8a0e-42af-8819-27229f578472.png" width="700">

The `Containers` menu item will now display the linked repository. 

<br>
#### **Build Docker Container** 
You can now start a new build for your algorithm by tagging your linked GitHub repository. A build will be started for each tag. Note that it could take a little while for the build to start as a worker needs to be available to start the build. The builds for your algorithm will be listed in the `Containers` menu item. You can view the build logs for each build by clicking the entry in the overview. 

<br>
##### **Tagging your repository** 
You can tag your repository using the [command line interface](https://git-scm.com/book/en/v2/Git-Basics-Tagging), [GitHub Desktop](https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/managing-commits/managing-tags#creating-a-tag), your favorite git program, or the web interface of GitHub. To tag your repository using the web interface of GitHub, create a new `release`. 

To create a new release, navigate to the repository's releases (at github.com/[your username]/[your repository name]/releases) and click `Draft a new release`: 

<img src="https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/12/23/8895758b-86a0-4f43-9a53-3dd07a568050.png" width="700">

Enter a name for your release to create the release and automatically tag your repository:

![](https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/12/22/36d98c41-aff4-45a2-a4ac-a629c64a6c30.png)

Click `Publish release`.

<br>
##### **Build process** 
After the repository is tagged, a Docker container will be created automatically using [AWS CodeBuild](https://docs.aws.amazon.com/codebuild/latest/userguide/concepts.html). You can see the progress of this build in the `Containers` menu item.  

<img src="https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/12/23/dd119e73-9639-4371-88a0-563cf712eba5.png" width="700"> 

The build logs can be viewed by clicking the `i` button. 

<img src="https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/12/23/aae8dae8-5e42-4c54-9e06-0b19bc49771a.png" width="700">

<br>
#### **Recurse Submodules** 
If your repository contains submodules that need to be cloned for the Docker build, enable `Recurse submodules` in the algorithm settings: 

**1. Update the algorithm settings**<br>
<img src="https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/12/23/493d0d86-2c0c-4674-bc8f-7809d5af188b.png" width="700">

**2. Enable Recurse submodules**<br>
<img src="https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/12/23/8c80ecd8-3138-4463-8799-7fb622477c61.png" width="450">

Click `Save` to store the change. 

<br>
#### **Link a GitHub repository without admin access** 
In case you want to link a GitHub repository you do not have admin access to, the workflow is a little different. This situation can arise, for example, if your repository is managed by your organisation instead of your personal GitHub account. You can recognise this situation from the `request` badge. 

<img src="https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/12/23/c8ab2753-ddfe-4515-b513-fe2f5a28963b.png" width="450">

In this case, ask the GitHub admin to install the Grand Challenge app for you. Your organization's GitHub admin can manually install the Grand Challenge app by navigating to [github.com/apps/grand-challenge/installations/new](https://github.com/apps/grand-challenge/installations/new) and selecting the required repositories.  This selection is similar to **2. Select the GitHub repository you want to link to your algorithm** above. However, this does not automatically link the repository to your algorithm. After the app is installed, you can manually link the repository to your algorithm by updating the `Repo name` in your algorithm settings. Write `[your organisation name]/[your repository name]` here:

<img src="https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/12/23/9a227b9f-c91a-41a9-859c-c0e7c552bd53.png" width="700">

Please note that a repository can only be linked to a single algorithm. 

<br>
#### **Uninstall Grand Challenge GitHub app** 
To uninstall the GitHub app, navigate to [github.com/settings/installations](https://github.com/settings/installations). Under `Installed GitHub Apps` click on `Configure` next to Grand Challenge. 

<img src="https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/12/23/f0cf9a21-9ad0-4fea-9fad-208809fe472a.png" width="700">

Scroll to the bottom and click `Uninstall`. 

<img src="https://rumc-gcorg-p-public.s3.amazonaws.com/i/2021/12/23/da571129-8601-4a62-b998-1fe7b1b4fe0c.png" width="700">

