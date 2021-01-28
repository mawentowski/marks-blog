---
title: Set up CDN
sidebar: azure-solutions_sidebar
permalink: setup-CDN.html
folder: azure-solutions/azure-pipelines
---
Azure Key Vault is service for storing keys, secrets and certificates securely so applications doesn’t keep these magical things on hard disc of server. When setting up CDN we need Azure Key Vault as it is the fastest way to get HTTPS work.

1. Go to the [Azure homepage](https://azure.microsoft.com).
1. In the search field at the top, type `key vaults` and select it.
1. Click **Create key vault**.

{% include image.html file="key-vaults.png" alt="key-vaults" caption="Enable Static Website" %}

{:start="4"}
1. Select the **Resource Group** you created previously (possibly `jekyll-site`)
1. Enter a **Key vault name**. I chose to make it `jekyll-site-key`.
1. Select **Region**. Ensure it is the same region as your static site. <!--warning -->

{% include image.html file="create-key-vault.png" alt="create-key-vault" caption="Create key vault page" %}

{:start="5"}
1. Leave the other fields the same and click **Review & Create**.
   - The message **Your deployment is complete should appear**.
1. Click **Go to Resource**.
1. Click **Certificates** from the side navigation.

{% include image.html file="certs.png" alt="certs" caption="Key vault resource page." %}

1. Click **Generate/Import**.
<!-- need .pfx or .pem SSL certificate.. -->


<!-- I do not think you want to do this twice, only for sita.aero. GOing to talk to Doug first to get his opinion -->