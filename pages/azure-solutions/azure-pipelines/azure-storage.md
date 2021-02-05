---
title: Azure Storage Account
sidebar: azure-solutions_sidebar
permalink: azure-storage.html
folder: azure-solutions/azure-pipelines
summary: This section walks you through the process of configuring an Azure storage account to host a static site in a blob container, including signing up for a new personal Azure account and a 30-day free trial subscription.
series: "Azure Solutions"
weight: 1.0
---
{% include series/series-button.html %}
<!-- ## 
This is the "Product menu" name not included in header. It
will include a range of topics relating to using Azure and
its totality, not just for hosting static sites.
-->

<!--
# Setting up Azure storage static website for Jekyll
This is the introductory page and the start of the blog
-->
{% include warning.html content="The process described herein is intended for demonstrative purposes only to highlight Azure's capabilities. You are encouraged not to use an Azure account linked to a company you do not own, and so instructions for creating a new Azure account for personal use are included. The configuration of the security settings of storage accounts linked to your organization needs to be based on your organization's security requirements." %}

<!-- Move this to separate intro section
## Prerequisites:
 - Google Chrome 
 -->

## Sign Up for a new Mircosoft Account
A Microsoft account is required to sign up for a Microsoft Azure account, and the easiest way to set up an account is to sign up for Outlook email.

If you already have a personal Microsoft Outlook email you would like to use to complete these steps, you may skip to [Sign Up for Azure](setup-azure.html#azuresignup).

{% include tip.html content="It is recommended to create a new Microsoft account to keep any existing business or personal accounts separate." type="primary" %} 

<!-- They can do this from Azure homepage, change this.. -->
*To create a new Microsoft account:*
1.  Go to [https://outlook.live.com](https://outlook.live.com/owa/).
1.  Click **Create Free Account**.

{% include image.html file="outlook-signup.png" alt="outlook-signup" caption="Sign up for an Outlook Email Address" %}

{:start="3"}
1.  Follow the instructions to create a free account.

{% include callout.html content="With a Microsoft account, you may now sign up for an Azure account." type="success" %}

<h2 id="azuresignup">Sign Up for Azure</h2>

Azure is a cloud platform that provides cloud services, including the ability to create storage accounts to host your static sites. You must associate the Microsoft account you created previously to your new Azure account.

*To sign up for Azure:*
1.   Go to the [Azure homepage](https://azure.microsoft.com).
     * If you are already signed in to an Azure account (perhaps your work account), then your name will display instead of **Sign In**. If you are signed into your work account, click **Sign Out**.
1.   Click **Free account** to create a new Azure account.

{% include image.html file="azure-free.png" alt="azure-free" caption="Create free Azure account" %}
{:start="3"}
1.   Click **Start Free**.
1.   Select the Outlook email address you created earlier to associate to the Azure account.
1.   Follow the onscreen directions to create the Azure account.

{% include callout.html content="After successfully signing up for an Azure account, you are directed to your Azure Portal (i.e. your personal Azure landing page)." type="success" %}

## Create a New Azure Subscription
Sign up for a free trial subscription that includes a storage account you will use to host your static site. 

{% include note.html content="The free account gives you $200 of free services for 30 days, after which you will be prompted to upgrade to a paid plan. Also note that you may only use the subscription for one project (for example, when connecting to your subscription to the Azure CLI task)." %}

*To create a new subscripton:*
1. Click **Storage accounts** underneath **Azure Services**. Alternatively, click the hamburger menu icon in the top-left corner and select it there.

{% include image.html file="azure-services.png" alt="azure-services" caption="Select Storage Accounts" %}

{:start="2"}
1. You may be notified you currently do not have a subscription.
1. Follow the onscreen instructions to create a new subscription account.
   - You now return to your Azure portal landing page. 

{% include callout.html content="After signing up for a new subscription, you return to your landing page. You may now create a new storage account to host your static site." type="success" %}

## Create a New Storage Account
Azure Storage is a Microsoft-managed service providing cloud storage. In this case, you will be hosting your static site through this service.

*To create a storage account:*
1. Once again, click **Storage accounts** underneath **Azure Services** from your Azure portal.
1. Click **Create Storage Account** below the **No storage accounts to display** message.

{% include image.html file="create-storage-button.png" alt="create-storage-button" caption="Storage accounts Page" %}

   - You are directed to the **Create storage account** page.
   - By default, **Free Trial** is selected as your subscription.

### Fill out Basics tab

The **Basics** tab allows you to control the basic settings of your storage account. 

{% include note.html content="The other tabs allow you to change more advanced settings that are not required for this tutorial. As such, they will not be covered." %}

{% include important.html content=" When you go to deploy a live site later, you will need to collaborate with your developers to determine the most secure and cost efficient settings to use. It is not recommended to go live with the settings used in this tutorial." %}


*To fill out the Basics tab:*

1. Under **Resource group**, click the **Create new** link.
1. Name it `static-res`.

{% include note.html content="The naming used for the resource group and storage account is only an example. When you deloy your own static site, you will want to change the naming to conform to your company standards. View the article [Considerations for naming Azure resources](https://docs.microsoft.com/en-us/azure/azure-government/documentation-government-concept-naming-resources) for more information." %}

{:start="3"}
1. Enter a **Storage account name**, for example, `static-store` (this name may not be available).
1. Pick the **Location** from the drop-down menu that makes the most sense. If it is correct, leave it be. For example, I live in the Netherlands so the most relevant location is `(Europe) North Europe`. 
1. Ensure the **Standard** radio button is selected.
1. Ensure the Account kind is **StorageV2**.
   - This is important because static site hosting is no longer available for a **V1** account.
1. Ensure **Read-access geo-redudant..** option is selected.
   - Your screen should look similar to below (except with different storage account name and location).

{% include image.html file="create-storage-account.png" alt="create-storage-account" caption="Create storage account page" %}

<!-- Do not think I need this since I am using defaults.
### Fill out Networking tab

1. Click ****Next: Data protection** at the bottom of the page, or click the **Networking** tab at the top.
1. Select **Public endpoint (all networks)** as the **Connectivity method**.
 You want this to be private, but I do not know how to add a virtual network or what that is. Lets do this from gmail account instead. until you
ask about what needs to be done. -->

### Review and Create Storage Account
It is time to review your changes and create the storage account.

*To create the storage account:*
1. Click **Review + create** at the bottom of the page, or click the **Review + create** tab at the top.
1. Confirm you have the correct settings selected based on the previous instructions and click **Create**.
1. Click **Go to Resource** at the bottom.

{% include callout.html content="After successfully creating your storage account, you are directed to the new storage account's page where you can configure a static site." type="success" %}

## Enable Static Website
You must enable static sites from your storage account page.

*To enable a static website:*
1. Click **Static website** from the side navigation.
1. Click the **Enabled** radio button.
1. Enter `index.html` in the **Index document name** field.
1. Enter `404.html` in the **Error document path** field.
   - A **successfully updated...** message should display in the top-right corner, and a primary/secondary endpoint should also display on the page.
1. Copy the **Primary endpoint** and store it somewhere for retrieval later.

   Your screen should look similar to below:

{% include image.html file="staticsite-config.png" alt="staticsite-config" caption="Enable Static Website" %}

{% include note.html content="The Primary endpoint is the address where you can see your static site after publishing. It is recommended you save this endpoint to your browser as you will be visiting it a lot." %}

{% include callout.html content="Now that your storage account has been created and is ready to host static sites, the next step is to create build and release pipelines inside Azure DevOps that deploy your site to the blob storage container." type="success" %}

## View $web folder in Storage Explorer (optional)

You should use Azure Storage Explorer to manage your static site files.

1. Go to google and search for `Azure Storage Explorer`.
1. Download it.
1. From within the Explorer, click **Add an account**.
1. Ensure the **Add an Azure Account** radio button is selected and **Azure** is selected from the drop-down.
1. Sign in to the outlook account you created in the previous section.
1. With your storage account selected, click **Apply**.
1. Locate the folder **$web** by drilling down from **Storage Accounts** to **Blob Containers**.
   - This is the blob container created in the previous section that will house your static site files once they are published.

{% include series/next-button.html %}

<!-- Do Azure storage explorer here -->


<!-- Insert next button like Tom's blog-->


<!-- 
Read this:
https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-static-website


<!-- What you are modifying. Content is less technical. More background information like setting up azure accounts. More stepped based than explanations -->

<!-- I remember you had a problem with blob storage now that I remember, another question to have>

<!-- 
/subscriptions/<subscriptionID>/resourceGroups/<ResourceGroupName>/providers/<ResourceProvider>/<ResourceType>/<ResourceName>
-->

<!-- Include test repo to demonstrate the Azure pipeline, your template!! Or bare bones template -->