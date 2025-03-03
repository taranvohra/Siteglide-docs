# ℹ️ Adding Dynamic Layouts to Themes & Modules

### Configuring Dynamic Layouts <a href="#configuring-dynamic-layouts" id="configuring-dynamic-layouts"></a>

These instructions are very similar whether you are following the theme or module creator pathway, so both tutorials converge here.

#### Step 1 - Create the File Structure for Dynamic Layouts <a href="#step-1-create-the-file-structure-for-dynamic-layouts" id="step-1-create-the-file-structure-for-dynamic-layouts"></a>

Each Layout gets its own folder in the file structure. It's position in the file structure is affected by its theme and its module.

Most Siteglide layouts actually consist of more than one layout, so Within that folder, you need to create the same number of source files inside your module folder.

How you organise your files into folders within your layout folder is optional, however, you will need to reference these source files' exact paths in the "src" property of the "files" array in the layout config later.

Module creators will normally have multiple theme folders with a single module folder and single layout\_config file in each. For example:

```bash
└───modules
    └───module_<module_vanity_id>
        ├───private
        │   └───views
        │       └───partials
        │           └───sitebuilder<secret_key_preceded_by_underscore>
        │               │   module_config.liquid
        │               │
        │               └───theme_01
        │               |   │   layout_config.liquid
        │               |   │
        │               |   └───module_<module_vanity_id>
        │               |       ├───1
        │               |       │   └───list
        │               |       │           item.liquid
        │               |       │           wrapper.liquid
        │               |       │
        │               |       └───2
        │               |           ├───detail
        │               |           │       item.liquid
        │               |           │       wrapper.liquid
        │               |           │
        │               |           └───testimonials
        |               |               └───list
        |               |                       item.liquid
        │               |                       wrapper.liquid
        │               └───theme_02
        │                   │   layout_config.liquid
        │                   │
        │                   └───module_<module_vanity_id>
        │                       ├───1
        │                       │   └───list
        │                       │           item.liquid
        │                       │           wrapper.liquid
        │                       │
        │                       └───2
        │                           ├───detail
        │                           │       item.liquid
        │                           │       wrapper.liquid
        │                           │
        │                           └───testimonials
        |                               └───list
        |                                       item.liquid
        │                                       wrapper.liquid
```

Theme creators will normally have only a single theme folder containing multiple module folders to organise layouts accordingly. For Example:

```bash
└───modules
    └───module_<module_vanity_id>
        ├───private
        │   └───views
        │       └───partials
        │           └───sitebuilder<secret_key_preceded_by_underscore>
        │               │   theme_config.liquid
        │               │
        │               └───theme_<module_vanity_id>
        │                   │   css.liquid
        │                   │   js.liquid
        │                   │   layout_config.liquid
        │                   │   static_layouts.liquid
        │                   │
        │                   ├───module_2
        │                   │   └───5
        │                   │           item.liquid
        │                   │           login.liquid
        │                   │           logout.liquid
        │                   │           wrapper.liquid
        │                   │
        │                   ├───module_3
        │                   │   ├───3
        │                   │   │   │   archive.liquid
        │                   │   │   │   search.liquid
        │                   │   │   │   sidebar.liquid
        │                   │   │   │
        │                   │   │   └───list
        │                   │   │           item.liquid
        │                   │   │           wrapper.liquid
        │                   │   │
        │                   │   └───4
        │                   │       │   archive.liquid
        │                   │       │   search.liquid
        │                   │       │   sidebar.liquid
        │                   │       │
        │                   │       └───detail
        │                   │               item.liquid
        │                   │               wrapper.liquid
        │                   │
        │                   │
        │                   ├───module_s1
        │                   │   └───2
        │                   │       │   dynamic_wrapper.liquid
        │                   │       │   static_wrapper.liquid
        │                   │       │
        │                   │       └───components
        │                   │               array_custom.liquid
        │                   │               basic_payment.liquid
        │                   │               boolean.liquid
        │                   │               checkout_standard.liquid
        │                   │               datasource.liquid
        │                   │               datasource_multi.liquid
        │                   │               date.liquid
        │                   │               email.liquid
        │                   │               email_edit.liquid
        │                   │               file.liquid
        │                   │               folder.liquid
        │                   │               heading.liquid
        │                   │               hidden_fields.liquid
        │                   │               image.liquid
        │                   │               image_array.liquid
        │                   │               input_checkbox.liquid
        │                   │               input_radio.liquid
        │                   │               name_field.liquid
        │                   │               number_float.liquid
        │                   │               number_integer.liquid
        │                   │               password.liquid
        │                   │               password_edit.liquid
        │                   │               quote_only.liquid
        │                   │               recaptcha.liquid
        │                   │               select.liquid
        │                   │               select_multi.liquid
        │                   │               string.liquid
        │                   │               subheading.liquid
        │                   │               subscription_detail.liquid
        │                   │               textarea.liquid
        │                   │
        │                   │
        │                   └───static
        │                       ├───hero
        │                       │       3.liquid
        │                       │
        │                       └───new_static_category
        │                               3.liquid
```

Layouts in the same module but different sub-modules will still share the same module folder. The sorting of sub\_modules is done instead based on the layout\_config file, see the next section.

If you want to see the format for adding layout source code to the files in this structure, look at step 4. Otherwise, move on to step 2.

#### Step 2 - Create the Layout Config File <a href="#step-2-create-the-layout-config-file" id="step-2-create-the-layout-config-file"></a>

While the actual code for each layout goes in its own file, SiteBuilder also needs Layout Config Files to give it the metadata needed to display and install layouts correctly.

A layout\_config file is needed for each theme you want to add layouts for.

Theme creators need only create a single layout\_config file for their module. For example, if you're creating a theme, your layout\_config file should be at the following path:\
`modules/module_<module_vanity_id>/private/views/partials/sitebuilder<secret_key_preceded_by_underscore>/theme_<module_vanity_id>/layout_config.liquid`

Module creators will need a layout\_config file per theme they wish to add their module layouts to. For example if a module creator wants to offer their users both Bootstrap and Flowbite layouts (they would have also set the "extends\_themes" key in their module\_config to include the same IDs "theme\_01" and "theme\_02"), they'll need to add files at the following paths:

`modules\module_<module_vanity_id>\private\views\partials\sitebuilder<secret_key_preceded_by_underscore>\theme_01\layout_config.liquid`\
`modules\module_<module_vanity_id>\private\views\partials\sitebuilder<secret_key_preceded_by_underscore>\theme_02\layout_config.liquid`

You'll see the main difference is that the folder named after the theme will either point at a theme you created or a theme created by someone else, depending if you are a theme or a module creator. The theme folder will also contain folders for layout code files as well as the config file.

Step 3 - Configuring the Layout Config Files

The following example is from a module creator's layout\_config file.

Perhaps the most complex and important part of the configuration to pay attention to is the files array. When SiteBuilder installs a layout, it takes a copy of the layout source code you've stored in the private folder and adds those copied files to the marketplace\_builder folder where they can be freely read and edited by the module user. It is therefore important to note the difference between the src property which points at the files you add and the dest property that points to where you wish the files to be installed.

```liquid

{ 
{% raw %}
{% comment %}Object. Required.{% endcomment %}
  "module_<module_vanity_id>": { {% comment %}Object. Required.{% endcomment %}
    "1": { {% comment %}Object (key matches the numbered folder containing the layout files). Required.{% endcomment %}
      "name": "Custom gallery image list", {% comment %}String. Optional (recommended, otherwise SiteBuilder will name the Layout by its module and a number).{% endcomment %}
      "type": "list", {% comment %}String ("default", "list" or "detail"- recommended most situations to choose list or detail. Default is used for modules which have no concept of list or detail, for example forms or some Secure Zones Layouts). Required.{% endcomment %}
      "image": "", {% comment %}String (image absolute URL). Required. A screenshot of the layout on a website. It can be tricky to get this right, but it's worth getting the best quality image possible to make your layout look attractive to users.{% endcomment %}
      "enabled": true, {% comment %}Boolean. Required. Set to false to hide the layout if it is not ready to be shown.{% endcomment %}
      "dest": "layouts/modules/module_<module_vanity_id>", {% comment %}String. Required. This is the main folder where the layouts will be installed. Currently it is not used, but exists for legacy reasons. Instead we use the similar fields inside the files array.{% endcomment %}
      "files": [ {% comment %}Array (array of objects). Required{% endcomment %}
        { {% comment %}Object. Required.{% endcomment %}
          "src": "list/item", {% comment %}String. Required. This should be a filepath relative to the folder with the same ID as this layout's source code. For example, the full filepath referred to here is "modules/module_<module_vanity_id>/private/views/partials/sitebuilder<secret_key_preceded_by_underscore>/theme_01/module_<module_vanity_id>/1/list/item.liquid" but only the path after the "1" folder and without the file extension is needed. {% endcomment %}
          "dest": "layouts/modules/module_<module_vanity_id>", {% comment %}String. Required. This should be a filepath relative to the marketplace_builder/views/partials folder where the module user's "installed" copy of the layout will be placed. Nested layouts, which we'll look at later, for example, embedding an author layout inside a Blog layout, use this to install layouts in any number of required locations.{% endcomment %}
          "install_type": "default" {% comment %}String (default,layout_is_liquid_file). Optional (default is default). Normally leave this property out. The default install process will look for a list/detail folder with the wrapper and item file inside and copy that structure in the destination folder. However, some layouts, like say, an Add to Cart button have a simpler structure with a single file which takes the name of the layout instead of a layout folder. In this case, set the install type to "layout_is_liquid_file"- which will take the file and rename it to have the name of the layout and put it directly inside the dest folder without a list/detail folder.{% endcomment %}
        },
        {
          "src": "list/wrapper", {% comment %}{% endcomment %}
          "dest": "layouts/modules/module_<module_vanity_id>"
        }
      ],
      "sub_module": 1 {% comment %}Integer. Required. Where a module might contain more than one kind of layout, each using a different Liquid syntax to output them, e.g. Secure Zones Login Forms and Logout Buttons, sub_modules are used to distinguish between them. If there is more than one sub_module defined in the module_config file, select the ID of the sub_module which best categorizes this layout. Only if no sub_modules are defined, can you add 0 to select no sub_modules. If you're not sure which sub_modules are available for a module, check the documentation for that module or contact the module creators.{% endcomment %}
    },
    "2": {
      "name": "Custom gallery video detail with embedded testimonials",
      "type": "detail",
      "image": "",
      "enabled": true,
      "coming_soon": false,
      "dest": "layouts/modules/module_<module_vanity_id>",
      "files": [
        {
          "src": "detail/item",
          "dest": "layouts/modules/module_<module_vanity_id>"
        },
        {
          "src": "detail/wrapper",
          "dest": "layouts/modules/module_<module_vanity_id>"
        },
        {
          "src": "testimonials/list/wrapper", {% comment %}Note this is an example of an embedded layout. We're still inside the same layout folder as the other files, but add another folder to keep the embedded layout files distinct and organised.{% endcomment %}
          "dest": "layouts/modules/module_8" {% comment %}Note this is an example of an embedded layout. The destination folder is actually in a completely different module folder. However, the name of the layout will remain the same. E.g. If the module user installs a layout and calls it "Gallery 2", both the Gallery Layout and the embedded Testimonials layout will have the folder names "module_<module_vanity_id>/gallery-2" and "module_8/gallery-2" respectively. See the embedded layouts section for more tips.{% endcomment %}
{% endraw %}
        },
        {
          "src": "testimonials/list/item",
          "dest": "layouts/modules/module_8"
        }
      ],
      "sub_module": 2
    }
  }
}


```

#### Step 4 - Adding the Content to Layout Source Files <a href="#step-4-adding-the-content-to-layout-source-files" id="step-4-adding-the-content-to-layout-source-files"></a>

##### Adding Liquid to Layouts using the Raw Tag

In step 1, you created the folder structure for the layouts, but this section shows how you can format the layout code within each file.

It's up to you what kind of Liquid code to add to layouts, but there is one important rule:

Where your layout contains any Liquid code which you wish to render at runtime, you need to wrap it in the `raw` liquid tags, see [https://documentation.platformos.com/api-reference/liquid/introduction#raw](https://documentation.platformos.com/api-reference/liquid/introduction#raw). In almost all cases, you can just wrap this tag around your entire layout. Without this tag, Liquid will run at build-time while SiteBuilder is creating your layout, which would most likely mean the Liquid would be rendered to nothing, or to something unexpected.

Important! Once you put raw tags into a layout, the Siteglide-CLI will ignore any errors in your code. So if you have an unexplained file in your layout that is not installing properly, try taking out the raw tags, syncing, then putting them back in. You may discover the error in the CLI.

If you're using VSCode, you can use find & replace to add raw tags to all files in a folder.

<figure><img src="https://res.cloudinary.com/sitegurus/image/upload/v1667563298/modules/module_86/documentation/adding_raw_tags.png" alt="VSCode regex find and replace ((.|\n)\*) with $1."><figcaption></figcaption></figure>

##### Pagination

Layouts should aim to be self-contained. This often means that Siteglide's default pagination position is too low and it's better to move the pagination higher up in the DOM (so that it has the correct padding after it.)

The recommendation is that you use the following code to position custom pagination:

```liquid
{% raw %}
{%- if _show_pagination == 'false' and pagination_layout != blank and pagination_layout != "default" -%}
  {%- include 'modules/siteglide_system/get/get_pagination', pagination_layout: _pagination_layout -%}
{%- endif -%}
{% endraw %}

```

To use it, the module\_user must both set `show_pagination: 'false'` on the include tag to remove the default pagination and then set a custom `pagination_layout`.

Built-in module `module_s2` can be used to add new pagination layouts to a theme.

##### Adding Settings (Optional)

As well as this rule, there are also some helpful conventions which you can follow when writing layouts. One of these is Layout settings.

The main purpose of Layout settings is to gather together at the top of the file, variables which cannot be handled completely dynamically and require the module user to enter some input to make the layout work as expected. For example, if you've got a link from the layout to another page, there's no way of a layout knowing the context of the site and which URL to link to.

This adds convenience to the user; instead of searching through the layout to find the variables they'll almost certainly want to change, they can look at the top of the layout first.

Here is an example of settings being implemented in a SiteBuilder Layout:

```liquid
{% raw %}
{% comment %} ---Settings--- {% endcomment %}
{% comment %}------ Login URL ------- String for the URL of your login page. {% endcomment %}
{% assign login_url = "/login" %}
{% comment %} ---End Settings--- {% endcomment %}
{% endraw %}

```

Notes:

1. Where a layout contains multiple files, the settings block should be placed at the top (under the tag) of the first file that will be outputted, which would normally be called the `wrapper`.
2. The entire settings block should be wrapped between two Liquid comments \`

\` and \`\`. 3. Each setting should be preceded by another comment with the name of the setting (6 dashes before and after), then a comment to explain the purpose of the setting. 4. Finally, each setting should contain a Liquid tag to set the variable. This variable's value should be read where needed within the rest of the file and within any other files in the layout which may need to use it. Due to Liquid inheritance, the variable will be available for any files included by the file that contains the setting block.

These conventions help to keep the settings consistent and readable for the module user (and the developer). Following them now will also allow your layouts to take advantage of future improvements when settings are further integrated into the SiteBuilder UI. Watch this space!

##### Sitebuilder Component IDs (optional)

Another convention we use when building layouts with JavaScript interactivity is the Sitebuilder component ID.

Where JavaScript needs to be given an element query selector in order to make that element interactive, you can normally pass it an element ID. However, you need to think about what would happen if the user added more than one similar (or the same) layout to the page.

Using the following code, we dynamically generate a unique ID for each layout that needs one. Since this is generated by Liquid at runtime, it doesn't matter if the same layout is used twice- the ID will still be unique. This is by convention generated straight after the settings.

```liquid
{% raw %}
{% comment %}---Settings---{% endcomment %}
{% comment %}---End Settings---{% endcomment %}
{% capture sitebuilder_uniq_component_id %}sitegurus_component_{% increment sitegurus_gen_uniq_component_id %}{% endcapture %}
{% endraw %}
<div id="slider_{{sitebuilder_uniq_component_id}}" class="js-slider"></div>
<div id="toggle_{{sitebuilder_uniq_component_id}}" class="js-toggle-button"></div>
<script>
  (function () {
    var a = document.querySelector('#slider_{{sitebuilder_uniq_component_id}}')
    var b = document.querySelector('#toggle_{{sitebuilder_uniq_component_id}}')
    // Run JS for initialising your components here.
  })();
</script>

```

Instead of including JS within the layout to capture these variables, it is possible to store the ID in data-attributes and target all the elements at once. This allows your JS to run asynchronously for better performance.

_Liquid_

```liquid
{% raw %}
{% comment %}---Settings---{% endcomment %}
{% comment %}---End Settings---{% endcomment %}
{% capture sitebuilder_uniq_component_id %}sitegurus_component_{% increment sitegurus_gen_uniq_component_id %}{% endcapture %}
{% endraw %}
<div data-slider="{{sitebuilder_uniq_component_id}}" class="js-slider"></div>

```

_JS_

```javascript
var sliders = document.querySelectorAll('[data-slider]');
sliders.forEach(
  function(slider) {
    var id = slider.dataset.slider;
    //Run JS to intialise the slider here.
  }
)
```

Using these conventions from the beginning should help you avoid bugs arising from conflicting IDs.

##### Nesting or embedding layouts (optional)

In the previous sections, the documentation alluded to nested or embedded layouts. This is an advanced feature of SiteBuilder which allows layouts from one module to embed within them modules from another.

Look back at the example for step 1 to see the file-structure for embedding a testimonials layout within a module layout (the layout folder is "2").

```bash
|               |        └───testimonials
|               |               └───list
|               |                       item.liquid
│               |                       wrapper.liquid
```

Look back at step 2 to see how the embedded layout is configured.

You also need finally in your Layout code to add the Liquid tag which will include the embedded layout itself.

The main limitation of embedded layouts, is that it's not always possible to know all of the information you'd need to embed a layout successfully. This will depend on context on a case-by-case basis.

One piece of information which you will have which might surprise you however, is the name of the layout. Due to the way we set up the layout config, the embedded layout will have the same layout name as the parent layout (they are installed at the same time!). This means whatever the module-user chooses to name the layout, you will be able to access it! Use the example below:

In this example, the layout\_config files array contains a file with the dest: `testimonials/list/wrapper`. Since list and wrapper are handled by Siteglide ( you need to add the `type: "list"` parameter though), only the "testimonials" part of the path is needed. Any other optional additional folders should also be added to the capture tag. We also prepend the name of the current parent layout. The embedded layout will have been created at the same time, with the same name, so we can reference it using the inherited `{{layout}}` variable.

```liquid
{% raw %}
{% capture testimonials_layout -%}{{layout}}/testimonials{%- endcapture %}
{% include 'module', id: '8', layout: testimonials_layout, type: 'list', item_ids: item_ids, _top_model: nil %}
{% endraw %}

```

_Resetting `_top_model` for consistent layout paths_

The unusual looking `_top_model: nil` parameter is useful for making sure the nested Siteglide tag looks in a consistent location for layouts. Due to legacy reasons, where an \`

\` tag is nested inside another, Siteglide will look inside the parent module folder for all child module layouts. This is inconsistent with other tags, for example secure zones where Siteglide will look in the child module's folder, so it's easier to use this parameter to tell Siteglide to ignore the parent layout and look in the module folder for the current module. That way you can always store layouts safely accordingly to their own functionality rather than the functionality of the layout they're nested inside.

_Preserving the Layout Variable across multiple layers of Liquid_

If you're nesting layouts in more than two layers, you may experience a difficulty where the first layer redefines the `layout` variable and it's not accessible in layers below. In this case, at the top layer, you should assign a new variable on the very top layer which will reliably not be overwritten:

```liquid
{% raw %}
{% assign original_layout = _layout %}
{% endraw %}

```

_Datasources_

If you wish, you can also make this embedded layout into a datasource! Here we use one of the datasource fields in the parent layout to store Testimonial IDs we can use to filter by.

```liquid
{% raw %}
{% if this.properties['module_field_109_8'] != blank %}
  {% capture testimonials_layout -%}{{layout}}/testimonials{%- endcapture %}
  {% assign item_ids = this.properties['module_field_109_8'] | join: "," %}
  {% include 'module', id: '8', layout: testimonials_layout, type: 'list', item_ids: item_ids, datasource: 'true' %}
{% endif %}
{% endraw %}
```

##### Code Snippets

If your layout uses a significant amount of Liquid so it's not realy a static layout, but it doesn't rely on any specific Siteglide Module or WebApp database table, you may wish to install it as a `code_snippet`.

To make a layout install as a code snippet, set the `"install_type": "code_snippet"` in the layout_config file. It's only possible for these layouts to have a single file. It doesn't matter what you name the file, but the src setting in layout_config must match that name.

##### WebApp Layouts

WebApp Layouts work exaclty the same way as Module Layouts, but with some key differences.

WebApp Layouts can output standard fields like categories as normal, however, most of the fields you'll want to output will be custom fields.

To make field mapping possible, you need to first figure out the field slots you want in the item.liquid layout file, by adding Liquid code like so:

```liquid
{% raw %}
{{field_map['Example Field Slot']}}
{% endraw %}
```

This field slot can represent any potential webapp custom field. The module user will select which webapp custom field they think will best fit, based on the name and recommended type, so choose names carefully.

Then, you need to add an object to the layout_config.liquid JSON, to define these field slots (note instead of module_3 etc, the folder should be webapp, but it sits alongside the other module folders):


```liquid
{% raw %}
{
  "webapp": {
    "5": {
      "name": "Card with link",
      "image": "https://res.cloudinary.com/sitegurus/image/upload/f_auto/v1678980100/modules/module_86/admin/libraries/5/WebApps/webapp-card-1.png",
      "dest": "layouts/webapps",
      "files": [
        {
          "src": "list/wrapper",
          "dest": "layouts/webapps"
        },
        {
          "src": "list/item",
          "dest": "layouts/webapps"
        }
      ],
      "type": "list",
      "tags": [
        "card"
      ],
      "field_mapping": { {% comment %}{Object. Required (for WebApps). Defines field slots for mapping.{% endcomment %}
        "Title": { {% comment %}Object. Required. Human-readable name of the field slot. This must match the reference in the Liquid file itself.{% endcomment %}
          "required": true, {% comment %}Boolean. For very important fields which the Layout would not work without, set this to true. Otherwise, set to false and add logic within the layout to hide an element if the field is null. The user should expect the layout to work out of the box, so long as they mapped all required fields.{% endcomment %}
          "recommended_types": [ "input_text","input_radio","select" ] {% comment %}Array of Strings. Required. To help the user find a suitable field for this slot quickly, you must add an array of field types as defined by Siteglide. The UI will move fields of this type to the top of the options during field mapping. {% endcomment %}
        },
        "Card Icon": {
          "recommended_types": ["image", "file"]
        },
        "Description Short": {
          "recommended_types": ["textarea", "input_text"]
        },
        "Button Icon": {
          "recommended_types": ["image", "file"]
        }
      },
      "sub_module": 1
    }
  }
}
{% endraw %}
```

The installation process will automatically add Liquid code to the top of your layouts. One snippet of code defines the user's chosen field mapping as JSON, where the keys are the slot names and the values are the Siteglide WebApp field IDs. The second snippet of code takes values from this and assigns them to the headings in the field_map object.

###### WebApp Layout File Structure

WebApp List Layouts must have a wrapper and an item file.

```json
"files": [
  {
    "src": "list/wrapper",
    "dest": "layouts/webapps"
  },
  {
    "src": "list/item",
    "dest": "layouts/webapps"
  }
],
```

WebApp Detail Layouts must have an item file. Since WebApp Detail views don't allow you to set the use_wrapper parameter, you need to write the layout without a wrapper. You also must set the install_type to webapp_detail which makes sure the file is renamed as the layout name given by the user.

```json
"files": [
  {
    "src": "list/item",
    "dest": "layouts/webapps",
    "install_type": "webapp_detail"
  }
],
```

##### Front-End Access to Module / WebApp Config Data

{% function table_config = "modules/module_86/front_end/functions/v1/get_table_config", model: _model, id: id, field_headings: field_headings %}

You can use the table_config function to fetch additional information about the layout which you may wish to output, e.g. the name of the WebApp and the names of the fields.

##### Troubleshooting Layouts

1. Check the JSON for each config file validates to correct JSON when you "include" and "output" the file on a test page with Liquid. A comma in the wrong place can invalidate your JSON and cause errors.
2. If there are missing files in your layout, try temporarily removing the raw tags from that file and syncing with Siteglide-CLI. The raw tags may be causing a syntax erro to go undiscovered.
3. Check that the raw tags are present in each file.
4. Check that the number of files listed in the layout\_config file matches, or is less than, the number of files in your layout's file structure.
5. When your layout is working, but you're working on improving the layout's functionality and styling, try using PageBuilder to quickly generate multiple test layouts, and use the view page feature to view. When done, close the modal with the top-righthand corner close button and run the test again when you're readyby giving the page a new name.
