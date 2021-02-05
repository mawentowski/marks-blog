---
title: Git Repositories
sidebar: azure-solutions_sidebar
permalink: git-repos.html
folder: azure-solutions/azure-pipelines
summary: This section guides you through the process of downloading a sample static site project from GitHub locally so it can be pushed the your remote repo in Azure. 
series: "Azure Solutions"
weight: 2.0
---
{% include series/series-button.html %}
<!-- Add note on distinction of shell sessions -->
## Summary of Previous Actions
In the previous section, you:
- Signed up for a new Azure account.
- Created a new free trial subscription.
- Created a new storage account.
- Configured the static website from within your storage account.

As a result, Azure generated a primary endpoint to access your new site and also created a new [blob container](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction#:~:text=Azure%20Blob%20storage%20is%20Microsoft's,as%20text%20or%20binary%20data.) called `$web`.

## Prerequisites
The following are required to complete this section:
- **Visual Studio Code**, or another text editor.
- **Git Bash**, if using Windows (comes with installation of Git)
- **Azure** account and free subscription (covered previously)
- **Ruby 2.5** or newer (full install)
- **Jekyll** (free)
- **Azure Storage Explorer** (free)

## Sign In to Azure DevOps
1. Go to [https://dev.azure.com](https://dev.azure.com).
1. If you are automatically signed in, click the circle with your initials in the top-right corner. 
1. If this is your work account (company email), select the account you created in the previous section, click **Sign in with a different account**.

## Create New Organization
An organization in Azure, according to Microsoft, "is mechanism for organizing and connecting groups of related projects". The organization is based on the organizational structure of a business (i.e. divisions). The organization you create does not need to take these factors into consideration, as only a basic organization is required to complete these steps.

*To create an organization:*
1. After signing in, click **Create a new organization**.

{% include image.html file="create-org.png" alt="create-org" caption="Get Started Page" %}

{:start="2"}
1. Follow the onscreen prompts until you reach the **Create a project to get started** screen.
1. Name the project something like `jekyll-proj`.
1. Select **Private** and create the project.

{% include tip.html content="Bookmark the URL of the location of your project for ease of access later." %}

{% include callout.html content="With the creation of an organization, you are now ready to set up your local repository and connect it to a remote repository in Azure DevOps." type="success" %}

## Download Sample Jekyll Project from GitHub
The static site you will deploy in Azure is a [Jekyll](https://jekyllrb.com/) site, a common static site generator used for blogs and other documentation projects.

{% include tip.html content="There are several methods for accessing the sample project's code on GitHub. However, it is recommended you do not clone or fork the sample repository. Instead, simply download the project as a zip file onto your machine." %}

*To download the project:*
1. Go to [https://github.com/gpeipman/JekyllBlog](https://github.com/gpeipman/JekyllBlog).
1. Click **Code** drop-down.
1. Select **Download Zip**

{% include image.html file="download-zip.png" alt="download-zip" caption="Git Repo Sample Project" %}

{:start="4"}
1. Download the `jekyll-proj` project to a dedicated location for your git repositories on your computer.
   - For example, you can create a folder called `Repos` in your **Documents** folder on your root directory.

{% include important.html content="Always store your git repositories in your root directory, otherwise you may encounter permissions errors. Your root directory is something like `C:\Users\firstName.lastName\` for Windows and `/Users/userName/` for Mac." %}

{:start="5"}
1. After downloading the file to the desired location, unzip it.

{% include note.html content="There is no `.git` folder yet because it is not a git repository yet." %}

{% include callout.html content="With the sample project downloaded, you will initialize a local git repo encompassing your project files as described in the next steps.." type="success" %}

<!-- Talk about difference between project and repo -->
<!-- Look up cost for hosting mutliple files and how that is possibe. Also definitions of resources, etc. -->
## Set Up Local Git Repo

{% include note.html content="In the following section, there are numerous references to running different commands *on the command line*. This is referring to the use of a command-line interface (CLI) like **Command Prompt**/**Powershell**/**Git Bash** *on Windows*, or the **Terminal** app *on Mac* (in addition to other command-line tools on either OS)." %}

### Initialize a Git Repository
Initializing a git repository on your project creates a `.git` folder. The project will now be tracked locally in source control. 

{% include important.html content="You must initialize the `git` repository from the top-level directory in your sample project, as described in the next steps. Otherwise, you will likely encounter errors." %}

*To initialize a repo:*
1. Navigate to the project directory where you downloaded the sample project.
1. Type `git init` to initialize a new git repo that will now track your project files.
<!-- It is confusing when switching between regular file explorer to command line -->
1. Navigate to your project folder using **File Explorer** *on Windows*, or **Finder** on *Mac*.
1. Confirm the `.git` folder is inside your project folder. If it is not visible, ensure that [hidden files](git-repos.html#verify) are revealed.

{% include warning.html content="If the **.git** folder is not visible and hidden files are visible, you likely initialized your git directory either within the parent folder of your project, or within one of your project folders. If you locate the .**git** folder in either of these locations, delete it, then initialize a new git repo from within the top-level directory of your project folder. Not initalizing the git repo in your project folder will cause issues later." %}


<h3 id="verify">Display Hidden Files</h3>

It is important that hidden files are displayed so you can verify the location of your `.git` folder after initializing a git repo.

On *Windows*:
1. Ensure you are using **File Explorer** (and not another command-line tool), and you are located within your project folder.
1. Verify if the `.git` folder is present. If not, continue.
1. Click the **View** tab at the top.
1. Click the **Options** drop-down arrow and select **Change folder and search options**.
1. Select the **Show hidden files, folders, and drives** radio button.
1. Click **Ok**.
   - The `.git` folder should be visible inside your project folder.

{% include image.html file="reveal-hidden-win.png" alt="reveal-hidden-win" caption="Hidden Git folder revealed" %}

{% include note.html content="Hidden files display in File Explorer are transparent. You will notice the `.git` folder is transparent because it is a file normally hidden from view." %}

*On Mac*:
1. Ensure you are using **Finder** (and not another command-line tool), and you are located within your project folder.
1. Hold down `cmd + shift + [.]`.
   - The **.git** folder should be visible inside your project folder.
<!-- Add Mac screenshot -->

### Commit Files Locally

After you download a sample project and initialize a Git repo, all the files in the repository are *untracked*, which means Git does not recognize the project files yet. You must `add` the files to tell Git they exist, then commit them locally.

*To commit files locally:*
1. Type `git add --all` to add the untracked files in your project to the staging area.
1. Type `git commit -m "first commit"` in your command line tool and hit Enter.
   - This command commits the project's tracked files to your local repo. 

{% include important.html content="While committing the files creates a save state locally, they still need to be pushed to the repo remote to be visible in Azure and made available to pipelines." %}

### Establish Connection to Remote Repo
Before committing files to your Azure DevOps remote repository, you must configure your local repository to use your DevOps repo as its remote. You will need to copy your remote repository's HTTPS link in Azure DevOps.

*To acquire the HTTPS link:*
1. Go to [https://dev.azure.com](https://dev.azure.com), sign in to your account (not work account), and open `jekyll-proj`.
1. From inside your project in Azure DevOps, click **Repos**.
1. With the **HTTPS** button selected (usually by default), click the copy button. <!-- Show screenshot -->

{% include image.html file="copy-remote.png" alt="copy-remote" caption="Repo tab of Azure DevOps" %}
   - The repo URL is now copied to your clipboard.
   <!-- Do this process in source tree next time -->

*To set the remote repo as origin:*

1. Open your command-line tool.
1. Ensure you are located within your project directory.
1. Type `git remote add origin` followed by the URL you copied previously from Azure DevOps.
   - *Example:* `git remote add origin https://outlookUser@dev.azure.com/outlookUser/jekyll-proj/_git/jekyll-proj`
1. Type `git remote show origin` to confirm the connection between your local repo (on your machine) and the remote repo (in Azure DevOps).
   - You may be prompted to sign into Azure.

### Push Local Files to Remote Repo
1. Type `git push --set-upstream origin master`.
   - This sets the remote repo as "upstream" and pushes your files to the remote repo on Azure.
1. From inside your project in Azure DevOps, click **Repos**, or refresh the page if you are already there.
   - You should now see the project files you pushed from your local git repo to this remote repo in Azure.

{% include callout.html content="With your project files now pushed to Azure, you are ready to beginning setting pipelines to build and publish your static site." type="success" %}

{% include series/next-button.html %}

<!--Blog topic -- essential Visual Studio code tools for tech writers, mardown, spellcheck>

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
-->