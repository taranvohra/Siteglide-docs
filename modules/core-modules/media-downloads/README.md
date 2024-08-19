# Media Downloads

## What are Media Downloads?

The Media Downloads Module allows you to upload files securely. You have control over who accesses the File, and how long links work for.

The Media Downloads Module is similar to File Manager, but is designed to handle files which need to be handled more securely. Some examples might include:

1. Files which exist behind a Secure Zone&#x20;
2. eBooks and other files you may need a Subscription to access

Upload Files Securely - It is not possible for internet users to "guess" the link to your files and download them.&#x20;

Generate secure links on the Front-End; each link will only be valid for a short amount of time after reloading the Page. This allows you to control who has access to the link, and how long they will have access for.

## How the Media Download Links Work

When you output a link on the Front End, it contains security parameters that will be different on every Page load. The purpose of these is to tie a security key with a time-limited window to access the file.  The expiry parameter will be used to denote how long the link is valid for after the page has been loaded.  For example, if a user loads the page and then clicks the link 20 minutes later, the download link will already be invalid as it will be over the 10 minute default window.  At this point the user will have to reload the page to generate a new valid link.

Despite this, you can use the link exactly like a normal URL to an asset, except that there is no need to use asset\_url because the link goes directly to the CDN.&#x20;
