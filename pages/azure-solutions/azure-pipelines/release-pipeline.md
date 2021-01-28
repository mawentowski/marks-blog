---
title: Release Pipeline
sidebar: azure-solutions_sidebar
permalink: release-pipeline.html
folder: azure-solutions/azure-pipelines
summary: This section guides you through the process of creating and configuring the release pipeline to publish the build artifacts.
---
{% include note.html content="The Release pipeline takes the build artifacts and uploads them to the blob storage container in your storage called `$web`." %}

## Summary of Previous Actions
In the previous section, you:
- Set up the build pipeline
- Manually uploaded your site Storage Explorer

As a result, you may now create a release pipeline later triggers after a successful build and deploys the static site.

## Set up the Release Pipeline
*To set up the release pipeline:*
1. Go to [https://dev.azure.com](https://dev.azure.com), sign in to your account (not work account), and open your Jekyll project.
1. Click **Pipelines**.
1. Click **Releases**.
1. If you are prompted to create a job, close this window.
1. Click the release name at the top and rename it to something like `Jekyll Release Pipeline`.
1. Add a comment like `Renamed Pipeline.`

### Add an Artifact

Artifacts are created after a successful build and are now available to the release pipeline to use as inputs.

*To add an artifact:*
1. Click **Add an artifact**.

{% include image.html file="add-artifact.png" alt="add-artifact" caption="New release pipeline page" %}

{:start="2"}
1. Under **Source**, select your Jekyll project.
   - This tells the release pipeline to use the files (i.e. artifacts) generated from the build pipeline in the **Artifacts** folder as inputs.
   - The other fields should automatically populate.
1. Click **Add**.
   - The release pipeline now will use the build artifacts as inputs.

### Add a Stage

Release pipelines contain alteast one stage compromised of one or more tasks. A stage is just a way of grouping tasks in a logical order.

*To add a stage:*

1. In the **Stages** box, click the **Add** drop-down.
1. Select **New Stage**.

<!-- Need new screenshot of this -->
1. Click **Empty Job**.
1. For **Stage name**, type `Publish Artifacts`.
1. Close this window.
   - A stage is created with an empty job.
1. Click the `1 job, 0 task` link.

{% include image.html file="1-job-0-task.png" alt="1-job-0-task" caption="Showing published artifacts release pipeline" %}

{:start="5"}
1. Click the plus icon next to **Agent job**.
1. In the search field, type `command`
   - **Command line** should display in the search results at the top.
1. Click **Add**.

{% include image.html file="agent-job.png" alt="agent-job" caption="Showing how to add a command line task" %}

{:start="8"}
1. Click **Command Line Script** underneath **Agent Job**.
1. For **Display Name**, enter `Clean Artifact Folder`.
1. In the **Script** box, type the following code:

<!-- See if there is snytax highlighting in output, bash causing
problems -->

```shell
del *.yml
del *.gemspec
````

{:start="11"}
1. For **Working Directory**, select the `site` folder and click **Ok**.

### Add an Azure CLI Job

The Azure CLI job uploads the build artifacts to the `$web` blob container where it can be accessed by a browser.

*To add an Azure CLI job:*

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

   - The task should look like the following:

{% include image.html file="upload-artifacts.png" alt="upload-artifacts" caption="Upload artifacts task populated with data" %}

1. For **Working Directory**, select your project folder (not site). Here is an example:
   -`$(System.DefaultWorkingDirectory)/_jekyll-project`
1. Click **Save** at the top.
1. For the **Comment**, enter something like `Initial version of release pipeline completed.`

{% include callout.html content="Now that a release pipeline has been created, you can create a release and manually trigger the pipeline for testing purposes." type="success" %}