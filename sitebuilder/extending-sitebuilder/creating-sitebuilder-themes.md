# ℹ️ Creating SiteBuilder Themes

## Creating a New Theme for SiteBuilder <a href="#creating-a-new-theme-for-sitebuilder" id="creating-a-new-theme-for-sitebuilder"></a>

A theme module in Siteglide is generally a module which does not add database functionality to the Siteglide Admin or the front-end, but does add files which are helpful for styling the front-end of a website. With the help of this documentation, you can go a step further by hooking into SiteBuilder functionality:

1. Page Templates

* You'll be able to configure SiteBuilder to create a Siteglide Page Template, containing all the global CSS and JS your theme needs for its HTML to look and interact as expected.

2. Layouts

* Any static or dynamic HTML or Liquid (respectively) layouts will not be installed straight away on a user's site, but will be available in the module UI. There are two main advantages of this: firstly, it avoids clutter; secondly, it allows you to make improvements to layouts without breaking any of the module-user's own changes- instead your improvements will be fetched next time the layout is installed.

3. Compatibility with Other Themes

* Building a theme module lets you create a single theme per module. However, by configuring the settings, you can mark your theme as compatible with other themes which use a similar CSS framework. This allows module-users to use layouts from several simialr thems on the same site.

### About our example theme <a href="#about-our-example-theme" id="about-our-example-theme"></a>

In this documentation, for an example, we'll be creating a theme for the Siteglide Studio Design System. As this theme is moving to being deprecated on Siteglide, it's an excellent opportunity to turn it into an open-source theme module to show you what is involved.

### Step 1 - Registering the Module in the Siteglide Marketplace <a href="#step-1-registering-the-module-in-the-siteglide-marketplace" id="step-1-registering-the-module-in-the-siteglide-marketplace"></a>

You'll need to register the new module with Siteglide to receive the "vanity\_id". We'll use this as a unique ID to identify your theme and module within SiteBuilder.

First in the Siteglide Portal, go to the marketplace tab and select "add new".

Secondly, fill out the name, type and description. For type, select "theme".

Thirdly, make a note of your "vanity ID". We'll refer to this as \<module\_vanity\_id> where it needs to be substituted in the examples.

### Step 2 - Registering the Module with SiteBuilder <a href="#step-2-registering-the-module-with-sitebuilder" id="step-2-registering-the-module-with-sitebuilder"></a>

Most of the files in your module will be in the private folder so SiteBuilder won't know they're there unless it knows where to look. You'll next need to create the following file at the public path: `modules/module_<module_vanity_id>/public/views/partials/sitebuilder/module_registry.liquid` to make your module available to SiteBuilder.

```liquid
---
metadata:
  enabled: true
  module_id: module_<module_vanity_id>
  type: theme
---
```

The placeholder \<module\_vanity\_id> should be replaced by the vanity ID that Siteglide gave you earlier.

### Step 3 - File Structure and Security <a href="#step-3-file-structure-and-security" id="step-3-file-structure-and-security"></a>

While most of your module files will sit in the private folder, Liquid allows developers to access private files if they know their filepaths.

To give an optional extra level of protection to your intellectual property, you can register your module with Sitegurus in return for a secret key. We'll give you this secret key and associate it with your module vanity ID so that SiteBuilder can find your files, but your users can't. When you're given your secret key, the /sitebuilder/ folder will be replaced in your file structure with /sitebuilder\_\<secret\_key>/

Do bear in mind that this system isn't perfect and we cannot guarantee that Liquid errors will not expose this key. We recommend careful testing to avoid errors with each new version.

If your module is open-source or you want to keep things simple, feel free to skip this section.

### Step 4 - Configuring your Theme <a href="#step-4-configuring-your-theme" id="step-4-configuring-your-theme"></a>

You'll need to add a theme\_config file at the following path: `modules/module_<module_vanity_id>/private/views/partials/sitebuilder<secret_key_preceded_by_underscore>/theme_config.liquid`. This adds the metadata SiteBuilder needs to understand your theme.

For the content, add the following, adapting it to your module where suitable:

```liquid
{% raw %}
{% comment %}Something{% endcomment %}
{
  "theme_<module_vanity_id>": {
    "title": "Siteglide Studio", {% comment %}String. Required. The name of your Theme.{% endcomment %}
    "enabled": true, {% comment %}Boolean. Required. Set to true to enable your theme.{% endcomment %}
    "image": "https://res.cloudinary.com/.../siteglide-studio.png", {% comment %}String (absolute path to image URL). Required. The banner image which will be displayed on the Page Template card when a template is created using this theme.{% endcomment %}
    "thumbnail_logo": "https://res.cloudinary.com/.../siteglide-studio-small.svg", {% comment %}String (absolute path to image URL). Optional. The smaller logo which will be displayed on the Layout Card for this Theme's layouts. Transparent background and square image recommended. It need be no bigger than 80px * 80px;{% endcomment %}
    "description": "This is an open source version of the now deprecated Siteglide Studio Design System designed to work with the SiteBuilder module.", {% comment %}Description{% endcomment %}
    "css_framework": { {% comment %}Object. Optional. This can help theme users understand its compatiblilty with other themes, for example two different themes using Bootstrap may look different, but the underlying code in their layouts may be so similar that it's useful to show layouts from both. If there is no relevant CSS framework, remove this property.{% endcomment %}
      "title": "Bootstrap 5", {% comment %}String. Required. The name of the CSS framework this theme uses. {% endcomment %}
      "logo": "https://res.cloudinary.com/sitegurus/image/upload/v1653915047/modules/module_86/admin/frameworks/icons/bootstrap-logo.svg", {% comment %}String (absolute URL for image). Optional. A small logo for the CSS framework which will be displayed on the Layout Card for this Theme's layouts.Transparent background and square image recommended. It need be no bigger than 80px * 80px;{% endcomment %}
      "docs_url": "https://getbootstrap.com/docs/5.0/getting-started/introduction/", {% comment %}String. Optional. Link to CSS framework docs. These may be distinct from your theme documentation. {% endcomment %}
      "show_sitebuilder_tailwind_settings": false, {% comment %}Boolean. Required. Mark false unless your CSS framework uses Tailwind. This gives this theme access to SiteBuilder's Tailwind Options instead of CSS preferences below.{% endcomment %}
      "show_framework_on_layout_card": false {% comment %}Boolean. Optional. If your theme and CSS framework have the same name e.g. Bootstrap and Bootstrap, mark as false to avoid repetition. If not, mark as true to display both Theme and Framework on the Layout card.{% endcomment %}
    },
    "layouts": {%- include 'modules/module_<module_vanity_id>/sitebuilder/theme_<module_vanity_id>/layout_config' -%}, {% comment %}Liquid include. Required. You can copy this as in the example. It links to the layout_config file which will be explained later.{% endcomment %}
    "modules": [  "module_s1",  "module_2",  "module_s2",  "module_3",  "module_s3",  "module_5",  "module_8",  "module_10", "module_12"], {% comment %}Array (array of strings). Required. These are the IDs of modules that this theme includes layouts for. A list of built in module IDs are available below.{% endcomment %}
    "approve_all_modules": true, {% comment %}Boolean. Required. Setting this to true allows any module creator to build module layouts for your theme, or any theme creator to mark their theme as compatible with yours. Setting this to false allows you to protect your IP by disallowing this kind of collaboration by default. For open-source themes, it's recommended to set this to true, as allowing collaboration is in the spirit of the open-source community.{% endcomment %}
    "approved_modules": [], {% comment %}Array (array of strings). Required (can be empty array). If you have set "approve_all_modules" to true, you can leave this as an empty array. Otherwise, if you've set "approve_all_modules" to false, you can use this array to specify modules which you've reviewed and would like to specifically allow to extend this theme. Module creators may get in touch with you and request for you to add their module to this list.{% endcomment %}
    "compatible_themes": ["theme_02"], {% comment %}This allows you to mark another theme as compatible with yours, by its ID. This tends to be useful if this theme uses the same underlying CSS framework. If either of two themes has this setting and neither has "approve_all_modules" as true {% endcomment %}
    "theme_not_installable_alone": false, {% comment %}Boolean. Optional. When set to false or unset, this theme is available to those making Page Templates in SiteBuilder. When set to true, this theme is only available as a compatible theme to extend another theme, and cannot be used in a Page Template in its own right. A good example here is Flowbite and Flowbite Pro themes. It would be confusing to give theme users a choice between the two when creating their page template, so only Flowbite has "theme_not_installable_alone" set to false. Flowbite Pro layouts are available though through the compatible themes feature to those using a Flowbite Page Template.{% endcomment %}
    "css_preference_options": {  {% comment %}Object (object map of keys). Optional (can be empty object). We'll explain this further in the next section. {% endcomment %}
      "scss": {  {% comment %}Object (key needs to be unique). Required. The key is both the option ID (you choose) and the folder name of the folder containing the CSS and SCSS files for this option.{% endcomment %}
        "title": "Sass",  {% comment %}Name of option which will display in the dropdown while creating a Page Template.{% endcomment %}
        "default_selected": true,  {% comment %}Boolean. Optional. Set to true if this should be the default option most people will need.{% endcomment %}
        "installable_files": [  {% comment %}Array (array of objects). Required. Add an object to the array of every file you'll need to install for the user to work with the CSS. For example, if this is a SCSS option, you'll need a separate object for each unique SCSS partial file they need.{% endcomment %}
          {  {% comment %}Object. Required.{% endcomment %}
            "src": "bootstrap",  {% comment %}String. Required. The filename of the file containing the CSS/SCSS etc. soruce code. Use URL encoding where a special character is needed, e.g. "%5" for an underscore in a CSS file. {% endcomment %}
            "ext": ".min.css",  {% comment %}String. Required. The extension the file should be given once installed..{% endcomment %}
            "link_in_template": true  {% comment %}Boolean. Required. If the file is required at runtime on the front-end, for example a file with .min.css extension, set this to true. Else, if this file is only intended to be used as a developer tool during build-time, mark to false. This means the Page Template will only load the CSS files it actually needs.{% endcomment %}
          },
          {
            "src": "bootstrap-theme",
            "ext": ".scss"
          },
          {
            "src": "%5Fcustom-styles",
            "ext": ".scss"
          },
          {
            "src": "%5Fcustom-variables",
            "ext": ".scss"
          }
        ],
        "description": "Creates Sass files on your site which you can use via Siteglide CLI. Note this will work with scss compilation tools which support the @import rule https://sass-lang.com/documentation/at-rules/import ." {% comment %}String. Required. Use this description to explain the benefits and limitations of this build method, as well as wany other instructions they'll need to use it.{% endcomment %}
{% endraw %}
      },
      "min_css": {
        "title": "Minified CSS",
        "installable_files": [
          {
            "src": "bootstrap",
            "ext": ".min.css",
            "link_in_template": true
          },
          {
            "src": "main",
            "ext": ".css",
            "link_in_template": true
          }
        ],
        "description": "Creates one minified file containing the framework's CSS code and provides a second unminified custom CSS file which you can use to make custom overrides."
      }
    }
  }
}
```

### Step 5 - Adding CSS Files to be used on Page Templates <a href="#step-5-adding-css-files-to-be-used-on-page-templates" id="step-5-adding-css-files-to-be-used-on-page-templates"></a>

In the previous step, when editing the theme\_config file, there was a CSS preferences object. Here we will look at this, and the alternative and add the files that are referenced in the config.

**CSS File Structure**

This is an example CSS file structure for the same theme.

```bash
└───modules
    └───module_113
        └───private
            └───views
                └───partials
                    └───sitebuilder
                        └───theme_113
                            └───css
                                ├───default
                                │       css.liquid
                                │
                                ├───min_css
                                │       custom.liquid
                                │       main.liquid
                                │
                                └───scss
                                        %5Flayouts.liquid
                                        %5Fmain.liquid
                                        %5Fstudio.liquid
                                        %5Fvariables.liquid
                                        main.liquid
```

Copy

**Default CSS**

Firstly, `../css/default/css.liquid` contains a Liquid snippet which will be added to all templates created using your theme. This happens regardless of whether or not a CSS preference is chosen (see next sub-section).

This file will contain Liquid/HTML. For example, it can be useful to include tags to files which are hosted on an external CDN and don't need to be hosted on Siteglide or edited. It can also contain inline style tags, should you so wish.

It is okay to include a small amount of JS here, for example, Flowbite includes a few lines of render-blocking JS so that dark mode is supported immediately on page load. As in this example, it's recommended that JS is only included here where it relates to styling. Another file exists for the main JS includes.

If you don't need to use this, you _must_ include the file, but please leave the contents completely blank.

**CSS Preferences**

As well as default CSS, you can choose to have some CSS files which are copied onto the module user's site and hosted there. The benefit of this is that it allows the module-user to edit that CSS.

This feature is very flexible. For example, you can cater to both module-users who prefer writing native CSS or users who use SCSS; you configure the options and then let the user decide which to install when they create a template.

We hope the flexibility is enough to enable a wide range of CSS frameworks.

1. Create a folder for each option you'd like to give the user. In the example file structure above, there is `min_css` and `css`. These folder names must match the keys in the theme\_config's `css_preference_options` object.
2. Within each folder, create a liquid file for each file you'd like to install. The file should be named the same as the destination file, but you must replace any special characters with their URL encoded equivalents. For example, an underscore should be replaced with `%5F`- see the example.
3. In each file, add YAML at the top of the Liquid file to add the following metadata- the role of this is to set what the extension of the final destination file will be.

```bash
---
metadata:
  file_extension: ".css"
---
```

4. Below this add the body of the file. e.g. the actual CSS/SCSS code.
5. When a user selects this option while building a template, all the files will be created on their site- but not all will have HTML `<link>` tags added to the template. - Remember to add the `link_in_template: true` property in the theme\_config for each option where this is needed- e.g. for `.min.css` files but not for `.scss` files.

If you don't need the CSS preferences feature, leave the "css\_preference\_options" property as an empty object `{}` in the theme\_config.\


#### Step 6 - JavaScript <a href="#step-6-javascript" id="step-6-javascript"></a>

To add JavaScript (which you don't expect to be edited by the ordinary module-user) to any templates which need to be installed, you can add any script tags to the path `modules/module_<module_vanity_id>/private/views/partials/sitebuilder/theme_<module_vanity_id>/js.liquid`. These will be added to the template, as is, when the template is created.

The JavaScript itself, where necessary, should be added to `.js` files in your module's private folder, or you may choose to link to scripts in a CDN.

**Editable JavaScript**

If there is some JavaScript you expect to be edited by the user, it's often best to add this as an inline `<script></script>` tag, either in the main js.liquid file, or in an individual layout.

**Inline JS for capturing Liquid variables**

Another situation where it might be useful to write inline JS is if you need to capture a variable from the Liquid. In this case, it's useful to write a short inline script to assign the variables to the global scope and then use a longer external script to use those variables. You can also write an API request to a Liquid page to fetch Liquid variables into your JS.

**Performance**

All JavaScript will be added to the head of the page, for simplicity.

To improve performance, it is recommended therefore that you write as much JavaScript as possible so that it can be deferred or loaded asynchronously.

Tips:

1. Write event listeners instead of using events which are stored in HTML attributes like `onclick=""`. This means that if a button is clicked before the JS is loaded, no "function is not defined" error will occur. The button only becomes interactive once the JS has loaded.
2. If using defer, your JS can normally use the DOMContentLoaded event to run your main JavaScript.

_HTML_

```html
<script defer src="..."></script>
```

_JS_

```javascript
document.addEventListener('DOMContentLoaded', init);
function(init) {
  //Your Code here.
}
```

3. For async code, you won't be able to control the order in which scripts load. To handle any dependencies, you can either use a bundler like Webpack to load JavaScript modules from a registry like npm or use the following pattern to load dependencies efficiently from a CDN:

_HTML_

```html
<script async src="..."></script>
```

_JS_

```javascript
//Check HTML is loaded. If it's already loaded, the document.readyState will show this and run the next function, else the event listener will wait for it to load.
if (
  document.readyState === 'complete'
  || document.readyState === 'loaded'
  || document.readyState === 'interactive'
) {
  loadScripts();
} else {
  //Set event listener or timeout.
  console.log('before load flowbite')
  document.addEventListener('DOMContentLoaded', loadScripts);
}

/* Load any dependencies your JS needs.

Each dependency script is added as a loadScript() function (JS URL as parameter) in the array. Since the loadScript function returns a promise to Promise.all, the script asks for all scripts at once (optimising performance), but won't proceed until they have all loaded successfully.

The scripts in the example are just examples and you'd replace them with your own.
*/

async function loadScripts() {
  window.interactiveElements = {};
  Promise.all(
    [
      loadScript('https://cdn.jsdelivr.net/npm/flowbite@1.5.3/dist/flowbite.min.js'),
      loadScript('https://cdn.jsdelivr.net/npm/choices.js@9.0.1/public/assets/scripts/choices.min.js')
    ]
  ).then(
    function(results) {
      init();
    }
  );
}

function init() {
  //Your code here. All dependencies will be ready to go, the DOM will be loaded, so you are free to write the JS you need with high performance!
}

//Helper function used earlier. This probably won't need editing. Credit to https://abdessalam.dev/blog/loading-script-asynchronously-as-a-promise-in-javascript/

function loadScript(src, async = true, type = 'text/javascript') {
  return new Promise((resolve, reject) => {
    try {
      const el = document.createElement('script');
      const container = document.head || document.body;

      el.type = type;
      el.async = async;
      el.src = src;

      el.addEventListener('load', () => {
          resolve({ status: true });
      });

      el.addEventListener('error', () => {
          reject({
              status: false,
              message: `Failed to load the script src`
          });
      });

      container.appendChild(el);
  } catch (err) {
      reject(err);
  }
  });
};
```
