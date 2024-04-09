

## Introduction

When migrating a site from one platform to another, we recommend that the first thing you do is import your assets.

This means that when you import your WebApps and WebApp Layouts later on, the paths to the images can easily be mapped.

There are two main ways to upload assets:

- via the Siteglide CLI
- via the Admin CMS/ File Manager

## Using File Manager to Upload Assets

File Manager currently allows you to bulk upload files within your browser. This is a great alternative to CLI for day-to-day use. You can create folders and upload assets within each as you go.

However, there could be browser limitations over how much can be uploaded at once (e.g. large file sizes), so we still recommend you use Siteglide CLI for bulk upload and for migrations.

## Uploading Your Assets Using Siteglide CLI

If you have a very large number of assets to upload (especially large images or videos), the best way to upload is via the Siteglide CLI.

In order to do this: you'll need to follow these steps. Where a step has a placeholder like <env>, add in your own environment, for example production:

1) First follow this tutorial to set up siteglide-cli, including adding an environment.

2) Create a new folder for your project if you've not already got one.

3) Change directory to that folder with the terminal command cd path/to/folder

4) Run the terminal command siteglide-cli pull <env> . When prompted to, type a capital "Y" to confirm.

![Pulling the Site File Structure](./.gitbook/assets/getgist/migrating-assets/fb8f4bc670c2a38c6fbbc9f18fce95d5afacd761fe8e9aa13d80259904725251image-4-1_1ydo3ql.png)

You will now have the Site stored in your new Project folder. On the root, level, you'll see a root folder called marketplace_builder.

![New marketplace_builder Folder](.gitbook/assets/getgist/migrating-assets/294d5510d2698532c2442e711cc0c01a811b1e75344835fbaf33d5835e4f2feaimage-11-1_vu91uc.png)

5) In your new Project folder, make sure the counterpart versions of these folders exist inside marketplace_builder/assets/ - by default after a pull, only a css and js folder will be shown. If needed, create any other folders here

![Assets Folder](.gitbook/assets/getgist/migrating-assets/9f1edf23b16194fb51d435ab39ad58522ff1d46dcd2d4e7bbfb1b9aef0026641image-6-1_x6mr68.png)

6) Run the terminal command siteglide-cli deploy <env> -w . This deploys your marketplace_builder folder, including the assets, to your website.

7) Check your assets have arrived successfully on Admin by navigating to CMS/File Manager and checking each of the four tabs.

![Check your new assets are visible in File Manager](.gitbook/assets/getgist/migrating-assets/9662cee3e64d1c5c9f6c8cd0f21217679a1fb196ebef396a78a2e008d173b420image-10-1_x7nc4i.png)

## Outputting your Assets

Assets are stored and accessed a bit differently on our platform. We do this to receive various benefits, check out our doc on [Assets]() to find out more.