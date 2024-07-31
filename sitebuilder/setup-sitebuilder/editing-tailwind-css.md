# 📋 Editing Tailwind CSS

## Before you Start

You will need to have already created a site with both Sitebuilder installed and a Flowbite/Tailwind Page template setup:

{% content-ref url="create-site-from-flowbite-template.md" %}
[create-site-from-flowbite-template.md](create-site-from-flowbite-template.md)
{% endcontent-ref %}

{% content-ref url="set-up-tailwind-css.md" %}
[set-up-tailwind-css.md](set-up-tailwind-css.md)
{% endcontent-ref %}

{% hint style="info" %}
It is possible to follow the [https://tailwindcss.com/docs/installation](https://tailwindcss.com/docs/installation) docs to set up the Tailwind CLI your own way. However, this article above sets up the folder structure in a way which is compatible with a Siteglide Site's folder structure and this article assumes your folder structure is set up the same way.
{% endhint %}

## Introduction

Having set up your local Project Folder with:

* A Text Editor for viewing your Folder Structure inside a Project Folder
* A Siteglide-CLI environment which connects your Project Folder to a Site
* An npm script which runs a Tailwind compilation process

This article will delve a little deeper into the files you can modify to take full control of your Tailwind build!

## Useful Tools for this Topic

* We recommend if you are using VSCode that you download and enable this extension, which will help VSCode understand Tailwind's syntax and give you tips on things like colours: [bradlc.vscode-tailwindcss](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)
* Also if you are using VS Code, this extension is useful for creating shortcuts to your favourite project folders: [https://marketplace.visualstudio.com/items?itemName=alefragnani.project-manager](https://marketplace.visualstudio.com/items?itemName=alefragnani.project-manager)
* This tool is really helpful for fetching colours with all the shades you need generated for you: [https://uicolors.app/create](https://uicolors.app/create)

## A Recommended Day-to-Day Workflow

(For Editing a Siteglide Site Which Uses a Tailwind Theme.)

1. Open up the Project Folder for your Site
2. In case your team have made any changes while you've been away, run `siteglide-cli pull <env>`
3. Split your terminal and simultaneously run:
   1. `siteglide-cli sync <env>` to push any code changes to the site
   2. `npm run tailwind` to watch for code changes and re-compile your Tailwind build (see [#the-tailwind.min.css-file](editing-tailwind-css.md#the-tailwind.min.css-file "mention"))
4. Make the necessary changes to your code.

## What does each Tailwind related File Actually Do?

### :deciduous\_tree: Folder Structure

```
└───marketplace_builder
    └───assets
        |   └───css
        |       tailwind.min.css
        └───modules
            └───module_86
                └───src
                        readme.md
                        tailwind.config.js
                        tailwind.css
```

### Source Files

`src` is short for source. These files are not designed to be seen by the browser. Instead think of them as the _recipe_ for a final Tailwind CSS file.

When you sync these files, they are still pushed to your Site because they are inside the marketplace\_builder folder. This allows you to share changes with other users on the Site (or yourself on different machines).

#### The `tailwind.config.js` File

This file is a configuration file and a Tailwind CSS feature which can be used to:

* Create and modify Tailwind Variables e.g. Colour, Spacing
* Include Plugins, for example we by default include the Flowbite plugin

You can learn all about Tailwind CSS configuration files here: [https://tailwindcss.com/docs/configuration](https://tailwindcss.com/docs/configuration)

You can find an example of default config variables here: [https://github.com/tailwindlabs/tailwindcss/blob/master/stubs/config.full.js](https://github.com/tailwindlabs/tailwindcss/blob/master/stubs/config.full.js) If you leave any variables blank, default values from this file will be used.

#### The `tailwind.css` File

This file can be used to write ordinary CSS, or you can use Tailwind's documented features. The file should not be linked to on a website, instead it will be compiled into a new production-ready CSS file when you save it and run the `npm run tailwind` build process.

Often with Tailwind CSS, you will find you will not need to enter this file often, as you can achieve most of the styling you want by using existing:

* Utility Classes
* Arbitrary Values in Utility Classes
* Prefixes instead of Media Queries

However, if you do want to write your own CSS, you will not find yourself limited!

See here to understand how to insert your CSS into one of Tailwind's layers: [https://tailwindcss.com/docs/adding-custom-styles#using-css-and-layer](https://tailwindcss.com/docs/adding-custom-styles#using-css-and-layer)

See here to understand how to add custom classes which combine existing Tailwind utility classes: [https://tailwindcss.com/docs/functions-and-directives#apply](https://tailwindcss.com/docs/functions-and-directives#apply)

### The `tailwind.min.css` Final CSS File

{% hint style="info" %}
See the folder structure above to find this file. You should not need to create it or edit it manually. The npm run tailwind command will compile it automatically from the src files.\
\
It should be linked in your Page Template, but by default a SiteBuilder Page Template will do this via a `tailwind/head` Liquid include. You could optionally replace this with a \<link> tag instead.
{% endhint %}

When you make changes to any of the following while `npm run tailwind` is running in your terminal:

* Your HTML (adding or removing new Tailwind classes)
* Your JavaScript (adding or removing new Tailwind classes) (in case classes will be added via JavaScript, e.g. when a Flowbite Component changes state.
* Your `tailwind.config.js` file
* Your `tailwind.css` file

A new version of the `tailwind.min.css` file will be generated. Use the Siteglide CLI to sync or deploy this to your Site to see your changes applied: [reference.md](../../developer-tools/cli/reference.md "mention")\
\
Tailwind uses tree-shaking so that any classes which aren't used by the files referenced above will be removed from the final CSS file to make it as fast as possible. It will also be minified.
