# 💻 Setting Up Tailwind CSS with Siteglide CLI - from scratch

## Using the Tailwind CLI with Siteglide <a href="#using-the-tailwind-cli-with-siteglide" id="using-the-tailwind-cli-with-siteglide"></a>

### Before You Start <a href="#before-you-start" id="before-you-start"></a>

* Check [Choosing a Build Method](https://www.sitegurus.io/documentation/sitebuilder/libraries\_and\_frameworks/libraries\_using\_tailwind\_css\_choosing\_a\_build\_method) first to choose which option suits you best.
* Make sure you have already installed the Siteglide-CLI and are familiar with its use. This should give you the tools and the understanding you need to follow this guide. [Introducing Siteglide CLI](https://developers.siteglide.com/introducing-siteglide-cli).

### Introduction <a href="#introduction" id="introduction"></a>

Using the Command Line Interface (CLI) to build a Tailwind CSS file allows you to use the latest versions of TailwindCSS and its various 1st and 3rd party plugins.

If you prefer using the Siteglide CLI to build sites already, the two CLIs work very well together.

This guide is both a quick-start guide to get you started and a set of tips for how to build Tailwind CLI into your Siteglide workflow.

### Quick Start <a href="#quick-start" id="quick-start"></a>

1.  SiteBuilder Tailwind Settings

    Navigate to the Settings tab in the SiteBuilder admin. (If this doesn't appear yet, you need to create a Page Template using a Tailwind Theme first.)

    ![How to Switch to CLI Mode](https://res.cloudinary.com/sitegurus/image/upload/v1658411912/modules/module\_86/documentation/Tailwind/select\_just\_in\_time.jpg)

    Then select "CLI".
2.  Create Directory Structure

    Open up a command-line terminal on your machine and change directory (`cd`) to your project folder. Use `siteglide-cli pull <env>` or `siteglide-cli init` to create your directory structure, if you haven't already.
3.  Copy Files

    Copy the files you need into your project folder, using whichever method you prefer.

    * Copy package.json and package-lock.json from the [example repository](https://github.com/SiteGurus/Siteglide-Tailwind-Template) root to your own. (See troubleshooting if your project already has a package.json file.)
    * Copy the tailwind.config.js and tailwind.css files from the [example repository](https://github.com/SiteGurus/Siteglide-Tailwind-Template/blob/main/marketplace\_builder/views/partials/tailwind/tailwind.config.js) in this folder:

    ```bash
    ├───marketplace_builder
    │   └───assets
    │       └───modules
    │           └───module_86
    │               └───src
    │                   tailwind.config.js
    │                   tailwind.css
    ```

    Copy

    to an identical folder structure inside your own project. Using this custom location will allow it to be pushed and pulled to the site.

    (If you prefer, you can create a new repository using the template in Github and then pull your site into the new folder!)
4.  Install NPM Dependencies

    In terminal, change directory to the root of your project folder

    ```bash
    cd <my_folder_path>
    ```

    Copy

    and use the command

    ```bash
    npm i
    ```

    Copy

    This will install the required dependencies needed to run the Tailwind CLI with our default setup.
5. Run the command `siteglide-cli sync <env>` to watch your `marketplace_builder` folder for changes and push these to the site.
6. Run the command: `npm run tailwind` to generate the CSS file for the first time. Since you started syncing in step 4, this will immediately be pushed to the site.
7.  Set up your Page Template

    You can either create a new template using SiteBuilder (option a) or edit an existing one (option b).

    a. After you have synced your new `css/tailwind.min.css` file to the site, the SiteBuilder module will by default add this CSS file to any [new templates](https://www.sitegurus.io/documentation/sitebuilder/themes/themes#creating-a-template) created through the Module.

    b. Edit your Page Template in Siteglide to change the default to your newly generated minified CSS file. If you've followed our example, this will be: `<link rel="stylesheet" href="css/tailwind.min.css file">`.

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
