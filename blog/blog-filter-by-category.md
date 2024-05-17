# Blog Filter by Category

This Navigation Option can be used in combination with other Navigation Options.

![](https://downloads.intercomcdn.com/i/o/167279170/60d8c5aaf4a5c32ae4069bd1/image.png)

## Introduction

This Article will show:

* How to include this Navigation Option when including the Blog
* The Default Layouts with explanation
* How to give the User Feedback on the type of results they are seeing.

## Add "use\_adv\_search" parameter to include for Blog List View

The "use\_adv\_search" parameter is needed to allow filtering from the URL to apply to your Blog Posts, this can be added to the include for Blog List like so:

```liquid
{%- include 'module'
    id: '3'
    layout: 'default'
    per_page: '20'
    show_pagination: 'true'
    sort_type: 'created_at'
    sort_order: 'desc'
    use_adv_search: 'true' 
-%}

```

## To Include this Option

Include the following liquid to dynamically get a list of available Blog Categories for the User to select:

```liquid
{%- include 'modules/siteglide_system/get/get_categories'
    categories_layout: 'default/categories'
    categories_layout_type: 'sidebar' 
-%}

```

The parameters refers to layout which will be used to display the Category links. \<code>categories\_layout\</code>should be the root layout folder where your blog layout is contained.

The `category_layout_type` is the sub-folder where the wrapper and item files are stored for filtering the blog list by category. The `category_layout_type` exists because some blog layouts may have a different partial layout for Categories within a Blog preview, footer or sidebar.

## Default Layout Examples with Explanation

### wrapper.liquid

```liquid
<div class="row no-gutters">
  <div class="col-12">
    <h2>Categories</h2>
    <ul>
      {% raw %}
{%- include 'modules/siteglide_system/get/get_items', item_layout: 'item' -%}
{% endraw %}
    </ul>
  </div>
</div>

```

### item.liquid

```liquid
<li>
    <a href="{{context.location.pathname}}?category={{this.id}}">{{this.properties.name}}</a>
</li>

```

The link should be the slug of your Blog List view followed by `?category={{this.id}}`. Siteglide will be able to read the Category id from the URL and populate the List View on refresh. In this example we use the context object to automatically get the slug of the current Blog Page.

## User Feedback

You may wish to give the User some feedback about the current filter/ search terms that are applied on the Blog list page. For Categories, you can use \<code>context.exports\</code> object to get the name of the category you are filtering by:

```liquid
{% raw %}
{% if context.params.category %}
  Posts about {{context.exports.categories.data[context.params.category].name}}
{% endif %}
{% endraw %}
```
