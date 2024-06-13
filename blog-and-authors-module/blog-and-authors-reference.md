# 👀 Blog & Authors Reference

### General Module Reference

This reference gives you a quick guide to all the code you can use with the Blog, but some features are available to all Modules, see more:

{% content-ref url="../siteglide-modules-marketplace/modules-reference.md" %}
[modules-reference.md](../siteglide-modules-marketplace/modules-reference.md)
{% endcontent-ref %}

### Navigation & Filtering

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

* A combination of `range_gt`, `range_gte`, `range_lt`, `range_lte` to set the date range to "range greater than", "range greater than or equal to" etc., in the format: %Y-%m-%d.&#x20;
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

* category - to be given the value of one or more category IDs to filter by, comma separated.&#x20;

#### By Author

&#x20;(Requires `use_adv_search`)

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
