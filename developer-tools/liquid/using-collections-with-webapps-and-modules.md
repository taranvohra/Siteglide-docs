---
title: Using WebApp Collections- Tutorial
slug: g1T0-
createdAt: 2021-02-17T12:53:22.000Z
updatedAt: 2023-04-11T11:05:58.000Z
---

# Using Collections with WebApps and Modules

Take control over your WebApp Layouts by exposing the Data and making your own For Loop with Liquid

## Prerequisites

In this Tutorial, we'll be using dot notation, so if you're not familiar with it, you may want to brush up here:

* [Getting Started with Dot Notation](https://developers.siteglide.com/tutorial)
* [Advanced Dot Notation - Arrays and Key Maps](https://developers.siteglide.com/advanced-arrays-and-key-maps-tutorial)

You'll also need to be familiar with WebApps:

* [Creating and Editing WebApps](https://help.siteglide.com/article/126-webapps-getting-started#2-creating-and-editing-items)
* [WebApp List Layouts](https://developers.siteglide.com/webapp-list-layouts)
* [WebApp Detail Layouts](https://developers.siteglide.com/webapp-detail-layouts)

## Introduction

By default in Siteglide, when you include a WebApp, we query the database and loop over the items for you. We take the data inside the loop and assign it to a variable called `this` which holds dynamic data about the current item. In certain situations, you may want to do something different, so we have provided the optional parameter `collection`.

Setting collection to `'true'` makes the data from the behind-the-scenes query available to you directly, without a layout.

## Using Collection

In the following example, we show the difference between a WebApp list which does use Collection and one which doesn't:

```liquid
{% raw %}
<div class="container">

  <h2>Here we have an ordinary WebApp</h2>
  {%- include 'webapp'
      id: '1'
      layout: 'portfolio_2'
      per_page: '20'
      show_pagination: 'true'
      sort_type: 'properties.name'
      sort_order: 'asc' 
  -%}
  
  <h2>Here we have a WebApp Collection</h2>
  {%- include 'webapp'
      id: '1'
      layout: 'portfolio_2'
      per_page: '20'
      show_pagination: 'true'
      sort_type: 'properties.name'
      sort_order: 'asc'
      collection: 'true' 
  -%}
  
  {{context.exports.webapp_1.data | json}}
  
</div>
{% endraw %}
```

This outputs:

<!-- ![](https://downloads.intercomcdn.com/i/o/170957349/28a44da8e57c6c597c0fa956/image.png) -->

To break it down further, setting collection to `true` exports the data to `{{context.exports}}` Under that, you can access it by the id of the WebApp in the original `include` tag. In this example, it's `1` so we can access `{{context.exports.webapp_1.data | json}}`.

You can then use dot notation to access the data as you wish.

## A Possible Use Case

When would you use collection?

Well some people will prefer to always use collection, others will prefer to use layouts. One possible use-case where Collection works better though is if you want to display the same WebApp twice on the Page but differently each time.

For example, what if you wanted to display the first item largely at the top, then display other items in smaller cards below?

You could use the \`

\` tag twice to achieve this, with different Layouts each time, but this would have a negative effect on performance. This would slow the Page down, because we would be querying the database behind the scenes twice (once for every time you include the tag).

Alternatively, you could include the webapp just once as a collection, then use Liquid to display the items you want in the way you want:

```liquid
{% raw %}
<div class="container">
  {%- include 'webapp'
      id: '1'
      per_page: '6'
      sort_type: 'properties.name'
      sort_order: 'asc'
      collection: 'true' 
  -%}
  <h2>Featured Item</h2>
  {% assign this = context.exports.webapp_1.data.result.items[0] %}
  {{this.Title}}
  <h2>Other Items</h2>
  {% for this in context.exports.webapp_1.data.result.items %}
    {{this.Title}}
  {% endfor %}
</div>
{% endraw %}
```

This outputs:

<!-- ![](https://downloads.intercomcdn.com/i/o/170961170/0dbe4c889cb38d1ea6abd650/image.png) -->

Great! Only one query needed behind the scenes and we've nearly met the objective, but there's one problem. The item "A Special Guest Appearance" has been included twice!

## Advanced Looping

We can use the `offset` parameter on our loop tag to start the loop at a different index. Let's skip the first index when we loop, as this item has already been displayed.

```liquid
{% raw %}
<div class="container">

  {%- include 'webapp'
      id: '1'
      per_page: '6'
      sort_type: 'properties.name'
      sort_order: 'asc'
      collection: 'true' 
  -%}

  <h2>Featured Item</h2>
  
  
{% raw %}
{% assign this = context.exports.webapp_1.data.result.items[0] %}
  {{this.Title}}
  
  <h2>Other Items</h2>
  
  {% for this in context.exports.webapp_1.data.result.items offset: 1 %}
    {{this.Title}}
  {% endfor %}
{% endraw %}
  
</div>


{% endraw %}
```

You can do a lot with loops. Offset is just one of your options. Head to the pOS documentation to learn more about loops in Liquid: [https://documentation.platformos.com/api-reference/liquid/loops](https://documentation.platformos.com/api-reference/liquid/loops)

## Using Layouts with Collections

Hang on, wasn't the point of Collections to avoid Layouts? Not quite! The idea was to give you control over the loop- layouts are still possible. I can still include my `portfolio_2` layout, but I need to work out its path from SITE MANAGER / Code Editor in Admin.

<!-- ![](https://downloads.intercomcdn.com/i/o/170964104/c1f3d4727c38bf6864313c84/image.png) -->

I can now include the Layout at this Path: \`

\`

The Layout is expecting an object called `this` containing the data, but as in the example above we already assigned variables called `this` containing the right data, the Layout works without further modification:

<!-- ![](https://downloads.intercomcdn.com/i/o/170964628/57c17615b319870fae403c96/image.png) -->
