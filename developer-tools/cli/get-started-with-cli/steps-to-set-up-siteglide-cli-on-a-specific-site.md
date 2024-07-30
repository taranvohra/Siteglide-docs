---
description: Connect to a site via CLI
---

# 📋 Site Setup

{% hint style="warning" %}
You need CLI installed first, check out our Quickstart guide:
{% endhint %}

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

Once you've installed the CLI you should be ready to learn how to set up a new project folder and connect it to a specific Siteglide Site. You'll need to follow these steps every time you want to use the CLI to work on a new site, so over time these will become very familiar.

## Step 1) Create a Project Folder on Your Machine

Your project folder will contain all of your Site's files.

Use Finder on Mac, or Windows Explorer to create this new empty folder, and give it a similar name to your site so you can find it again.\
\
We recommend creating this folder inside a sensible organisation structure, for example you may have a single folder which contains all of your project folders, or you might organise by customer.

## Step 2) Open Your Project Folder in a Text Editor

In order for a CLI tool's ability to deploy and pull code from a Site to be useful, we need to have a good place to look at and change that code.

While you are free to use any kind of terminal or any kind of Text Editor, we'll use VSCode for these steps- one major benefit is that its integrated terminal allows you to easily manage your project in one place. It also comes with lots of useful extensions.

If you do not already have a text editor installed, you can browse for one or install VSCode here: [https://code.visualstudio.com/download](https://code.visualstudio.com/download)

You can then open your project folder in the Text Editor:

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Step 3) Open the Integrated Terminal

{% hint style="info" %}
If your IDE or Text Editor does not have an integrated terminal, you can open any terminal and change directory to your project folder.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

The terminal will appear in its own panel, by default below the code. In VSCode this will automatically change directory to your project folder (if not, do this manually)!

<figure><img src="../../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
If you need to run multiple commands at once, you will need two terminals. In VSCode you can "split" the terminal window if you want to run multiple commands at once and keep an eye on all of them.
{% endhint %}

## Step 4) Make Sure Your Email Address is Listed in the Site Users

Open up the Siteglide Portal and find your Site in the Sites option in the left-hand-side menu.

In the Users tab, make sure your user's email address is listed. If not, invite yourself (as an existing user) to the Site.

<figure><img src="../../../.gitbook/assets/image (3) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Step 5) Copy the Env Command with Pre-Filled Variables

In the Details tab, near the bottom of the Site information, find the CLI Command and copy it.

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Step 6) Run the Env Command to Set Up a Connection Between your Project Folder and a Site

Paste the command into your integrated terminal.

When prompted, enter the Siteglide Password associated with the email address in the command.

{% hint style="info" %}
This won't work unless you follow step 5 first!\
\
If you forget your password, you can reset your password on the Siteglide Portal first.
{% endhint %}

This command creates what we call an envrionment. Think of it as a connection between a project and a Site. Sometimes you may maintain a staging Site and a live Site for the same project and you might create both a staging and a production environment.

You will need to remember the name of your environment in order to use any other Siteglide-CLI commands, but if you forget, there will be a .siteglide-config file in the root of your project folder which will list them:

<figure><img src="../../../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Step 7) Run an Initial Pull of the Site to Pull Down the Existing Code Base

You're now set up with Siteglide-CLI for this Site!\
\
The obvious first move would be to pull the existing Site's files down to the Site, using the following command in the terminal:

```
siteglide-cli pull staging
```

This will create your directory structure and populate it with your site's files and assets (images will not be pulled due to their size - see export command).

{% hint style="info" %}
If you use Github for backing up your code, debugging and undoing mistakes, it's a good idea to initiate it and make your initial commit now.
{% endhint %}

## Next

You now know how to set up Siteglide CLI on a Site! You can follow these steps every time you want to work on a new Site.

Next, check the [siteglide-cli-reference.md](../cli-reference/siteglide-cli-reference.md "mention") for how to:

* Deploy all your code to the site
* Sync individual files to the site as you save them
* And remember how to pull all the code down to your project folder
