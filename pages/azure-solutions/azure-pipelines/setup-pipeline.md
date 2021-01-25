---
title: Set up Pipeline
sidebar: azure-solutions_sidebar
permalink: setup-pipeline.html
folder: azure-solutions/azure-pipelines
---
# Set Up Build and Release Pipelines

## Build-Pipeline YAML File
 In the root directory of your project, there is a definition file called `build-pipeline.yml`.

 <!-- Insert screenshot? -->
 
 This file *defines* the build and release pipelines of your static site. In essence, whenever a build is triggered (ex. a commit or merge on the `master` branch), the commands in the `build-pipeline.yml` are executed.
 
 Jekyll commands are run to *build* the static site (i.e. build pipeline), then the *release* pipeline publishes the build to the storage account you set up previously in the blob container at `$web`. 

<!-- Info or tip.. -->
{% include note.html content="The same jekyll commands you would normally execute from the command line to build your site locally are performed here, except they are now executed automatically on the server. The process of automating the build and release of code is called *Continuous Integration/Deployment* in the DevOps world, and the aim here to apply the same principles using these pipelines to documentation projects." %}

 Once published, your static site can then be viewed at your static sites's endpoint (i.e. URL you type in the browser to view the site). The location of which was discussed in the previous section.

<!-- https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/ruby?view=azure-devops Good resource for Ruby apps!-->
### Summary of Executed Commands

- `gem install jekyll bundler` - Installs Jekyll.
- `bundle install` - Installs the dependencies specified in your Gemfile.
- `jekyll build` builds the site and outputs a static site to a directory called `_site` in your project.

After Jekyll successfully builds the site, the `_site` folder is copied to the build pipeline artifacts folder where it can be accessed for the build pipeline.

<!-- What happens in the Release pipeline? -->

<!-- Dont use quotes, use italics for emphasis. Use ex. for examples, i.e. for in other words, and use code snippet for file names. Bold for onscreen buttons, etc. -->
# Set Up Build Pipeline
1. Go to [https://dev.azure.com](https://dev.azure.com), sign in to your account (not work account), and open your Jekyll project.
1. From inside your project in Azure DevOps, click **Pipelines**.
1. Click **Create Pipeline**.
1. Select **Azure Repos Git**.
1. Select your Jekyll project.
1. Click **Existing Azure Pipelines YAML file**.
1. Under **Path**, select `/build-pipeline.yml`.
1. Click **Continue**.
   - A **Review your pipeline YAML** displays.
1. Click **Run** to run the build pipeline.
   - Under **Jobs**, **Status** should read `Success`.
1. Click `published` to confirm the static site has been published to the **Artifacts** folder. The `site` folder should be there as shown below.<!-- Elaborate on this. Also, show screenshot -->
<!-- Continue to Azure Storage Explorer to do a test upload, cannot figure this out -->
## Set Up Release Pipeline
1. Go to [https://dev.azure.com](https://dev.azure.com), sign in to your account (not work account), and open your Jekyll project.
1. Click **Pipelines**.
1. Click **Releases**.
1. If you are prompted to create a job, close this window.
1. Click the release name at the top and rename it to something like `Jekyll Release`.
1. Add a comment like `Renamed Pipeline.`

### Add an Artifact
1. Click **Add an artifact**.
1. Under **Source**, select your Jekyll project.
   - This tells the release pipeline to use the files (i.e. artifacts) generated from the build pipeline in the **Artifacts** folder as inputs.
   - The other fields should automatically populate.
1. Click **Add**.

### Add a Stage
Release pipelines contain alteast one stage compromised of one or more tasks.

1. In the **Stages** box, click the **Add** drop-down.
1. Select **New Stage**.
1. Click **Empty Job**.
1. For **Stage name**, type `Publish Artifacts`.
1. Close this window.
   - A stage is created with an empty job.
1. Click the `1 job, 0 task` link.
1. Click the plus icon next to **Agent job**.
1. In the search field, type `command`
   - **Command line** should display in the search results at the top.
1. Click **Add**.
1. Click **Command Line Script** underneath **Agent Job**.
1. For **Display Name**, enter `Clean Artifact Folder`.
1. In the **Script** box, type the following code:

<!-- See if there is snytax highlighting in output, bash causing
problems -->
```
del *.yml
del *.gemspec
````
1. For **Working Directory**, select the `site` folder and click **Ok**.

### Add an Azure CLI Job
1. Click the plus button next to **Agent job**.
1. Type `Azure CLI` in the search field, select it, then click **Add**.
   - The **Azure CLI** job has been added to the pipeline.
1. Click **Azure CLI** underneath **Agent Job**.
<!-- It cost 30 dollars to create the storage container and post files there -->
1. For **Display Name**, type `Upload Artifacts to Blob Container` 
1. For **Azure subscription**, click the drop-down arrow and select the `Free Trial` subscription.
1. Ensure you are using Google Chrome and not another browser, otherwise it may stall after entering your credentials.
1. Click **Authorize**.
1. Sign in using your username and password.
<!-- Need to get Hail to verify you are doing the most secure thing -->
1. For **Script Type**, select `Batch`.
1. For **Script Location**, select `Inline Script`.
1. Enter the following into the **Inline Script** box, replacing `account-name` with the name of your storage account: 

   `az storage blob upload-batch --source site --destination $web --account-name [INSERT STORAGE ACCOUNT NAME NO BRACKETS!] --output table --no-progres`.
1. For **Working Directory**, select your project folder (not site). Here is an example:
   -`$(System.DefaultWorkingDirectory)/_jekyll-project`
1. Click **Save** at the top.
1. For the **Comment**, enter something like `Initial version of release pipeline completed.`

### Create a New Release
1. Click **Create Release** at the top-right of the screen.
1. For **Stages for trigger...*, select `Publish Artifacts` (or a name you chose previously.)
1. For **Release description**, you may leave it blank.
1. Click **Create**.

### Deploy to Live Site
1. Click **Publish Artifacts** under **Stages**. 
  - You will notice it says *Not Deployed*.
1. Click the **Deploy** button.
1. Add a comment like `First deployment` and click **Deploy**.
   - If successful, it will say `Succeeded` under the name of the Agent job.

### Verify Site is Live
1. Go to Azure Storage Explorer and open the $web blog container.
   - You should see the static site files.
1. Go to Google Chrome, enter the endpoint (URL) of your site, and hit Enter.
1. Your static site should load




<!-- Idea! DO that Azure popup for context help. You access it by clicking help on the Pipelines page.-->
<!-- Setup Jenkinds with Github pages idea -->

## Handling Deleted Files
If files are deleted locally, then the release pipleine will not know to remove them from the live site.

My recommendation is to delete the files manually, both locally using Windows Explorer <!-- What about mac --> and from the live site using Azure Storage Explorer. You do not need to worry about the build pipeline, those files are always regenerated based on the files currently in your Azure repo.

An alternative is the "clean slate" approach where you remove all files from the live site before new ones are uploaded to the **Artifacts** folder after a build. That way, any deleted files will not be present the next time your site is published.

It may also be possible to add a job that somehow compares the files in the **Artifacts** folder after a build against the files in the live site, then subsequently looks for files no longer present and removes them. I have not experimented with this approach.

Either way, I do not believe it is too big a hassle to clean out the old files manually, but make the best decision for your situation.
