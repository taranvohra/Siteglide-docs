# 🔹 Support for Marketplace Modules

### Who is this aimed at? <a href="#who-is-this-aimed-at" id="who-is-this-aimed-at"></a>

This route is for those who are creating a Siteglide module which adds database functionality to Siteglide. It shows how SiteBuilder compatible layouts can be included within the module itself.

Through this route, you can create layouts for your module for any existing themes which allow extension. For example, you may add either Flowbite or Bootstrap layouts for your module to cater for both sets of users.

If a theme-creator does not generally allow extension, please contact them to see if they would consent to allow you to extend their theme.

#### Understanding this documentation <a href="#understanding-this-documentation" id="understanding-this-documentation"></a>

We'll add both a commented example you can look at on Github and an explanation here.

#### Registering the Module with Siteglide <a href="#registering-the-module-with-siteglide" id="registering-the-module-with-siteglide"></a>

The first step is to register your module in the Siteglide marketplace in order to receive your module's Siteglide marketplace ID (if you haven't already). You'll need to reference this ID in several places, so make a note of it.

To start with, you just need to fill out the required fields. Add a name and set the type to "module", write a short description and initial version e.g. 0.1.0.

The "Vanity ID" will then appear. This is the unique ID that can be used across the marketplace to refer to your module.

#### Registering the Module with SiteBuilder <a href="#registering-the-module-with-sitebuilder" id="registering-the-module-with-sitebuilder"></a>

Most of the files in your module will be in the private folder so SiteBuilder won't know they're there unless it knows where to look. You'll next need to create the following file at the public path: `modules/module_<module_vanity_id>/public/views/partials/sitebuilder/module_registry.liquid` to make your module available to SiteBuilder.

```liquid
---
metadata:
  enabled: true
  module_id: module_<module_vanity_id>
  type: module
---
```

The placeholder \<module\_vanity\_id> should be replaced by the vanity ID that Siteglide gave you earlier.

#### File Structure and Security <a href="#file-structure-and-security" id="file-structure-and-security"></a>

While most of your module files will sit in the private folder, Liquid allows developers to access private files if they know their filepaths.

To give an optional extra level of protection to your intellectual property, you can register your module with Sitegurus in return for a secret key. We'll give you this secret key and associate it with your module vanity ID so that SiteBuilder can find your files, but your users can't. When you're given your secret key, the /sitebuilder/ folder will be replaced in your file structure with /sitebuilder\_\<secret\_key>/

Do bear in mind that this system isn't perfect and we cannot guarantee that Liquid errors will not expose this key. We recommend careful testing to avoid errors with each new version.

If your module is open-source or you want to keep things simple, feel free to skip this section.

#### Configuring the Module <a href="#configuring-the-module" id="configuring-the-module"></a>

To configure the module and help SiteBuilder understand at a high level what content it contains, you need to create a file at the following path:\
`modules\module_<module_vanity_id>/private/views/partials/sitebuilder<secret_key_preceded_by_underscore>/module_config.liquid`. If you skipped the last section, you would keep the "/sitebuilder/" folder without an underscore or secret key.

```liquid
{
  "module_<module_vanity_id>": {
    "title": "Example Module", 
{% raw %}
{% comment %}String. Required. The title of your module in Siteglide{% endcomment %}
    "description": "A simple module with a title, image and rich text field.", {% comment %}String. Optional. A description of what your module does. This is not currently used, but may be used in future.{% endcomment %}
    "install_type": "default", {% comment %}String. Required. Leave as "default". Only the "forms" module uses a different value.{% endcomment %}
    "external_docs_link": "", {% comment %}String (absolute URL). Optional. If you have documentation for your module, add the URL here.{% endcomment %}
    "sub_modules": { {% comment %}Object. Required. Sub-modules allow you to categorise different kinds of layouts used by your module. For Example, the Secure Zones Module contains Login Forms and Logout buttons and both are output using a different Liquid tag. If you don't need sub-modules, there is an example below this of what that object should look like.{% endcomment %}
      "1": { {% comment %}String (integer as string). Required. Each sub-module should be given a unique ID. It's easiest to count up from 1.{% endcomment %}
        "name": "Layouts without a Login Button", {% comment %}String. Required. This name is visible both as a tag within the layout card and as a heading in the layout list to organise layouts via their sub_modules.{% endcomment %}
        "liquid_tag": "module", {% comment %}String. Required. When an "include" liquid tag is created, what will the first parameter be? In almost all cases, this should be "module".{% endcomment %}
        "allow_default_settings": true, {% comment %}Boolean. Required. Setting to true means that when a layout of this module is added through PageBuilder, the normal module settings like "per_page" will be offered to the module user in the settings side-panel. If any of these settings don't make sense, you should set this to false and manually add any settings which are needed instead, see the example further below. {% endcomment %}
        "define_new_settings": [],
        "siteglide_module_id": "<module_vanity_id>" {% comment %}String or null (integer as string). Required. This will for a default sub_module almost certainly be your <module_vanity_id>. It controls the "id" parameter when either layouts or PageBuilder outputs a Liquid tag for one of your layouts.{% endcomment %}
      },
      "2": {
        "name": "Layouts with a Login Button",
        "liquid_tag": "module",
        "allow_default_settings": true,
        "define_new_settings": [],
        "siteglide_module_id": "<module_vanity_id>"
      }
    },
    "available_on_pagebuilder": true, {% comment %}Boolean. Required. Set to true for your module to appear in PageBuilder.{% endcomment %}
    "extends_themes": ["theme_01"] {% comment %}Array. Required (can be empty array). This setting allows your module to add layouts to themes created by others in the marketplace. You can find theme IDs in the documentation for themes found in the marketplace. Normally these should be of the format "theme_" followed by the vanity ID of the theme's Siteglide module. At the time of writing, there are two themes built in to SiteBuilder: "theme_01" is Flowbite and "theme_02" is Bootstrap. It is possible for the theme creator to deny all modules the ability to extend their theme or to allow only certain modules to extend it. If you're not sure, ask the module creator for permission. Sitegurus generally welcomes module creators to extend any theme we maintain.{% endcomment %}
{% endraw %}

  }
}
```

Note that this file is a liquid file and allows Liquid syntax, but at runtime will compile to a JSON file. This means you must write the syntax so that the end result validates as JSON or risk introducing Liquid errors into the module as a whole. Comments can be added as Liquid comments (as we have used), as these will be removed at runtime.

**Modules without sub-modules example**

Here is an example of the Blog module's configuration which does not have sub-modules. You should always provide a "default" sub-module instead of the list in the example above.

```liquid
"sub_modules": {
  "0": { 
{% raw %}
{% comment %}String (integer as string). Required. The key for a "default" sub-module should always be 0.{% endcomment %}
    "name": "default",{% comment %}String. Required. The name for a "default" sub-module should always be "default".{% endcomment %}
    "liquid_tag": "module", {% comment %}String. Required. When an "include" liquid tag is created, what will the first parameter be? In almost all cases, this should be "module".{% endcomment %}
    "allow_default_settings": true,{% comment %}Boolean. Required. Setting to true means that when a layout of this module is added through PageBuilder, the normal module settings like "per_page" will be offered to the module user in the settings side-panel. If any of these settings don't make sense, you should set this to false and manually add any settings which are needed instead, see the next example below. {% endcomment %}
    "siteglide_module_id": "3" {% comment %}String or null (integer as string). Required. This will for a default sub_module almost certainly be your <module_vanity_id>. It controls the "id" parameter when either layouts or PageBuilder outputs a Liquid tag for one of your layouts.{% endcomment %}
{% endraw %}

  }
}
```

**Modules with non-standard parameters in their Liquid Tags**

The following example shows the configuration for the "Headers" sub\_module within the built-in Menu Module. Since the Siteglide Liquid tag offers slightly different parameters from a normal module tag, the settings must be configured to reflect this.

We will only comment on the parts of this example which are different from the previous example. Return to the previous example for an explanation of the other keys.

```liquid
"sub_modules": {
  "1": {
    "name": "Login Forms",
    "liquid_tag": "login_form",
    "allow_default_settings": false, 
{% raw %}
{% comment %}Boolean. Required. In the Siteglide menu module there is no such thing as a per_page parameter (and several other default settings don't work either) so we disable default settings. In your module it is most likely that you'll wish to keep this as true and add new settings on top of the default settings. {% endcomment %}
    "define_new_settings": [ {% comment %}Array (array of objects). Optional. {% endcomment %}
        { {% comment %}Object. Optional. Describes adding a single setting in PageBuilder to set a parameter in the Liquid tag which will be generated in the page. Rememeber that with Liquid inheritance you can actually pass any unreserved parameter to the Liquid tag and it will be inherited in the Layout, so this is a very flexible tool.{% endcomment %}
            "key": "redirect", {% comment %}String. Required. This is the key of the parameter that's available in the liquid tag.{% endcomment %}
            "name": "Redirect", {% comment %}String. Required. This is the name of the setting shown in PageBuilder. It is essentially the same as the key, but can be more user-friendly. In this example it just capitalises the key.{% endcomment %}
            "type": "string", {% comment %}String. Required. The type of value. At the moment only "string" is available, but we can add more on request, for example "array".{% endcomment %}
            "default": "/my-account", {% comment %}String. Required. A default value for the setting. Can be empty string if no default is needed..{% endcomment %}
            "required": true {% comment %}Boolean. Required. Set to true to make sure this setting has a value for the user to continue. It is our intention to make required settings appear in the main body of PageBuilder rather than the settings sidepanel. This should make it easier for the user to focus on the required fields.{% endcomment %}
        }
    ],
    "siteglide_module_id": null {% comment %}String or null. Required. While this is normally an essential, for this particular secure zones Liquid tag, Siteglide does not use an ID parameter. In your module, this would be very unlikely. Most likely you'd add your <module_vanity_id> as in the examples above.{% endcomment %}
{% endraw %}
  }
}
```

#### Configuring Layouts <a href="#configuring-layouts" id="configuring-layouts"></a>

While layout code is stored in files in your main file structure, the layout\_config liquid file is needed to give SiteBuilder the metadata it needs to display these layouts in the UI, find the files it needs and install them to the correct folders.

These instructions are mostly the same whether you are a module or a theme creator, so from here we'll link you to the joint documentation on configuring layouts. Just note that for module creators, you would normally only link layouts back to your module vanity ID and submodule ID.

If you wanted to add for example a front-end eCommerce layout for users to buy the content in a courses module, you could harness sub-modules to achieve this.
