# Category Detail Layouts

Category Detail Pages give you additional features including Breadcrumbs, Parent Category Lists, Child Category Lists and more.

## Introduction

In this set of Articles, we'll show you the Liquid syntax needed to get the most out of [Categories](https://help.siteglide.com/article/123-categories-getting-started) on the Front End. Once you have enabled a Detail Page for a Category, you can output any of the following on your Detail Layout:

## Breadcrumbs

Output breadcrumb of Categories to the current Category page using the defined layout:`<div data-gb-custom-block data-tag="-" data-0='category_breadcrumbs' data-1=', layout: ' data-2='breadcrumb'></div>`

## Parent Category List

Output parent Categories using the defined layout: `<div data-gb-custom-block data-tag="-" data-0='category_parent' data-1=', layout: ' data-2='parent'></div>`

## Child Category List

Output child Categories using the defined layout: `<div data-gb-custom-block data-tag="-" data-0='category_children' data-1=', layout: ' data-2='children'></div>`

## Items in this Category

Output all items categorised to the current Category Page using the defined layout: `<div data-gb-custom-block data-tag="-" data-0='category_items' data-1=', layout: ' data-2='items'></div>`&#x20;

Note that this will only output items in this specific Category. To output all items that belong to sub-Categories, then add another parameter of `show_all_sub_items: 'true'`.

## WebApp, Module and Products in this Category

You can use the Category ID `{{this.id}}` to filter WebApp, Module or Product Lists and display the Items with this Category assigned (and those belonging to Categories which are children of this Category).

We'll include some examples here of how the `{{this.id}}` variable can be used specifically on the Category Detail Page to filter by that Detail Page's Category dynamically:[ Learn more about filtering WebApps and Modules by Category](https://developers.siteglide.com/filtering-webapps-and-modules-by-categories)

### Products

For example, the following code will output Products on the Category Detail Page, filtered by that Category:

```liquid
{%- include 'ecommerce/products'
    layout: "my_layout"
    category_ids: this.id
    type: 'list' 
-%}
```

### WebApps

Change the ID to fetch different WebApps.

```liquid
{%- include 'webapp'
    id: '1'
    layout: "my_layout"
    category_ids: this.id
    type: 'list' 
-%}
```

### Modules

Module 3 refers to the Blog; you can change the ID to fetch different Modules.

```liquid
{%- include 'module'
    id: '3'
    layout: "my_layout"
    category_ids: this.id
    type: 'list' 
-%}
```

#### Default Fields

The following tags are available within the advanced category layouts:

| **Field Name** | **Liquid Tag**         | **Description**      |
| -------------- | ---------------------- | -------------------- |
| Category Name  | `{{ this.name }}`      | Name of the category |
| Category URL   | `{{ this.full_slug }}` | URL of the category  |
| Category ID    | `{{ this.id }}`        | ID of the cateogory  |

## Folder Structure

Category layouts are stored in the following folder structure, which you can view via Code Editor: `layouts/categories/`

Within this folder you will find the following:

* `detail/`- detail layouts contain the code displayed on category pages
  * `default.liquid` - the default detail layout for categories
* `list/` - list layouts allow you to customise how categories are displayed on category detail pages
  * `breadcrumb.liquid` - allows you to customise how categories are displayed within breadcrumbs on the current category detail page
  * `children.liquid` - allows you to customise how child categories are displayed on the current category detail page
  * `items.liquid` - allows you to customise how items that are categorised to the current category are displayed
  * `parent.liquid` - allows you to customise how parent categories are displayed on the current category detail page
