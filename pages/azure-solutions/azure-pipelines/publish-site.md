---
title: Publishing the Site
sidebar: azure-solutions_sidebar
permalink: publish-site.html
folder: azure-solutions/azure-pipelines
summary: This section guides you through the process of manually triggering a release so the release pipeline deploys the jekyll site to blob storage.
---
## Summary of Previous Actions

In the previous section, you set up the release pipeline.

As a result, you may now create a release and manually trigger the pipeline for testing purposes.

## Create a New Release

Creating a release is a way to initiate a release pipeline manually, as opposed it being initiated automatically after a build. This approach is done here for testing purposes only. The goal is to have the pipelines automatically initiated whenever a change is committed to the master branch of the repo.

*To create a new release:*
1. Click **Create Release** at the top-right of the screen.
1. For **Stages for trigger...**, select `Publish Artifacts` (or a name you chose previously.)
   - For this release, the `Publish Artifacts` stage is set to trigger manually instead of automatically after a build
1. For **Release description**, you may leave it blank.

{% include image.html file="create-release.png" alt="create-release" caption="Showing published artifacts release pipeline" %}

{:start="4"}
1. Click **Create**.
   - A message displays indicating that the release was successfully created.

{% include image.html file="release-link.png" alt="release-link" caption="Release successfully created message with link" %}

{:start="5"}
1. Click the link in the message to go to the release's page.

### Deploy to Live Site

You may now manually trigger (i.e. deploy) the release from the release page.

*To deploy to the live site:*
1. Click **Publish Artifacts** under **Stages**. 
  - You will notice it says *Not Deployed*.
1. Click the **Deploy** button.

{% include image.html file="deploy.png" alt="deploy" caption="Release pipeline page" %}

{:start="5"}
1. Add a comment like `First deployment` and click **Deploy**.
   - If successful, it will say `Succeeded` under the name of the Agent job.

{% include callout.html content="After successfully deploying the release, your site as now been upload to the `$web` blob storage container. You may now view your site at your static site's primary endpoint." type="success" %}

{:start="6"}
1. Go to **Azure Storage Explorer** and open the `$web` blog container.
   - You should see the static site files.
1. Go to **Google Chrome**, enter the endpoint (URL) of your site, and hit **Enter**.
   - Your static site should load in the browser.




<!-- Idea! DO that Azure popup for context help. You access it by clicking help on the Pipelines page.-->
<!-- Setup Jenkinds with Github pages idea -->

## Managing Deleted Files
If files are deleted locally, then the release pipleine will not know to remove them from the live site.

My recommendation is to delete the files manually, both locally using Windows Explorer <!-- What about mac --> and from the live site using Azure Storage Explorer. You do not need to worry about the build pipeline, those files are always regenerated based on the files currently in your Azure repo.

An alternative is the "clean slate" approach where you remove all files from the live site before new ones are uploaded to the **Artifacts** folder after a build. That way, any deleted files will not be present the next time your site is published.

It may also be possible to add a job that somehow compares the files in the **Artifacts** folder after a build against the files in the live site, then subsequently looks for files no longer present and removes them. I have not experimented with this approach.

Either way, I do not believe it is too big a hassle to clean out the old files manually, but make the best decision for your situation.
