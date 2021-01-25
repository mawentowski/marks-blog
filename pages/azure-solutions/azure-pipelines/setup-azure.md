---
title: Configure Storage Account to Host a Static Site
sidebar: azure-solutions_sidebar
permalink: setup-azure.html
folder: azure-solutions/azure-pipelines
summary: This section walks you through the process of configuring an Azure storage account to host a static site in a blob container, including signing up for a new personal Azure account and a 30-day free trial subscription.
---
<!-- ## 
This is the "Product menu" name not included in header. It
will include a range of topics relating to using Azure and
its totality, not just for hosting static sites.
-->

<!--
# Setting up Azure storage static website for Jekyll
This is the introductory page and the start of the blog
-->
{% include important.html content="The process described herein is intended for demonstrative purposes only to highlight Azure's capabilities. You are encouraged not to use an Azure account linked to a company you do not own, and so instructions for creating a new Azure account for personal use are included. The configuration of the security settings of storage accounts linked to your organization needs to be based on your organization's security requirements." %}

<!-- Move this to separate intro section
## Prerequisites:
 - Google Chrome 
 -->

## Sign Up for a new Mircosoft Account
A Microsoft account is required to sign up for a Microsoft Azure account, and the easiest way to set up an account is to sign up for Outlook email.

If you already have a personal Microsoft Outlook email you would like to use to complete these steps, you may skip this step. 

{% include tip.html content="It is recommended to create a new Microsoft account to keep any existing business or personal accounts separate." type="primary" %} 

<!-- They can do this from Azure homepage, change this.. -->
*To create a new Microsoft account:*
1.  Go to [https://outlook.live.com](https://outlook.live.com/owa/).
1.  Click **Create Free Account**.
1.  Follow the instructions to create a free account.
    - With a Microsoft account, you may now sign up for an Azure account.

## Sign Up for Azure
Azure is a cloud platform that provides cloud services, most notably storage accounts to host static sites. You must associate your Microsoft account to your Azure account.

*To sign up for Azure:*
1.   Go to the [Azure homepage](https://azure.microsoft.com).
     * If you are already signed in to an Azure account (perhaps your work account), then your name will display instead of **Sign In**. If you are signed into your work account, click **Sign Out**.
1.   Click **Free account** to create a new Azure account.
1.   Click **Start Free**.
1.   Select the outlook email address you created earlier to associate to the Azure account.
1.   Follow the onscreen directions to create the Azure account.
   - Once complete, you are directed to your Azure Portal (i.e. your personal Azure landing page).

## Create New Subscription
Sign up for a free trial subscription that includes a storage account you will use to host your static site.

{% include note.html content="The free account gives you $200 of free services for 30 days, after which you will be prompted to upgrade to another plan like pay as you go." %}
{% include note.html content="This is my note. All the content I type here is treated as a single paragraph." %}
To create a new subscripton:
1. Click **Storage accounts** underneath **Azure Services**. Alternatively, click the hamburger menu icon in the top-left corner and select it there.
1. You are notified you currently do not have a subscription.
1. Follow the instructions to create a new subscription account.
   - You now return to your Azure portal landing page. 

## Create a New Storage Account
Azure Storage is a Microsoft-managed service providing cloud storage. In this case, you will be hosting your static site through this service.

To create a storage account:
1. Click **Storage Accounts** again.
1. Click **Create Storage Account** below the **No storage accounts to display** message.
   - You are directed to the **Create storage account** page.
   - By default, **Free Trial** is selected as your subscription.

### Fill out Basics tab

1. Under **Resource group**, click the **Create new** link.
1. Name it `jekyll-site`.

{% include note.html content="A resource group is a container that holds related resources for an Azure solution" %}

1. Enter a **Storage account name**, for example, **staticsiteshost** (this name will not be available, but you get the idea).

{% include note.html content="The naming used for the resource group and storage account is only an example. When you deloy your own static site, you will want to change the naming to conform to your company standards. View the article [Considerations for naming Azure resources](https://docs.microsoft.com/en-us/azure/azure-government/documentation-government-concept-naming-resources) for more information." %}

1. Pick the **Location** from the drop-down menu that makes the most sense. If it is correct, leave it be. For example, I live in the Netherlands so the most relevant location is `(Europe) North Europe`. 
1. Ensure the **Standard** radio button is selected.
1. Ensure the Account kind is **StorageV2**.
   - This is important because static site hosting is no longer available for a **V1** account.
1. Ensure **Read-access geo-redudant..** option is selected.

### Fill out Networking tab

1. Click ****Next: Data protection** at the bottom of the page, or click the **Networking** tab at the top.
1. Select **Public endpoint (all networks)** as the **Connectivity method**.
<!-- You want this to be private, but I do not know how to add a virtual network or what that is. Lets do this from gmail account instead. until you
ask about what needs to be done. -->

### Review changes and create the storage account
1. Click **Review + create** at the bottom of the page, or click the **Review + create** tab at the top.
1. Confirm you have the correct settings selected based on the previous instructions and click **Create**.
1. Click **Go to Resource** at the bottom.
   - You are directed to the new storage account's page.

## Configure the Static Website
1. Click **Static website** from the side navigation.
1. Click the **Enabled** radio button.
1. Enter `index.html` in the **Index document name** field.
1. Enter `404.html` in the **Error document path** field.
   - A **successfully updated...** message should display in the top-right corner, and a primary/secondary endpoint should also display on the page.
1. Copy the **Primary endpoint** and store it somewhere for retrieval later.

   Your screen should look similar to below:



{% include image-tom.html file="staticsite-config.png" alt="Jekyll" caption="Enable Static Website for Storage Account" %}

{% include note.html content="The Primary endpoint is the address where you can see your static site after publishing. It is recommended you save this endpoint to your browser as you will be visiting it a lot." %}

<!-- Insert next button like Tom's blog-->
The next step is to create build and release pipelines inside Azure Dev Ops that deploy your site to the blob storage container.

<!-- 
Read this:
https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-static-website


<!-- What you are modifying. Content is less technical. More background information like setting up azure accounts. More stepped based than explanations -->

<!-- I remember you had a problem with blob storage now that I remember, another question to have>

<!-- 
/subscriptions/<subscriptionID>/resourceGroups/<ResourceGroupName>/providers/<ResourceProvider>/<ResourceType>/<ResourceName>
-->

<!-- Include test repo to demonstrate the Azure pipeline, your template!! Or bare bones template -->