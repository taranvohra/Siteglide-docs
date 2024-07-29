# Module Setup

Here we will outline the process involved in creating, building, submitting, and maintaining a Module in the following series of docs.

## Prerequisites

* [ ] Know how to use CLI - [introduction.md](../../../developer-tools/cli/introduction.md "mention")
* [ ] Know how to use Github - [GitHub](https://github.com/)
* [ ] Your IDE (Integrated Development Environment) of choice (VSCode, Atom, Sublime etc)

## Introduction

We will use the [Siteglide Theme Demo](https://github.com/Siteglide/Module\_Siteglide\_ThemeDemo) as an example of a pre-built Module which is available on the Marketplace which you can install on your own staging site to view.

With that in mind, anywhere in this documentation where you see text wrapped in `<>` are placeholders. For example `<module_name>` would be `module_76` with the Siteglide Theme Demo module (more on this later!).

## Create your Module in Siteglide

The first step to building your module is to create a listing for it in Siteglide. Within your Portal from the left-hand menu, select “Custom Modules” and then click the blue “+ Add New Module” button in the top right-hand corner.

![](../../../assets/Z3A0h1xufodpWF\_DGlyFX\_screenshot-2022-03-10-at-110207.png)

Next, fill in the Module Details form. For now, you only need to provide the following basic information:

* **Name**: The name of your module shown in the Marketplace and Siteglide Admin.
* **Version**: A version number following the [Semantic Versioning](https://semver.org/) standard. Usually this would start as 1.0.0.
* **Description**: Small text description of what the Module is - appears in ? icon in ‘name’ column on the Module installation page.
* **Type**: Which category you would put your module into.
* **Show Menu Item**: Does your module need to be within the sites menu under “Modules”? For example for a theme that has no items then this would be set to No.

We will come back later to enter information into the remaining fields, so for now click the blue “Save” button in the bottom right-hand corner to save your new module. Your module will only be visible to yourself at this point as it is not marked as “Public” and has not been approved for the Marketplace.

### Vanity ID

Now that you have created your new module, when you view it you will see that it has a “Vanity ID” field. Make a note of this number for later as it will be used within the Module.

![](../../../assets/stqCwmwpnsFI2fIdbpvC1\_custom-module-vanity-id-2.png)
