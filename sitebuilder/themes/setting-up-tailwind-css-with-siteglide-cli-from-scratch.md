# 📋 Set Up Tailwind CSS

## Before You Start <a href="#before-you-start" id="before-you-start"></a>

{% hint style="info" %}
You must already have a Site with SiteBuilder installed
{% endhint %}

### Introduction <a href="#introduction" id="introduction"></a>

Using the Command Line Interface (CLI) to build a Tailwind CSS file allows you to:

* Use the latest versions of TailwindCSS and its various 1st and 3rd party plugins.
* Get the best performance front-end as Tailwind can scan your entire codebase to carry out "tree-shaking" to only include utility classes you actually need
* Faster development performance as you can rebuild your CSS faster, and therefore build things faster

Each time you start working on a new project, you will need to follow these steps, however, the setup time is worth it as it will give you a much smoother experience going forward.

## Step 1) Check Your SiteBuilder Tailwind Settings are Set to CLI Build

Older versions of SiteBuilder would have defaulted to use the JIT option as a default. Make sure it's set to CLI!

<figure><img src="https://p186.p2.n0.cdn.zight.com/items/xQuorQvv/57b911fc-9d00-4f9f-81bc-8e70036dbf09.jpg?source=viewer&#x26;v=%22fcaa1cc100f3008ef92010120f6756c7%22" alt=""><figcaption></figcaption></figure>

## Step 2) Set up Project Folder in a Code Editor and Connect it with your Siteglide Site Using Siteglide CLI

You will need to install Siteglide CLI- if you haven't or are not sure if you have, head here first:

{% content-ref url="../../developer-tools/cli/get-started-with-cli/getting-started-with-cli.md" %}
[getting-started-with-cli.md](../../developer-tools/cli/get-started-with-cli/getting-started-with-cli.md)
{% endcontent-ref %}

Next you'll need to follow the steps to create a project folder for your new Site and setup Siteglide CLI for this new Site:

{% content-ref url="../../developer-tools/cli/get-started-with-cli/steps-to-set-up-siteglide-cli-on-a-specific-site.md" %}
[steps-to-set-up-siteglide-cli-on-a-specific-site.md](../../developer-tools/cli/get-started-with-cli/steps-to-set-up-siteglide-cli-on-a-specific-site.md)
{% endcontent-ref %}

Once you've pulled the Codebase for the new Site down into your project folder, continue to the next step.

## Step 5) Move the Tailwind Files to the Correct Folders

We'll be using npm (Node Package Manager) to install the software and settings we need to run Tailwind on your machine. This is the same tool you will have used to install the Siteglide-CLI.

We've built files in the Site Template which contain the instructions npm needs to set you up automatically.

Find the files in the folder:

```
└───marketplace_builder
    └───assets
        └───modules
            └───module_86
                └───src
                    │   readme.md
                    └───open_me_to_set_up_tailwind_1st_time
                        ├───copy_and_paste_my_files_into_the_root_project_folder
                        │   package-lock.json
                        │   package.json
                        └───copy_and_paste_my_files_into_the_src_folder
                            tailwind.config.js
                            tailwind.css
```

And **copy and paste** these two files `package.json` and `package-lock.json` into the root project folder (next to- but not inside - marketplace\_builder).

<pre><code>│   package-lock.json
│   package.json
└───marketplace_builder
    └───assets
        └───modules
            └───module_86
                └───src
                    │   readme.md
                    └───open_me_to_set_up_tailwind_1st_time
                        ├───copy_and_paste_my_files_into_the_root_project_folder
                        │   package-lock.json
<strong>                        │   package.json
</strong>                        └───copy_and_paste_my_files_into_the_src_folder
                            tailwind.config.js
                            tailwind.css
</code></pre>

Next, move the `tailwind.config.js` and `tailwind.css` files from the `copy_and_paste_my_files_into_the_src_folder` folder to the `marketplace_builder/assets/modules/module_86/src folder`:

<pre><code>│   package-lock.json
│   package.json
└───marketplace_builder
    └───assets
        └───modules
            └───module_86
                └───src
                    │   readme.md
                    │   tailwind.config.js
                    │   tailwind.css
                    └───open_me_to_set_up_tailwind_1st_time
                        ├───copy_and_paste_my_files_into_the_root_project_folder
                        │   package-lock.json
<strong>                        │   package.json
</strong>                        └───copy_and_paste_my_files_into_the_src_folder
                            tailwind.config.js
                            tailwind.css
</code></pre>

## Step 6) Use NPM to Automatically Install Dependencies

Using your integrated terminal from step 2, which is already open in your project directory, run the command:

```
npm i
```

{% hint style="info" %}
You may be given some warnings and information by npm at this stage. For the sake of this tutorial most are safe to ignore for now and come back to later.
{% endhint %}

## Step 7) Run Commands to Build your tailwind.min.css File and Sync it

Split your terminal in two. We'll need one window to build our Tailwind CSS and a second one to sync our changes to the Site:\\

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

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
