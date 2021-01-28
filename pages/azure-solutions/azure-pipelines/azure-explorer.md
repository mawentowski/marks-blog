---
title: Azure Explorer
sidebar: azure-solutions_sidebar
permalink: azure-explorer.html
folder: azure-solutions/azure-pipelines
---
# Manage the static site with Azure Storage Explorer

You should use Azure Storage Explorer to manage your static site files.

Go to google and search for Azure Storage Explorer.
Download it.
From within the Explorer, click **Add an account**.
Ensure the **Add an Azure Account** radio button is selected and **Azure** is selected from the drop-down.
Sign in to the outlook account you created in the previous section.
With your storage account selected, click **Apply**.
Locate the folder **$web** by drilling down from **Storage Accounts** to **Blob Containers**.
   - This is the blob container created in the previous section that will house your static site files once they are published.

To demonstrate how Azure Explorer works.
1. Click the 3 dots next to `site` folder and select **Download Artifacts**. 
1. Save the folder to anywhere on your computer.
1. Unzip the folder (any method).
1. Copy the unzipped folder.
1. Open **Azure Storage Explorer** and open the `$web` folder.
1. Click the **Upload** button.
   - A **Upload folder** popup displays.
1. Click `No folder selected`.
1. Navigate to, and select the `site` folder you downloaded previously.
1. Leave the other fields as is and click **Upload**.

<!--Could not get this to work.... >

Managing files on Azure storage
For static web site Azure creates blob container called $web. You can upload some small file there and try to download it through browser.

To manage files on Azure storage I use Microsoft Azure Storage Explorer. It’s free to download.

For me it is main tool for managing blobs and file shares on Azure. It supports blobs, file shared, queues and tables. If you need to manage static blog files or just check what was deployed then Azure Storage Explorer is tool to use.

When accessing blob storage containers through blob storage URL there are access controls in place. Also there’s no support for directory index files (index.html). Static website URL skips access rules and handles $web container as just a folder in web server. When using static website URL our index.html files are served.




{% include note.html content="When accessing blob storage containers through blob storage URL there are access controls in place. Also there’s no support for directory index files (index.html). Static website URL skips access rules and handles $web container as just a folder in web server. When using static website URL our index.html files are served." %}
