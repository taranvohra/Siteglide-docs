---
title: Slider
slug: jvkd-
createdAt: 2021-02-16T14:52:22.000Z
updatedAt: 2023-04-11T10:03:19.000Z
---

# 💻 Reference: Slider

Add images and content to your Slides in Admin and display on a Site either using our custom Layouts or creating your own

### Prerequisites

* You've Installed the Slider Module
* You've [added Slides in the Admin](https://help.siteglide.com/article/131-modules-getting-started#2-creating-and-editing-an-item)

### Introduction

Our Slider Module allows you to add images/content to Slides within the Admin, which can then be outputted as List Views either using our pre-built layouts or creating your own! We've chosen to use GlideJS for our layouts, but you can use any plugin you prefer.

Once you've installed the Slider Module on your Site, you'll be able to find Sliders in the left-hand menu under Modules/Slider. For a recap of how to install Modules on a Site, [see here](https://help.siteglide.com/article/131-modules-getting-started#2-installing-modules).

### Syntax

```liquid
{%- include 'module'
    id: '4'
    layout: 'default'
    per_page: '20'
    show_pagination: 'false'
    sort_type: 'properties.name'
    sort_order: 'asc' 
-%}

```

### Parameters

* `id` - the Module's ID
* `item_ids` - output one or more module items, comma seperated
* `category_ids` - output all items in one or more categories, comma seperated
* `layout` - default is /default/ - 'layout' values are relative to the folder: layouts/modules/Slider(module\_4)/\[layout name]
* `per_page` - defines the number of items outputted on the page
* `sort_type` - defines the type by which items are ordered
  * `properties.name` - name of the Module item (alphabetical)
  * `created_at` - date the Module item was created
  * `updated_at` - date the Module item was last edited
  * `properties.weighting` - weighting of the Module item
  * `properties.release_date` - date the item is set to be released
* `sort_order` - defines the order in which the type is sorted
  * `asc` - sort items in ascending order
  * `desc` - sort items in descending order
* `show_pagination` - this should be false
* `uniq_slider_id` - used when outputting multiple of the same layout on one page.

### Liquid Tags

| **Field Name**   | **Liquid Tag**                 | **Description**                  |
| ---------------- | ------------------------------ | -------------------------------- |
| Item Name        | \{{ this\['name'] \}}          | name of the Slide                |
| Weighting        | \{{ this\['weighting'] \}}     | weight of item, used for sorting |
| Release Date     | \{{ this\['release\_date'] \}} | release date of the item         |
| Expiry Date      | \{{ this\['expiry\_date'] \}}  | expiry date of the item          |
| Enabled          | \{{ this\['enabled'] \}}       | enable/disable the item          |
| Title            | \{{ this\['title'] \}}         | title of the Slide               |
| Subtitle         | \{{ this\['subtitle'] \}}      | subtitle of the Slide            |
| Description      | \{{ this\['description'] \}}   | description of the Slide         |
| Button Name      | \{{ this\['button name'] \}}   | button name                      |
| Button Link      | \{{ this\['button link'] \}}   | button link                      |
| Unique Slider ID | \{{ uniq\_slider\_id \}}       | slider's unique id               |

### Layouts

You can find all our Slider Layouts on [Layout Libary](https://studio.siteglide.com/layouts), to copy these onto your Site first create a folder in Code Editor, learn more [here](https://help.siteglide.com/article/214-code-editor-getting-started). Make sure your new Slider Layout has a List View folder within it, should look like this:

<!-- ![](https://downloads.intercomcdn.com/i/o/229068073/48df7e0feff380586d9f59ac/image.png) -->

Now copy the item/wrapper code into the List folder. Make sure to specify the Layout name when including the Module.

### Using the same Layout multiple times on one page

If you're using the same Slider Layout more then once on a Page you'll need to add a "Unique Slider ID" to your include:

```liquid
{% raw %}
{%- include 'module'
    id: '4'
    layout: 'default'
    per_page: '20'
    show_pagination: 'false'
    uniq_slider_id: '333' 
-%}
{% endraw %}
```

If this is added we'll run some extra logic on the layouts to ensure JS is mounted to the correct layout.

### GlideJS

We've chosen to build our Layouts using the GlideJS Slider plugin, if you would like to customize our layouts further we'd recommend reading [GlideJS' Documentation](https://glidejs.com/docs/). There are loads of different ways to build the Sliders- simply choose which type you suits you!
