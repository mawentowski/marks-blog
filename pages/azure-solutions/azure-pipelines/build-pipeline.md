---
title: Build Pipeline
sidebar: azure-solutions_sidebar
permalink: build-pipeline.html
folder: azure-solutions/azure-pipelines
summary: This section guides you through the process of setting up the build pipeline that builds the jekyll site (i.e. produces build artifacts) that will then be used by the release pipeline to deploy the site.
---
## Summary of Previous Actions
In the previous section, you:
- Downloaded the sample Jekyll project and initialized a local git repo
- Established a connection to the remote repo in Azure and pushed the sample project files.

As a result, you may now create build and release pipelines that trigger based on changes made to the master branch of your remote repo in Azure.

## Build-Pipeline YAML File Explained
 In the root directory of your project, there is a definition file called `build-pipeline.yml`.

 <!-- Insert screenshot? -->
 
 This file *defines* the build and release pipelines of your static site. In essence, whenever a build is triggered (ex. a commit or merge on the `master` branch), the commands in the `build-pipeline.yml` are executed.
 
 Jekyll commands are run to *build* the static site (i.e. build pipeline), then the *release* pipeline publishes the build to the storage account you set up previously in the blob container at `$web`. 

<!-- Info or tip.. -->
{% include note.html content="The same jekyll commands you would normally execute from the command line to build your site locally are performed here, except they are now executed automatically on the server. The process of automating the build and release of code is called *Continuous Deployment* in the DevOps world, and the aim here to apply the same principles using these pipelines to documentation projects." %}

{% include image.html file="build-yaml.png" alt="build-yaml" caption="Project repo in Azure showing the YAML build file" %}

Once published, your static site can then be viewed at your static sites's endpoint (i.e. URL you type in the browser to view the site). The location of which was discussed in the previous section.

<!-- https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/ruby?view=azure-devops Good resource for Ruby apps!-->
### Summary of Executed Commands

- `gem install jekyll bundler` - Installs Jekyll.
- `bundle install` - Installs the dependencies specified in your Gemfile.
- `jekyll build` builds the site and outputs a static site to a directory called `_site` in your project.

After Jekyll successfully builds the site, the `_site` folder is copied to the build pipeline artifacts folder where it can be accessed for the build pipeline.

<!-- What happens in the Release pipeline? -->

<!-- Dont use quotes, use italics for emphasis. Use ex. for examples, i.e. for in other words, and use code snippet for file names. Bold for onscreen buttons, etc. -->
## Set Up Build Pipeline

The build pipeline executes the commands in `build-pipeline.yml`, which includes jekyll commands, as well as commands that copy the build artifacts so they can be published in the release pipeline to your storage account.

*To set up the build pipeline:*

1. Go to [https://dev.azure.com](https://dev.azure.com), sign in to your account (not work account), and open your Jekyll project.
1. From inside your project in Azure DevOps, click **Pipelines**.
1. Click **Create Pipeline**.

{% include image.html file="create-first.png" alt="create-first" caption="Pipelines page in Azure DevOps" %}

{:start="4"}
1. Select **Azure Repos Git**.
1. Select your Jekyll project.
1. Click **Existing Azure Pipelines YAML file**.
1. Under **Path**, select `/build-pipeline.yml`.
1. Click **Continue**.
   - A **Review your pipeline YAML** displays.
1. Click **Run** to run the build pipeline.
   - Under **Jobs**, **Status** should read `Success`.
   - If not, continue to [Troubleshooting Build Errors](build-pipeline.html#trouble)
1. Click `published` to confirm the static site has been published to the **Artifacts** folder. 

{% include image.html file="1-published.png" alt="1-published" caption="Build Summary Page" %}

  - The `site` folder should be present as a build artifact.

<h2 id="trouble">Troubleshooting Build Errors</h2>

While the`build-pipeline.yml file` you added to the project was designed to work with this sample project (hopefully), there is potential for errors if you are using the same build file with a different Jekyll project (such as when you implement this solution in the future). 

This is because most jekyll projects have unique `gem` files with different gem dependencies that require specific commands to be used (and not others). For example, certain jekyll projects require different build commands.

*For basic troubleshooting:*
1. Open the job (if not already open).
1. Look for the section of the build file that the build failed on, indicated by a red marker.
1. Read the message associated with build failing.
   - Sometimes the suggestions to resolve the issue are helpful, othertimes they are too obscure to understand fully (especially when dealing with gem dependencies).
1. Try to resolve the issue based on the error message received.
   
The most common issue I came across was during the execution of jekyll build commands. If you are using `bundle exec jekyll build` in the build file, try `jekyll build`, or vice versa.

## Upload and View Manaully
These steps demonstrate how to manually download the build artifacts, upload them to blob storage, then view the site at the static site's endpoint in the browser.

{% include tip.html content="These steps are optional, but it is a good way to understand the publication process that the release process will automate." type="primary" %}

*To upload and view your site:*
1. Click the 3 dots next to `site` folder and select **Download Artifacts**. 
1. Save the folder to anywhere on your computer.
1. Unzip the folder (any method).
1. Open **Azure Storage Explorer** and open the `$web` folder.
1. Click the **Upload** button.
   - A **Upload folder** popup displays.
1. Click `No folder selected`.
1. Navigate to, and select the `site` folder you downloaded previously.
1. Leave the other fields as is and click **Upload**.
1. Go to your browser.
1. Enter your static site's endpoint (i.e. URL) and hit Enter.
   - The static site should display.
1. Delete the `site` you uploaded to Azure Storage.

{% include callout.html content="Now that the build pipeline has been set up to build the static site, the next step is to set up the release pipeline to deploy the site." type="success" %}


<!-- Elaborate on this. Also, show screenshot -->
<!-- Continue to Azure Storage Explorer to do a test upload, cannot figure this out -->

