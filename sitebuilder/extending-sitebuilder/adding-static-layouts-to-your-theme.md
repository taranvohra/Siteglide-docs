# ℹ️ Adding Static Layouts to your Theme

This documentation is aimed at those following the [theme-creator](/sitebuilder/extending-sitebuilder/creating-sitebuilder-themes.md) route. It's not currently supported to include static layouts within the module-creator route.

Static layouts are HTML layouts which can be included in a theme. They won't directly interface with the database in the same way as a dynamic layout and are likely to have their content edited by the module-user, either in the code, or in the Siteglide Admin's Studio tab.

#### Where does the user access static layouts? <a href="#where-does-the-user-access-static-layouts" id="where-does-the-user-access-static-layouts"></a>

1.  The Studio tab in Siteglide is one place that SiteBuilder static layouts will appear. They can be dragged and dropped into the page and edited there.

    SiteBuilder static layouts will only appear in the Studio tab if the theme to which they belong is attached to any installed Page Template on the site. It's not yet possible to only show static layouts which are an exact match to the current page's template, but we will implement this when we can.
2. PageBuilder will show static layouts as section blocks which can be added to the page within the SiteBuilder UI. These will only show for the currently selected theme.

#### Siteglide's Static Layouts Webhook <a href="#siteglides-static-layouts-webhook" id="siteglides-static-layouts-webhook"></a>

Siteglide will be publishing a webhook allowing any module to add static layouts to the Studio tab without going through SiteBuilder. SiteBuilder builds upon that API with behind-the-scenes code which merges all static layouts in the file structure and automatically builds their categories.

#### File Structure <a href="#file-structure" id="file-structure"></a>

Under your theme folder, you'll need to create folders for each category of Static Layouts. The folder name will be capitalised and its underscores will be replaced by spaces within the UI e.g. "call\_to\_action" becomes "Call To Action".

Within each folder, each static layout gets its own file. The name of this file should be a number, which relates to the layout's ID in the `static_config` file, see next step.

```bash
└───modules
    └───module_<module_vanity_id>
        └───private
            └───views
                └───partials
                    └───sitebuilder<secret_key_preceded_by_underscore>
                        └───theme_<module_vanity_id>
                            |   static_config.liquid
                            └───static
                                ├───hero
                                │       1.liquid
                                │       2.liquid
                                │
                                └───features
                                        1.liquid
```

#### Adding Content to Files <a href="#adding-content-to-files" id="adding-content-to-files"></a>

At the present time, static content should be added inside each file as HTML only (including `<style>` or `<script>` tags if you like). It may be possible in future to include Liquid wrapped in raw tags, but it is not currently.

#### Static Config File <a href="#static-config-file" id="static-config-file"></a>

The `static_config.liquid` file should be added inside the theme folder in order to give SiteBuilder the metadata it needs to find your layouts and display them in either the Studio tab UI or the PageBuilder UI.

```liquid
{% raw %}
{
  "name": "Studio", 
{% comment %}String. Required. The name of your theme{% endcomment %}
  "id": "theme_<module_vanity_id>", {% comment %}String. Required. {% endcomment %}
  "categories": [
    {
      "name": "Hero", {% comment %}String. Required. The name of your category. Should match the folder name in the file structure, when converted to lowercase and spaces replaced with underscores.{% endcomment %}
      "id": "1", {% comment %}String. Required. Must be unique within categories. {% endcomment %}
      "layouts": [
        {
          "id": "1", {% comment %}String. Required. Must be unique within layouts and exactly match the filename of the layout it describes. {% endcomment %}
          "thumbnail": "https://res.cloudinary.com/...hero-1.png" {% comment %}String (absolute path image URL). Required. While the image will be thumbnail sized in Studio, it should be large enough to display correctly in PageBuilder, so should be at least 800px wide.{% endcomment %}
        },
        {
          "id": "2",
          "thumbnail": "https://res.cloudinary.com/...hero-2.png"
        }
      ]
    },
    {
      "name": "Feature",
      "id": "2",
      "layouts": [
        {
          "id": "1",
          "thumbnail": "https://res.cloudinary.com/...feature-1.png"
        }
      ]
    }
  ]
}
{% endraw %}
```
