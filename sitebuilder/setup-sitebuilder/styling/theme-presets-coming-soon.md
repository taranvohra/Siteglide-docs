---
description: >-
  Theme Presets are a Way to change a Theme's CSS variables, like colour and
  font, giving your site an interesting new look without needing to make big
  changes to HTML or CSS classes.
---

# 🏗️ Theme Presets

## Pre-Requisites

* You have [set up the Siteglide CLI](../site-setup/) ready for use on a Site
* You understand Siteglide-CLI [Pull](https://docs.siteglide.com/en/developer-tools/cli/reference#pull) and [Sync ](https://docs.siteglide.com/en/developer-tools/cli/reference#sync)commands&#x20;
* You have [created a Flowbite\* Page Template](https://docs.siteglide.com/en/sitebuilder/setup-sitebuilder/site-setup/create-a-page-template) from the SiteBuilder Module
* You have set up your project [ready to use Tailwind CSS via CLI](../set-up-tailwind-css.md) with the SiteBuilder module's recommended file structure

## About Presets

Theme Presets are a Way to change a Theme's CSS variables, like colour and font, giving your site an distinctive new look without needing to make changes to HTML or CSS classes. They should be compatible with all our existing Flowbite layouts\*.\
\
They are useful for:

* Create new sites using the SiteBuilder layouts, and give them a distinctive look from step one.
* Take an existing site and try it out with different Presets to help you or your client visualise different design choices with the real content.

### How it Works

Our Presets use Tailwind CSS Presets and Plugins behind the scenes.

To allow you to change the currently selected preset from the SiteBuilder Settings tab, we use a small, boilerplate preset called  `sitebuilder_preset_settings.js`. When the SiteBuilder settings are updated to select a new preset, this file is modified to point at the Preset you have selected.

Small Plugins are included within Presets in order to enable them to set global styling like fonts as well as changing variables which affect existing utility classes.

{% hint style="info" %}
\*Our first release of Theme Skins only supports Tailwind-based Themes, since we are able to leverage the powerful presets feature provided by Tailwind.
{% endhint %}

## Getting Started - Coming Soon

The easiest way to get started with a Theme Preset will be to install a site from one of our Site Templates which will come with a specific Preset already set up. We are currently working on these, so watch this space.

## Usage - Via SiteBuilder Settings

1. Open the Modules / SiteBuilder Module
2. Navigate to the Settings tab.
3. Select a Preset from the options.
4. Each Preset may have different versions. To get started, keep the default selected version.
5. Save your settings. This will save the setting and modify settings files on your site, but your Tailwind distributable CSS file will still need to be compiled using the Siteglide CLI - more on that next.&#x20;
6. Next, go to your code editor and open a terminal window. Close any sync commands that are currently running and run a `siteglide-cli pull` command. This will pull down the files for each Preset in the module and the newly-updated `sitebuilder_preset_settings.js` file.

{% hint style="info" %}
Do not directly modify either the `sitebuilder_preset_settings.js` file or other files in the `modules/module_86/public` folder since the module settings may overwrite your changes.
{% endhint %}

7. Check your Tailwind CSS config (normally at path `marketplace_builder\assets\modules\module_86\src\tailwind.config.js`) and your Tailwind CSS source file, normally at path: `marketplace_builder\assets\modules\module_86\src\tailwind.css`.
   1.  Set the presets option in your config to point at the `sitebuilder_presets_settings` file:

       ```javascript
       module.exports = {
         // Pointing Presets at the router file will allow the SiteBuilder module to change theme skin defaults. Anything you write in the "theme" object can override this.
         presets: [
           require('tailwindcss/../../modules/module_86/public/assets/css/presets/sitebuilder_preset_settings')
         ],
         ...
       }
       ```
   2. Variables in your config will [merge](https://tailwindcss.com/docs/presets#merging-logic-in-depth) with variables in the Preset. If you wish for the Preset to change specific variables, you may wish to selectively comment-out parts of your Preset which set the same variables.&#x20;
   3. CSS rules in your CSS source file may override the Preset's plugins, which might for example be setting fonts. If you wish for the Preset to set these rules, you may wish to selectively comment-out CSS rules.&#x20;

{% hint style="info" %}
The newer default config and source CSS files we provide will start with a leaner initial config than in previous SiteBuilder versions. These new versions of the files will already point to the `sitebuilder_presets_settings.js` and will override less variables with Flowbite defaults so these steps will not normally be necessary on a new site.&#x20;
{% endhint %}

8. Start a `siteglide-cli` sync command.
9. Start a `npm run tailwind` command. A new `tailwind.min.css` file will be created and synced, using the new Preset and your existing CSS rules.

That's it! Any Pages which are using a Page Template which links to this new CSS file will be restyled to use this Preset's variables.&#x20;

### Troubleshooting

1. Make sure the Page you are testing with uses a Flowbite Page Template. (We will support other Themes in future, but currently Presets are only available on Themes which use Tailwind, of which Flowbite is the only one currently).
2. Make sure the SiteBuilder settings have either Preview Mode or CLI Mode selected. JIT mode should not be selected as this does not support Presets.
3. Check the Tailwind Docs for more information about how Presets handle conflicts with your own config and source CSS. You may be expecting the Site's appearance to change, but your own variables may be preventing that change.
4. Check that any classes you are testing are present in the layouts you are using. Tailwind CSS's tree shaking means that if an element does not have the class `bg-accent-500` that class won't be included in the `tailwind.min.css` file even if the preset defines this colour.
5. Try manually then saving and syncing the tailwind.min.css file to confirm it has uploaded since making changes.&#x20;
6. Make sure you are not directly modifying files in the `modules/module_86/public` folder. These can be overridden by the module, so your changes could be lost.&#x20;

## Modifying Default Behaviour and Disabling Features

We have designed the Presets feature to strike a balance between convenience and flexibility. To a large extent, reading the Tailwind documentation on:

* [Configuration](https://tailwindcss.com/docs/configuration)
* [Presets](https://tailwindcss.com/docs/presets)
* [Plugins](https://tailwindcss.com/docs/plugins)

And referencing the preset JS files in the modules/module\_86/public/assets/presets directory will allow you to modify behaviours to suit your needs. We will just cover a few common use-cases relevant to using this feature with Siteglide.

### Preventing SiteBuilder Settings from Changing Preset

Once you've experiemented with Presets and have made a decision on whether to use a specific preset, no presets or a preset from a third party, you may no longer wish to allow the SiteBuilder module's settings to change the preset. If so, you can change your configuation to stop pointing at:&#x20;

```javascript
require('tailwindcss/../../modules/module_86/public/assets/css/presets/sitebuilder_preset_settings')
```

...and instead point directly at your chosen Preset's file location, or set presets to an empty array `[]` to completely disable all presets including Tailwind's default settings or remove the presets key completely to remove presets but keep Tailwind's defaults.&#x20;

## Preset Versions

&#x20;This allows a Preset creator to make changes without affecting your live sites, since your site can continue to safely use an older version without maintenance and updates.&#x20;

We don't anticipate that it will be common practice to update a version of a Preset on a live site, but it is an option that's open to you.\
\
If you're starting a project from the beginning, it will probably make sense to use the latest version unless you are avoiding specific known issues in the newest version.\


