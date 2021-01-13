# Manage the static site with Azure Storage Explorer

In the previous section, you:
- Signed up for a new Azure account.
- Created a new free trial subscription.
- Created a new storage account.
- Configured the static website from within your storage account.

As a result, Azure generated a primary endpoint to access your new site and also created a new [blob container](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction#:~:text=Azure%20Blob%20storage%20is%20Microsoft's,as%20text%20or%20binary%20data.) called `$web`.

You should use Azure Storage Explorer to manage your static site files.


Go to google and search for Azure Storage Explorer.
Download it.
From within the Explorer, click **Add an account**.
Ensure the **Add an Azure Account** radio button is selected and **Azure** is selected from the drop-down.
Sign in to the outlook account you created in the previous section.
WIth your storage account selected, click **Apply**.
Locate the folder **$web** by drilling down from **Storage Accounts** to **Blob Containers**.
   - This is the blob container created in the previous section that will house your static site files once they are published.

To demonstrate how Azure Explorer works.
Create a simple text file on your Desktop called "test.txt". 
Open the file and enter the word "test".
Save the file.
In Azure Storage Explorer, click **Upload** from within the **$web** blob container.
Select **Upload Files**.

Could not get this to work....



Managing files on Azure storage
For static web site Azure creates blob container called $web. You can upload some small file there and try to download it through browser.

To manage files on Azure storage I use Microsoft Azure Storage Explorer. It’s free to download.

For me it is main tool for managing blobs and file shares on Azure. It supports blobs, file shared, queues and tables. If you need to manage static blog files or just check what was deployed then Azure Storage Explorer is tool to use.

When accessing blob storage containers through blob storage URL there are access controls in place. Also there’s no support for directory index files (index.html). Static website URL skips access rules and handles $web container as just a folder in web server. When using static website URL our index.html files are served.




{% include note.html content="When accessing blob storage containers through blob storage URL there are access controls in place. Also there’s no support for directory index files (index.html). Static website URL skips access rules and handles $web container as just a folder in web server. When using static website URL our index.html files are served." %}
