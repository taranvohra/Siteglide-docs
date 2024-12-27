# ℹ️ Theme Module Example

In this example we're going walk through, step by step, how to create a Website Theme Module that could either be used as a private module for your agency or shared publicly in the marketplace to deliver turnkey site solutions to your clients and more.

![](../../assets/Rq5gKKmUJUrFAEhkGbzjA\_module-siteglide-theme-demo-1.png)

It is recommended that you download our example [Theme Demo Module Repository from GitHub](https://github.com/Siteglide/Module\_Siteglide\_ThemeDemo) so that you have all of the code and asset files available at each step of this guide and can easily follow along to and have your module end up looking exactly the same.

## Create Your Module

The first step to building your module is to create a listing for it in Siteglide. Within your Portal from the left-hand menu, select "Custom Modules" and then click the blue "+ Add New Module" button in the top right-hand corner.

You only need to fill in basic information into the core fields. Checkout the [Create your Module in Siteglide](/developer-tools/building-for-marketplace/site-template-modules-and-how-to-make-your-own#how-to-convert-a-trial-site-to-a-template.md) doc for more information.

Remember to note down your newly generated Vanity ID.

## Create Your Folder Structure

First, create a fresh staging site for your module. Checkout [Create Your Staging Site](/developer-tools/building-for-marketplace/create-folder-structure#create-your-staging-site) **:** for more information on this step.

Second, create a folder for your project on your local machine. Working within your new project folder, connect to your new staging site via CLI to pull the initial site files down onto your computer.

Next, create a top level folder called `modules/<module_name>/public` within your project folder. Because we are creating a basic theme Module, we don’t need to create the private top level folder. Checkout [Top Level Folders](/developer-tools/building-for-marketplace/create-folder-structure#top-level-folders.md) for more info.

![](../../assets/OSlgyzgpAqML1M1TXp\_T0\_create-top-level-folder-1.png)

### Assets

Within the public folder, we want to add in the core assets our Theme Module will use. There are three folders we want to copy in to our own Module project folder:

* `bootstrap5-plain-assets` - Core Bootstrap 5 image assets which our Theme pages will display.
* `js` - Core Bootstrap 5 JS files along with a custom JS file which our Theme pages will run using.
* `scss` - Core Bootstrap 5 CSS files along with a custom CSS file which will Style our Theme pages.

![](../../assets/y6nt6TQcgn2mRkIQRkLvx\_theme-module-assets-1.png)

Open the `Module_Siteglide_ThemeDemo` project folder you downloaded earlier and navigate into `modules/<module_name>/public/assets`. From here, drag and drop all three `bootstrap5-plain-assets`, `js` & `scss` folders into your own Module project assets folder.

### Views

Next we’re going to add in various core elements such as Pages, a Page Template, Header & Footer.

First, within your `modules/<module_name>/public` folder, create a new folder called `views`. Inside the views folder, we’ll be creating several new folder structures to house the various files we’d like to include. Below I’ll list each of these directories and give an explanation as to what they will be used for:

* `layouts/templates` - A Page Template file used to wrap all of our theme pages.
* `pages` - Several Pages we would like to include in our module and display on the site.
* `partials/includes/header` - Page Header file used to store the Header including main navigation.
* `partials/includes/footer` - Page Footer file used to store the Footer including secondary navigation.

Setting Pages up with appropriate Template, Header & Footer files allows us to only write the code once and apply it consistently across all of our theme pages. It also makes it easier to update later if we’d like to. For more information on page structure checkout: [Templates - Getting Started](/site-manager2/templates.md).

![](../../assets/1m1nO4GayNeKDrW66UBjw\_theme-module-layouts-1.png)

Open the `Module_Siteglide_ThemeDemo` project folder you downloaded earlier and navigate into `modules/<module_name>/public/views`. From here, drag and drop all three `layouts`, `pages` & `partials` folders into your own Module project views folder.

### Correcting Your Files

As we’ve been copying files from the Theme Demo Module, we’ll need to update the module name in some paths written in the files. Open up your IDE and bulk find/replace `module_76` with your `<module_name>`.

## Module Setup Files

Next, we want to create one of the setup file options available: install-process.json.

Create a file called install-process.json on the root folder of your Module Project (alongside /modules/). Checkout [Module Setup Files](/developer-tools/building-for-marketplace/create-folder-structure#module-setup-files.md) for more info.

Add the following Code Snippet to your newly created Install Process file:

```none
{
  "1.0.0": "set_homepage"
}
```

Adding this line of code to the install-process.json file will ensure that when a user installs our module, the home/start page is automatically applied as part of the installation. Otherwise, the existing home/start page on a site will be honoured.

## View Your Staging Module Site

Now that we have added all of the core assets and views to our module, let’s see it in action!

Using CLI run the [deploy command](/developer-tools/cli/reference#deploy.md) to send all of the files within your project folder up to your staging site.

![](../../assets/nBrvK3QRxl04hiWbB\_\_sv\_theme-module-deploy-1.png)

Open your staging site to view your work both front-end and back end.

Your site should now look and behave like this front-end: [Module Siteglide Theme Demo](https://module-siteglide-theme-demo.staging.oregon.platform-os.com/).

If you’re happy everything looks as it should, continue to the final step. If not, check back along the steps above to make sure you’ve not missed anything.

## Submit Module For Approval

First, delete the `marketplace_builder` folder from your project folder on your local machine. We don’t want to include this to avoid overwriting any pre-existing content on sites which install our module.

### Preparing To Submit

Follow the checklist to confirm your Theme Module is ready for submission:

* [ ] You’ve got all your files (assets, logic, layouts etc.) in the correct folders (private, or public)
* [ ] Your module folder is named in the correct format of `<module_name>`
* [ ] You have not included a `marketplace_builder` folder
* [ ] You’ve prepared your setup.json file if a model is required for this Module and the Module ID in setup.json matches the Vanity ID in Siteglide Admin

Here is what your project folder should now look like:

![](../../assets/ib89QWFYkVQU6a8T4V96o\_theme-module-project-ready-1.png)

### GitHub

Now that we have prepared our files, if you haven’t already create a new GitHub Repository and commit your project folder to it.

Please ensure:

* [ ] Your Module is in a branch named master in your GitHub Repository. This is the only branch Siteglide will read from. Note that Github may name your branch main by default. If that happens you can change that [here](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-branches-in-your-repository/renaming-a-branch)

### Sending your Module to Siteglide

Next we will need to update the Module item that you made in Admin earlier to include some extra information. Checkout the [Sending your Module to Siteglide](/developer-tools/building-for-marketplace/submit-module-for-approval#sending-your-module-to-siteglide.md) doc for more information.

Once you’ve submitted your Module for approval you’ll need to give us access to see the Module. This is needed for the initial approval, but also for ongoing access to be able to install the latest version of the Module. To provide us with access you need to invite Siteglide API ( [api@siteglide.com](mailto:api@siteglide.com) ) as a collaborator for the GitHub Repository. Checkout the [After Submitting your Module](/developer-tools/building-for-marketplace/submit-module-for-approval#after-submitting-your-module.md) doc for more information.

## Updating & Maintaining Your Module

There are a couple of key things you should be aware of when managing and updating your module moving forward. Checkout this doc for more info: [Updating Existing Modules](/developer-tools/building-for-marketplace/updating-existing-modules.md).
