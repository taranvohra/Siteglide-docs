---
description: Page Templates help you standardise how multiple pages look/work
---

# 🏗️ Create a Page Template

A Page Template is an essential component, any of our Marketplace Templates will come with at least one already but you can create them here:

<figure><img src="../../.gitbook/assets/SiteBuilder-Page-Templates.jpg" alt=""><figcaption><p>One template already exists (Main) but you can create more if needed</p></figcaption></figure>

SiteBuilder simply leverages the Page Templates functionality in Siteglide but builds it for you with useful options to save you time.

In the popup, choose:

* A name e.g. "Main"
* Default Page Template - optional
* the Flowbite Theme (other SiteBuilder Themes will be available to download from Marketplace)
* Optionally, add a Menu, but this is not neccesary for this tutorial

Themes automatically add any of the following to a Page Template:

* CSS
* JavaScript
* Config Files
* Standard Page Template HTML and Liquid

These will then be applied consistently to any Page the Page Template is attached to.

Once created, you can find your template in the SiteBuilder Page Templates tab and in the Siteglide Admin under `SITE MANAGER > Templates`. These Page Templates are fully editable and you can attach them to Siteglide Pages as normal.

Once you've created a Page Template, you'll unlock the PageBuilder, Layouts and Settings tabs.

### Flowbite-specific options

{% hint style="info" %}
The Flowbite template starts with a default Tailwind CSS file which allows most layouts to work out of the box, but if you want to start changing things, you'll need to follow the rest of these setup steps!
{% endhint %}

When creating your Page Template, you can select a Tailwind build method of either:

* CLI
* Preview
* Use the default from the SiteBuilder Settings tab

When editing your Page Template later, you can modify the `template_build_method` parameter and set it to either `'cli'`, `'preview'` or empty string `''`.

You can learn more about [which build method to use here](about-sitebuilder/tailwind-css-themes-choosing-a-build-method.md), or continue to[ set up our recommended CLI method](set-up-tailwind-css.md)!
