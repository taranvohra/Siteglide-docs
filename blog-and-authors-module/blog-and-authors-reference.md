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

Include the Archive Layout (included in the default layout, or make your own)

<pre class="language-liquid"><code class="lang-liquid"><strong>{%- include 'modules/siteglide_blog/get/get_blog_archive'
</strong>    archive_layout: "default/archive"
    archive_layout_type: "sidebar_years_and_date_search" 
-%}
</code></pre>

Include: Search Blog Between Two Dates (included in the default layout, or make your own)

```liquid
{%- include 'modules/siteglide_blog/get/get_blog_archive'
    archive_layout: "default/archive"
    archive_layout_type: "sidebar_years_and_date_search" 
-%}
```

Advanced Filtering

```
{%- include 'module'
    id: '3'
    layout: 'default'
    use_adv_search: 'true' 
-%}
```
