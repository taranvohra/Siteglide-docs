# 👀 Blog & Authors Reference

### General Module Reference

This reference gives you a quick guide to all the code you can use with the Blog, but some features are available to all Modules, see more:

{% content-ref url="../siteglide-modules-marketplace/modules-reference.md" %}
[modules-reference.md](../siteglide-modules-marketplace/modules-reference.md)
{% endcontent-ref %}

### Navigation & Filtering

As always, to use filtering on an included module layout, add the `use_adv_search` parameter. To allow searching, add `use_search`.

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

Include the Archive Layout (included in the default layout, or make your own)

<pre class="language-liquid"><code class="lang-liquid"><strong>{%- include 'modules/siteglide_blog/get/get_blog_archive'
</strong>    archive_layout: "default/archive"
    archive_layout_type: "sidebar_years_and_date_search" 
-%}
</code></pre>

#### By Category

(Requires `use_adv_search`)

Include the following liquid to dynamically get a list of available Blog Categories for the User to select:

```liquid
{%- include 'modules/siteglide_system/get/get_categories'
    categories_layout: 'default/categories'
    categories_layout_type: 'sidebar' 
-%}
```

#### By Author

&#x20;(Requires `use_adv_search`)

```liquid
{%- include 'modules/siteglide_authors/get/get_authors'
    author_layout: 'default/author'
    author_layout_type: 'sidebar'
    author_field: 'module_field_3_4' 
-%}
```

#### Keyword Search

Link to the page with a keyword parameter in the URL to perform a search. (Requires `use_search`)

```
<form action="{{context.location.pathname}}">
  <input type="search" placeholder="enter search term..." name="keyword">
</form> 
```
