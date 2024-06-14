# 📋 Steps to Set Up Tailwind CSS with Siteglide CLI on a Site with SiteBuilder Installed

## Before You Start <a href="#before-you-start" id="before-you-start"></a>

{% hint style="info" %}
This Article is very similar to [setting-up-tailwind-css-with-siteglide-cli-from-a-flowbite-site-template.md](setting-up-tailwind-css-with-siteglide-cli-from-a-flowbite-site-template.md "mention") but in this article, it doesn't matter how or when you created your Site. If you install the SiteBuilder Module with any version since 4.11.2, these steps will work.
{% endhint %}

* Check [Choosing a Build Method](https://www.sitegurus.io/documentation/sitebuilder/libraries\_and\_frameworks/libraries\_using\_tailwind\_css\_choosing\_a\_build\_method) first to choose which option suits you best.
* This Article assumes you have already created and chsoen a Siteglide Site to work on

### Introduction <a href="#introduction" id="introduction"></a>

Using the Command Line Interface (CLI) to build a Tailwind CSS file allows you to:

* Use the latest versions of TailwindCSS and its various 1st and 3rd party plugins.
* Get the best performance front-end as Tailwind can scan your entire codebase to carry out "tree-shaking" to only include utility classes you actually need
* Faster development performance as you can rebuild your CSS faster, and therefore build things faster

Each time you start working on a new project, you will need to follow these steps, however, the setup time is worth it as it will give you a much smoother experience going forward.

### Step 1) Install the SiteBuilder Module <a href="#quick-start" id="quick-start"></a>

Check if you have already installed the SiteBuilder Module on your site. The version should be at least 4.11.2

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

The SiteBuilder Module comes with the Free Flowbite Theme automatically.&#x20;

If the download appears to have crashed, try refreshing the page and trying again - it is a large package of files.

## Step 2) Install a Flowbite Site Template

{% hint style="info" %}
If you have already created a Flowbite Page Template using SiteBuilder, you can skip this step.
{% endhint %}

In the Siteglide Admin, under modules in the menu, enter the SiteBuilder Module.\
\
Find Page Templates in the tabs:

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

In the popup, choose:

* A name e.g. "Main"
* Default Page Template - optional
* the Flowbite Theme (other SiteBuilder Themes will be available to download from Marketplace)
* Optionally, add a Menu, but this is not neccesary for this tutorial

This template starts with a default Tailwind CSS file which allows most layouts to work out of the box, but if you want to start changing things, you'll need to follow the rest of these setup steps!

## Step 3) Check Your SiteBuilder Tailwind Settings are Set to CLI Build

Older versions of SiteBuilder would have defaulted to use the JIT option as a default. Make sure it's set to CLI!

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

## Step 4) Set up Project Folder in a Code Editor and Connect it with your Siteglide Site Using Siteglide CLI

You will need to install Siteglide CLI- if you haven't or are not sure if you have, head here first:

{% content-ref url="../../siteglide-cli/getting-started-with-cli.md" %}
[getting-started-with-cli.md](../../siteglide-cli/getting-started-with-cli.md)
{% endcontent-ref %}

Next you'll need to follow the steps to create a project folder for your new Site and setup Siteglide CLI for this new Site:

{% content-ref url="../../siteglide-cli/steps-to-set-up-siteglide-cli-on-a-specific-site.md" %}
[steps-to-set-up-siteglide-cli-on-a-specific-site.md](../../siteglide-cli/steps-to-set-up-siteglide-cli-on-a-specific-site.md)
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

### Step 6) Use NPM to Automatically Install Dependencies

Using your integrated terminal from step 2, which is already open in your project directory, run the command:

```
npm i
```

{% hint style="info" %}
You may be given some warnings and information by npm at this stage. For the sake of this tutorial most are safe to ignore for now and come back to later.
{% endhint %}

### Step 7) Run Commands to Build your tailwind.min.css File and Sync it

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

#### Changing the Page Template's default path to your compiled CSS <a href="#changing-the-page-templates-default-path-to-your-compiled-css" id="changing-the-page-templates-default-path-to-your-compiled-css"></a>

If you've edited your Tailwind CLI settings to create the min.css file in a different location, you can edit a Page Template generated through SiteBuilder so that it correctly links to the new file path. Add a new parameter `optional_path_to_cli_css` to the Tailwind Head file.

```liquid
{% raw %}
{% include 'modules/module_86/tailwind/head', optional_path_to_cli_css: 'css/tailwind2.min.css' %}
{% endraw %}
```

Copy

### An Example Workflow using Siteglide CLI and Tailwind CLI <a href="#an-example-workflow-using-siteglide-cli-and-tailwind-cli" id="an-example-workflow-using-siteglide-cli-and-tailwind-cli"></a>

Each time you start work:

1. Pull the latest files from the site using `siteglide-cli pull`. It's important to have the latest files, because Tailwind only adds classes that you're actually using, but it can only see which files you're using if the files are available locally.
2. Use `siteglide-cli sync` to watch your `marketplace_builder` folder.
3. In terminal, run the command: `npm run tailwind` to watch for Tailwind changes.
4. Now you can begin work! Every time you make a change and save, your updated file will sync to Siteglide and so will a brand new version of the Tailwind CSS.

### Adding Custom CSS <a href="#adding-custom-css" id="adding-custom-css"></a>

You can use the src file `tailwind_src/tailwind.css` to write any custom CSS for your Tailwind build. Check the [Tailwind CSS documentation on Functions & Directives](https://tailwindcss.com/docs/functions-and-directives) for details.

### Troubleshooting <a href="#troubleshooting" id="troubleshooting"></a>

#### NodeJS and NPM Versions <a href="#nodejs-and-npm-versions" id="nodejs-and-npm-versions"></a>

If you see an error relating to the version of NPM, you may want to check which version of NodeJS and NPM you have installed on your machine:

```bash
node -v
```

Copy

```bash
npm -v
```

Copy

Follow the instructions here to update depending on your operating system: [Installing NPM](https://docs.npmjs.com/cli/v8/configuring-npm/install).

#### Version Control and Conflicts on Siteglide <a href="#version-control-and-conflicts-on-siteglide" id="version-control-and-conflicts-on-siteglide"></a>

If you work with other developers (or on multiple devices) on the same Siteglide project, it is definately recommended to use a version-control (otherwise known as source-control) tool like GitHub to share your package.json file etc. with the other developer.

The risk of conflicts is somewhat mitigated if you follow our reccomendation in the Quick Start guide of storing the `tailwind.config.js` file in a custom location (inside `marketplace_builder/views/partials`). This means it will be accessible via Siteglide CLI pull and editable via sync, but not from the Siteglide Admin.

If you are using version-control, the node\_modules folder can become very large and we recommend adding this to your `.gitignore` file or equivalent.

#### I've got a `syntax error` when I run the `npm run tailwind` command <a href="#ive-got-a-syntax-error-when-i-run-the-npm-run-tailwind-command" id="ive-got-a-syntax-error-when-i-run-the-npm-run-tailwind-command"></a>

There might be an issue with your Tailwind Config File. Try temporarily reverting the file to the state it is in here and see if that fixes the problem. If not [contact Sitegurus](https://sitegurus.io/).

#### I've got a different problem <a href="#ive-got-a-different-problem" id="ive-got-a-different-problem"></a>

Please [contact Sitegurus](https://sitegurus.io/).

### Removing JIT Code from the Template <a href="#removing-jit-code-from-the-template" id="removing-jit-code-from-the-template"></a>

If you are certain that you won't be using the [Tailwind's JIT Compiler Via CDN](https://www.sitegurus.io/documentation/sitebuilder/libraries\_and\_frameworks/tailwinds\_jit\_compiler\_via\_cdn) in the future, you can optionally remove the `<script type="module">` and `<script type="tailwind-config">` tags containing the JIT version of the Tailwind Config file from the Page Template. This may help avoid clutter and confusion.

### Alternative Configurations <a href="#alternative-configurations" id="alternative-configurations"></a>

#### I already have a package JSON file. <a href="#i-already-have-a-package-json-file" id="i-already-have-a-package-json-file"></a>

In that case, use npm to add dev-dependencies to the existing file rather than copying across our file:

```bash
npm i -D tailwindcss@3.1.5
```

Copy

```bash
npm i -D flowbite@1.4.7
```

Copy

```bash
npm i -D flowbite-typography@1.0.2
```

Copy

[Adding Dependencies to a package.json file](https://docs.npmjs.com/specifying-dependencies-and-devdependencies-in-a-package-json-file#adding-dependencies-to-a-packagejson-file).

#### I use an alternative package manager, instead of NPM. <a href="#i-use-an-alternative-package-manager-instead-of-npm" id="i-use-an-alternative-package-manager-instead-of-npm"></a>

This is fine! We don't cover this in our example, but there is plenty of documentation out there. You can use the information in the answer above to see which dependencies we use.

#### Editing this configuration <a href="#editing-this-configuration" id="editing-this-configuration"></a>

This repository is a "quick-start" guide, not fixed instructions for how to use Tailwind with Siteglide. Feel free to read the relevant documentation from [Tailwind](https://tailwindcss.com/docs/installation), [NPM](https://docs.npmjs.com/specifying-dependencies-and-devdependencies-in-a-package-json-file), [Flowbite](https://flowbite.com/docs/getting-started/quickstart/) and configure Tailwind however you wish.

#### I prefer to work in the Siteglide Admin <a href="#i-prefer-to-work-in-the-siteglide-admin" id="i-prefer-to-work-in-the-siteglide-admin"></a>

Have you tried our [JIT Compiler](https://www.sitegurus.io/documentation/sitebuilder/libraries\_and\_frameworks/tailwinds\_jit\_compiler\_via\_cdn)? Based on the fantastic JIT Compiler from the folks at Beyond Code, we've added caching to allow better production speeds and integrated it with a Siteglide Template. This allows a developer to use Tailwind entirely from the Siteglide Admin without using any CLI tools.
