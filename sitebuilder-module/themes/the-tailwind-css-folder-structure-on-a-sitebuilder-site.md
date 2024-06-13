# 🔹 The Tailwind CSS Folder Structure on a SiteBuilder Site

## Pre-Requisites

We recommend you start here to build a Site Template and set up a local Project Folder with Siteglide CLI and Tailwind, before starting this article:

{% content-ref url="setting-up-tailwind-css-with-siteglide-cli-from-a-flowbite-site-template.md" %}
[setting-up-tailwind-css-with-siteglide-cli-from-a-flowbite-site-template.md](setting-up-tailwind-css-with-siteglide-cli-from-a-flowbite-site-template.md)
{% endcontent-ref %}

{% hint style="info" %}
It is possible to follow the [https://tailwindcss.com/docs/installation](https://tailwindcss.com/docs/installation) docs to set up the Tailwind CLI your own way. However, this article above sets up the folder structure in a way which is compatible with a Siteglide Site's folder structure and this article assumes your folder structure is set up the same way.
{% endhint %}

## Introduction

Having set up your local Project Folder with:

* A Text Editor for viewing your Folder Structure inside a Project Folder
* A Siteglide-CLI environment which connects your Project Folder to a Site
* An npm script which runs a Tailwind compilation process&#x20;

This article will delve a little deeper into the files you can modify to take full control of your Tailwind build!

## The SRC Folder

The `src` folder can be found at the directory:

```
└───marketplace_builder
    └───assets
        └───modules
            └───module_86
                └───src
                        readme.md
                        tailwind.config.js
                        tailwind.css
```

`src` is short for source. These files are not designed to be seen by the browser. Instead think of them as the _recipe_ for a final Tailwind CSS file.&#x20;

### The tailwind.config.js File

This file is a configuration file which can be used to:

* Create and modify Tailwind Variables e.g. Colour, Spacing
* Include Plugins, for example we by default include the Flowbite plugin

You can find an example of default config variables here:

\
If you leave a variable blank, it will use the default.&#x20;

\
\
