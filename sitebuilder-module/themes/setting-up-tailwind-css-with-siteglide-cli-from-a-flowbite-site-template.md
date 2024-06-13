# 💻 Setting Up Tailwind CSS with Siteglide CLI - from a Flowbite Site Template

{% hint style="info" %}
This Article is very similar to [setting-up-tailwind-css-with-siteglide-cli-from-scratch.md](setting-up-tailwind-css-with-siteglide-cli-from-scratch.md "mention") but by using a Flowbite Site Template as a starting point, we are able to skip several steps, making this article a better place to start for beginners.
{% endhint %}

## Using the Tailwind CLI with Siteglide <a href="#using-the-tailwind-cli-with-siteglide" id="using-the-tailwind-cli-with-siteglide"></a>

### Before You Start <a href="#before-you-start" id="before-you-start"></a>

* Check [Choosing a Build Method](tailwind-css-themes-choosing-a-build-method.md) first to choose which option suits you best.
* Make sure you have already installed the Siteglide-CLI and are familiar with its use. [getting-started-with-cli.md](../../siteglide-cli/getting-started-with-cli.md "mention")

### Introduction <a href="#introduction" id="introduction"></a>

Using the Command Line Interface (CLI) to build a Tailwind CSS file allows you to:

* Use the latest versions of TailwindCSS and its various 1st and 3rd party plugins.
* Get the best performance front-end as Tailwind can scan your entire codebase to carry out "tree-shaking" to only include utility classes you actually need
* Faster development performance as you can rebuild your CSS faster, and therefore build things faster

If you prefer using the Siteglide CLI to build sites already, the two CLIs work very well together.

This guide is both a quick-start guide to get you started and a set of tips for how to build Tailwind CLI into your Siteglide workflow.

## Step 1) Create a Site from the eCommerce Site Template <a href="#quick-start" id="quick-start"></a>

{% hint style="info" %}
You can use an existing Site you created from a Site Template previously, but it may not contain all of the files you need if it is older. If you get stuck, try a new Site Template creation and copy across the files you are missing.
{% endhint %}

In the Siteglide Portal, choose Marketplace in the menu and filter by the Category "Template":

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

For this step-by-step article, we'll use the Flowbite eCommerce Site Template, but in future you will be able to use any Template which uses Tailwind CSS in its [SiteBuilder Theme](./).

Click the card to open up the modal:

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Fill out the settings and click the button to start the Site Create Process.

This will take a while and you'll get an email when it finishes. You should have time to make a cup of tea and return in a few minutes to move on to Step 2.

## Step 2) Set up Siteglide CLI for your new Site

You will need to install Siteglide CLI- if you haven't or are not sure if you have, head here first:

{% content-ref url="../../siteglide-cli/getting-started-with-cli.md" %}
[getting-started-with-cli.md](../../siteglide-cli/getting-started-with-cli.md)
{% endcontent-ref %}

Next you'll need to follow the steps to create a project folder for your new Site and setup Siteglide CLI for this new Site:

{% content-ref url="../../siteglide-cli/steps-to-set-up-siteglide-cli-on-a-specific-site.md" %}
[steps-to-set-up-siteglide-cli-on-a-specific-site.md](../../siteglide-cli/steps-to-set-up-siteglide-cli-on-a-specific-site.md)
{% endcontent-ref %}

Once you've pulled the Codebase for the new Site down into your project folder, continue to the next step.

## Step 3) Move the package.json Files to the Project Folder Root

We'll be using npm (Node Package Manager) to install the software and settings we need to run Tailwind on your machine. This is the same tool you will have used to install the Siteglide-CLI.

We've built files in the Site Template which contain the instructions npm needs to set you up automatically.

Find the files in the folder:

```
└───marketplace_builder
    └───assets
        └───modules
            └───module_86
                └───src
                        package-lock.json
                        package.json
                        readme.md
                        tailwind.config.js
                        tailwind.css
```

And **copy and paste** these two files out of the folder and into the root project folder (next to- but not inside - marketplace\_builder).

```
│   package-lock.json
│   package.json
│
└───marketplace_builder
    └───assets
        └───modules
            └───module_86
                └───src
                        readme.md
                        tailwind.config.js
                        tailwind.css
```

{% hint style="info" %}
We've removed the files from the old folder for clarity, but you can leave a copy there too if you like. This means another collaborator on the Site can set up their Tailwind the same way!
{% endhint %}

### Step 4) Use NPM to Automatically Install Dependencies

Using your integrated terminal from step 2, which is already open in your project directory, run the command:

```
npm i
```

{% hint style="info" %}
You may be given some warnings and information by npm at this stage. For the sake of this tutorial most are safe to ignore for now and come back to later.
{% endhint %}

### Step 5) Run Commands to Build your tailwind.min.css File and Sync it

Split your terminal in two. We'll need one window to build our Tailwind CSS and a second one to sync our changes to the Site:\\

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Use this command to build your Tailwind's CSS (we'll look at this in more detail in a minute):

```
npm run tailwind
```

In the other terminal window, use this command to sync changes to the Site with Siteglide-CLI (replace \<env> with your environment name from step 2):

```
siteglide-cli sync <env>
```

Both commands will keep running indefinately and will watch your files for changes. Every time you change a Liquid file the Tailwind will re-compile the CSS if it needs to!

You can now start building your Site using Tailwind CSS!

## Next

Head to the next article to understand in more depth:

* The Tailwind Config File
* The Tailwind source CSS file
* The Tailwind distributable CSS file

{% content-ref url="the-tailwind-css-folder-structure-on-a-sitebuilder-site.md" %}
[the-tailwind-css-folder-structure-on-a-sitebuilder-site.md](the-tailwind-css-folder-structure-on-a-sitebuilder-site.md)
{% endcontent-ref %}
