# Set Up Git Repositories
This section guides you through the process of downloading a sample Jekyll project from GitHub locally so it can be pushed the your remote repo in Azure. 

## Summary of Previous Actions
In the previous section, you:
- Signed up for a new Azure account.
- Created a new free trial subscription.
- Created a new storage account.
- Configured the static website from within your storage account.

As a result, Azure generated a primary endpoint to access your new site and also created a new [blob container](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction#:~:text=Azure%20Blob%20storage%20is%20Microsoft's,as%20text%20or%20binary%20data.) called `$web`.
## Sign In to Azure DevOps
1. Go to [https://dev.azure.com](https://dev.azure.com).
1. If you are automatically signed in, click the circle with your initials in the top-right corner. 
1. If this is your work account (company email), select the account you created in the previous section, click **Sign in with a different account**.

## Create New Organization
1. After signing in, click **Create a new organization**.
1. Follow the onscreen prompts until you reach the **Create a project to get started** screen.
1. Name the project something like `jekyll-project`.
1. Select **Private** and create the project.

Tip: <!-- Add tip formatting -->Bookmark the URL of the location of your project for ease of access later.

## Download Sample Jekyll Project from GitHub
1. Go to [https://github.com/gpeipman/JekyllBlog](https://github.com/gpeipman/JekyllBlog).
1. Click **Code** drop-down.
1. Select **Download Zip**
1. Download the `jekyll-project` project to a dedicated location for your git repositories on your computer.
   - For example, you can create a folder called `Repos` in your **Documents** folder on your root directory.

{% include note.html content="Always store your git repositories on your root directory, otherwise you may encounter permissions errors. For Windows, your root directory may be `C:\Users\Mark.Wentowski\`. *Add Mac root directory and reference to setting up dev environment.*" %}

{% include note.html content="Note that you are downloading only the project files at this stage. When downloading a project, there is no  `.git` folder, and thus it is not a git repository yet. You will create the git repo that encompasses the project files in a later step." %}

1. After downloading the file to the desired location, unzip it.
   - *On Windows*, you can right-click the zipped file and select **Extract** all.
   - *On Mac*, ...

<!-- Talk about difference between project and repo -->
<!-- Look up cost for hosting mutliple files and how that is possibe. Also definitions of resources, etc. -->
## Set Up Local Git Repo
### Navigate to the project directory
<!-- Do a more thorough view of this like looking at file explorer in setting up dev evironment -->
1. Open a terminal:
   - *For Windows*, go to your search bar and type `command prompt`, and select it. Alternatively, you can use Powershell.
   - *For Mac*, locate **Shell** from your launchpad (go back and reveiw this).
1. Change working directory:
   - *For Windows*, your current folder location will be something like `C:\Users\firstName.lastName>`. Type `cd` followed by the relative (correct term?) path to the jekyll project. For example, `C:\Users\firstName.lastName\Documents\Repos\jekyll-project`.
   - *For Mac*, ...
### Initialize a Git Repo
1. Type `git init` to initialize a new git repo that is now tracking your project files.
<!-- It is confusing when switching between regular file explorer to command line -->
1. Navigate to your project folder using **File Explorer** *on Windows*, or (add here) <!-- Go over how to add extension for file explorer on Mac-->*on Mac*.
1. Confirm the **.git** folder is inside your project folder. If you do not see it, see the next section.

### Verify Location of Git Folder
On *Windows*:
1. Ensure you are using **File Explorer** (and not Command Prompt), and you are located within your project folder.
1. Verify if the **.git** folder is present. If so, skip the next steps. If not, continue.
1. Click the **View** tab at the top.
1. Click the **Options** drop-down arrow and select **Change folder and search options**.
1. Select the **Show hidden files, folders, and drives** radio button.
1. Click **Ok**.
   - The **.git** folder should now be visible inside your project folder.

*On Mac*:
   - Fill in.

{% include note.html content="If the **.git** folder is still not visible, you likely initialized your git directory either within the parent folder of your project, or within one of your project folders. If you locate the .**git** folder in either of these locations, delete it, then initialize a new git repo from within your project folder. Not initalizing the git repo in your project folder will cause you a massive headache later." %}

### Establish Connection to Remote Repo
1. Go to [https://dev.azure.com](https://dev.azure.com), sign in to your account (not work account), and open your Jekyll project.
1. From inside your project in Azure DevOps, click **Repos**.
   - You should be located within the **Files** folder therein.
1. With the HTTPS button selected (usually by default), click the copy button. <!-- Show screenshot -->
   - The repo URL is now copied to your clipboard.
   <!-- Do this process in source tree next time -->
1. Switch back to your terminal (i.e. Command Prompt/Powershell *for Windows* or Bash *for Mac*). <!--bash or shell? -->
1. Ensure you are located within your project directory.
1. Type `git remote add origin` followed by the URL you copied previously.
   - Example: `git remote add origin https://outlookUser@dev.azure.com/outlookUser/jekyll-project/_git/jekyll-project`
1. Type `git remote show origin` to confirm the connection between your local repo (on your machine) and the remote repo (in Azure DevOps).
   - You may be prompted to sign into Azure.
### Commit Files Locally
1. Type `git add --all` to add the untracked files in your project to the staging area.
1. Type `git commit -m "first commit"` in your command line tool and hit Enter.
   - This command commits the project's tracked files to your local repo. <!-- ALERT! -->They still need to be pushed to the local repo.
### Push Local Files to Remote Repo
1. Type `git push --set-upstream origin master`.
   - This sets the remote repo as "upstream" and pushes your files to the remote repo on Azure.
1. From inside your project in Azure DevOps, click **Repos**, or refresh the page if you are already there.
   - You should now see the project files you pushed from your local git repo to this remote repo in Azure.



<!--Blog topic -- essential Visual Studio code tools for tech writers, mardown, spellcheck>
<!--
command line basics
Structure root vs personal
Press up and down to locate recent commands
Difference URLs mac and Windows.
pwd
Locate directory you want to put your git directory in file explorer
Cd to that directory
look at directory on computer, it is now there.
Do PWD directory and you will see you are one up from it
Do ls to list files
Copy the name of repo from the list
CD into directory cd marks-blog
git status
if you cloned a repo, then it will be up to date with origin/master
if you created a blank remote repo (like azure) then you need to do below command
Do git add --all, or do the A to add all of the files
git commit -a -m "random commit"
click trash can to delete terminal session
Cmd tilda to bring up terminal