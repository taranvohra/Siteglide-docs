# 🔧 Tags for Blog & Authors

### General Module Reference

This reference gives you a quick guide to all the code you can use with the Blog, but some features are available to all Modules, see more:

{% content-ref url="../../../developer-tools/marketplace/building-for-marketplace/modules-reference.md" %}
[modules-reference.md](../../../developer-tools/marketplace/building-for-marketplace/modules-reference.md)
{% endcontent-ref %}

### Blog Fields

The Blog uses standard module fields as well as it's own core fields:

{% content-ref url="../../../developer-tools/marketplace/building-for-marketplace/modules-reference.md" %}
[modules-reference.md](../../../developer-tools/marketplace/building-for-marketplace/modules-reference.md)
{% endcontent-ref %}

| **Field Name**                                                                                                                                                      | **Liquid Tag**                  | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Title                                                                                                                                                               | \{{ this\['Title'] \}}          | title of the Blog Post                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Subtitle                                                                                                                                                            | \{{ this\['Subtitle'] \}}       | subtitle of the Blog Post                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Description                                                                                                                                                         | \{{ this\['Description'] \}}    | list description of the Blog Post                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Author - Syntax type 1 (Requires Authors Module)                                                                                                                    |                                 | data source of author. Parameters: author\_layout: path to the folder containing author layouts. author\_layout\_type: name of author layout folder (containing wrapper and item files). author\_id: Unique ID of the author for this item- can be dynamically passed in with `this['Author']`.                                                                                                                                                       |
| Author - Syntax type 2 (Requires Authors Module) - The benefit of this syntax is that it should be more consistent with how other Modules are outputted on the Page |                                 | data source of author. Parameters: layout path to the folder containing author layouts within the blog module. type- name of the layout folder containing wrapper and item Liquid layout files. datasource - should be set to true to indicate that this module is a sub-module placed inside another module Layout. item\_ids - indicates the unique ids of the Author items you want to display- can be dynamically passed in with `this['Author']` |
| Main Image                                                                                                                                                          | \{{ this\['Main Image'] \}}     | main image of the Blog Post                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Main Image Alt                                                                                                                                                      | \{{ this\['Main Image Alt'] \}} | main image alt tag of the Blog Post                                                                                                                                                                                                                                                                                                                                                                                                                   |
| List Image                                                                                                                                                          | \{{ this\['List Image'] \}}     | list image of the Blog Post                                                                                                                                                                                                                                                                                                                                                                                                                           |
| List Image Alt                                                                                                                                                      | \{{ this\['List Image Alt'] \}} | list image alt tag of the Blog Post                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Content                                                                                                                                                             | \{{ this\['Content'] \}}        | main content of the Blog Post                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Category Array                                                                                                                                                      | \{{ this.category\_array \}}    | outputs comma-separated list of IDs for Categories this item belongs to.                                                                                                                                                                                                                                                                                                                                                                              |

### Blog Navigation & Filtering

As always, to use filtering on an included module layout, add the `use_adv_search` parameter. To allow searching, add `use_search`. These settings instruct this component to _watch_ the URL for changes in URL parameters and will adjust results accordingly when the URL changes; forms, anchors or JS (for example, the SiteBuilder Live Updates API) can be used to change the URL and apply these.

```
{%- include 'module'
    id: '3',
    layout: 'default',
    use_search: 'true',
    use_adv_search: 'true',
-%}
```

#### By Date

(Requires `use_adv_search`)

Include the Archive Layout (included in the default layout, or make your own) to list all available years or months containing blog posts.

<pre class="language-liquid"><code class="lang-liquid"><strong>{%- include 'modules/siteglide_blog/get/get_blog_archive'
</strong>    archive_layout: "default/archive"
    archive_layout_type: "sidebar_years_and_date_search" 
-%}
</code></pre>

Inside an archive layout, you have access to the following variables which can be looped over to find the months in which at least one blog post was published: `blog_archive_years` and `months_by_year`

To apply filters, the URL must be given the following parameters:

* A combination of `range_gt`, `range_gte`, `range_lt`, `range_lte` to set the date range to "range greater than", "range greater than or equal to" etc., in the format: %Y-%m-%d.
* `range_type` - an optional convention, you can set this to e.g. "between" or "month" so that you can interpret the URL accordingly when you arrive.
* `range_field` - is used in Events module, but not needed here. Default is to use release date for range field

#### By Category

(Requires `use_adv_search`)

Include the following liquid to dynamically get a list of available Blog Categories for the User to select:

```liquid
{%- include 'modules/siteglide_system/get/get_categories'
    categories_layout: 'default/categories'
    categories_layout_type: 'sidebar' 
-%}
```

To apply filters, the URL must be given the following parameters:

* category - to be given the value of one or more category IDs to filter by, comma separated.

#### By Author

(Requires `use_adv_search`)

```liquid
{%- include 'modules/siteglide_authors/get/get_authors'
    author_layout: 'default/author'
    author_layout_type: 'sidebar'
    author_field: 'module_field_3_4' 
-%}
```

To apply filters, the URL must be given the following parameters:

* `module_field_3_4` - set to a valid Author's module item ID
* `author_name` - an optional convention making it easier to display this when arriving at the list.

#### Keyword Search

Link to the page with a `keyword` parameter in the URL to perform a search. (Requires `use_search`)

```
<form action="{{context.location.pathname}}">
  <input type="search" placeholder="enter search term..." name="keyword">
</form> 
```

### Authors

#### Fields:

Authors uses standard module fields as well as it's own core fields:

{% content-ref url="../../../developer-tools/marketplace/building-for-marketplace/modules-reference.md" %}
[modules-reference.md](../../../developer-tools/marketplace/building-for-marketplace/modules-reference.md)
{% endcontent-ref %}

<table data-header-hidden data-full-width="true"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Field Name</strong></td><td><strong>Liquid Tag</strong></td><td><strong>Description</strong></td></tr><tr><td>Title</td><td>{{ this['Title'] }}</td><td>name of the Author</td></tr><tr><td>Subtitle</td><td>{{ this['Subtitle'] }}</td><td>Job title or other short text about the Author</td></tr><tr><td>Description</td><td>{{ this['Description'] }}</td><td>Description of the Author</td></tr><tr><td>Image</td><td>{{ this['Image'] | asset_url }}</td><td>Image of the Author</td></tr><tr><td>Image Alt</td><td>{{ this['Image Alt'] }}</td><td>Image alt of the Author image</td></tr><tr><td>Linkedin URL</td><td>{{ this['LinkedIn URL'] }}</td><td>Linkedin profile URL of the Author</td></tr><tr><td>Facebook URL</td><td>{{ this['Facebook URL'] }}</td><td>Facebook profile URL of the Author</td></tr><tr><td>Twitter URL</td><td>{{ this['Twitter URL'] }}</td><td>Twitter profile URL of the Author</td></tr><tr><td>Instagram URL</td><td>{{ this['Instagram URL'] }}</td><td>Instagram profile URL of the Author</td></tr><tr><td>Pinterest URL</td><td>{{ this['Pinterest URL'] }}</td><td>Pinterest profile URL of the Author</td></tr></tbody></table>
