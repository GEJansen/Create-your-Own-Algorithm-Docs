**<h3 class="text-center ">Cloning a repository from a Challenge baseline Algorithm </h3>**

<br>
For Algorithm submission to Type II challenges, we recommend cloning the repository of the baseline Algorithm of the Challenge, if the organizers made one available. As Challenge repositories sneed to be private, we cannot simply fork the baseline repository, because GitHub doesn't allow it. [Instead](https://docs.github.com/en/repositories/creating-and-managing-repositories/duplicating-a-repository), before we can start editing, we must clone the baseline, push it to our own repository,  and then clone that repo.  

To do so, first make sure to have [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and [git-lfs](https://docs.github.com/en/repositories/working-with-files/managing-large-files/installing-git-large-file-storage) installed on your local computer, and create a [GitHub](https://github.com/) account, if you do not already have one. On GitHub, create a new repository and set it to private. We will call it `your-repo` (but pick a name you like). Next, clone the **baseline** repository in your local (git-bash) terminal:


    $ cd /path/to/home
    $ git clone --bare https://github.com/ChallengeOrganizer/algorithm-baseline.git
    
Replace `path/to/home` with your desired home path, and replace the URL with the URL of the actual challenge baseline repository (+`.git`). Then go to the baseline repository folder, push it to `your repo` , and (optionally) delete the original:

    $ cd algorithm-baseline.git
    $ git push --mirror https://github.com/YourUsername/your-repo.git 
    $ cd ..
    $ rm -rf algorithm-baseline.git
    
Then finally, clone your own repository:

    $ git clone https://github.com/YourUsername/your-repo.git

#### **Bring your own Algorithm in process.py** 
The next step is to bring your algorithm into the process.py script, by swapping out the baseline algorithm with yours. Hopefully, it will be as simple as changing the model definition, and copying your model weights to the folder. 

When you're adding additional files, such as your model weights, you have to edit the Dockerfile, by adding the following line for every additional file:

    COPY --chown=algorithm:algorithm checkpoint /opt/algorithm/checkpoint

Replace both instances of `checkpoint` with the file path that you need for your Algorithm to run.
In addition, any additional dependencies will need to be added to the **requirements.txt** file with the version number specified, which looks like this:

    evalutils==0.3.0
    scikit-learn==1.0
    scipy==1.6.3
    scikit-image==0.18.1

#### **Commit and push changes to your own repository**

When you're done, commit and push your local repository to your own GitHub repository:

    $ cd your-repo.git
    $ git add --all
    $ git commit -m "First commit to my own Algorithm repo" 
    $ git push

The next step is to [link](https://grand-challenge.org/documentation/linking-a-github-repository-to-your-algorithm/) your newly created repository to an Algorithm submission. This means that the Algorithm will be built in the cloud by Grand Challenge. If the building phase fails because of some bug that snuck into your code, we advise to test and debug locally. In that case, we would recommend to install Docker in a (virtual) Linux environment, the Windows 11 guide for this can be found [here](https://grand-challenge.org/documentation/setting-up-wsl-with-gpu-support-for-windows-11/). This allows you test and debug locally, as explained in the next subtab.
