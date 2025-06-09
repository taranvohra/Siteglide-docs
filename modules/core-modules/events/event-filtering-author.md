# ℹ️ Filter By Host (Author)

This Option Lets you filter Events by Host

## Prerequisites

* You have installed the Events Module
* You have installed the Authors Module
* You have added at least one Author as an Event Host

## Introduction

This article explains:

* How to include the Browse by Host (Author) Option when including a Blog List
* Default Layout Examples
* How to give feedback to the User about their results e.g. in the screenshot "Events hosted by Regina Alexander"

## Add "use\_adv\_search" parameter to include for Event List View

The "use\_adv\_search" parameter is needed to allow filtering from the URL to apply to your Event Items, this can be added to the include for Event List like so:

```liquid
{%- include 'module'
    id: '12'
    layout: 'default'
    per_page: '20'
    show_pagination: 'true'
    sort_type: 'created_at'
    sort_order: 'desc'
    use_adv_search: 'true' 
-%}


```

## To Include this Option

Include the following liquid to dynamically get a list of available Event Hosts for the User to select.

```liquid
{%- include 'modules/siteglide_authors/get/get_authors'
    author_layout: 'design_system/1/author'
    author_layout_type: 'list'
    author_field: 'module_field_12_4' 
-%}

```

The `author_field` will be `module_field_12_4` if you are using Siteglide's Authors Module. The layouts are structured in the same way as Category Layouts in the previous section.

## Default Layout Examples with Explanation

#### wrapper.liquid

```liquid
<div class="row no-gutters">
  <div class="col-12">
    <h2>Authors</h2>
    <ul>
      
{% raw %}
{%- include 'modules/siteglide_system/get/get_items', item_layout: 'item' -%}
{% endraw %}

    </ul>
  </div>
</div>


```

#### item.liquid

```liquid
<a
  class="authorAnchorSidebar" 
  href="{{context.location.pathname}}?module_field_12_4={{this.id}}&author_name={{this.name | url_encode}}"
>
{% raw %}
{% if this['Image'] -%}
    <img src="{% if this['Image'] contains 'http' -%}{{this['Image']}}{% else -%}{{this['Image'] | asset_url}}{% endif -%}" alt="{{this['Image Alt']}}">
  {% endif -%}
{% endraw %}

  <li>{{this['name']}}</li>
</a>


```

To filter the Blog List View, you need a link to the Blog List View slug, followed by `"?module_field_12_4={{this.id}}"`. Siteglide will be able to read the URL and filter the list.

## User Feedback - Displaying the currently applied filter

To make it easier to give feedback to the User, you can optionally include the Host's name in the URL:

```liquid
<a href="{{context.location.pathname}}?module_field_12_4={{this.id}}&host_name={{this.name | url_encode}}"></a>


```

On the List view, you can then include the following liquid to read the URL and decode the Author name you are currently filtering by:

```liquid
{% raw %}
{% if context.params.module_field_12_4 %}
  Events hosted by {{context.params.host_name | url_decode}}
{% endif %}
{% endraw %}
```
