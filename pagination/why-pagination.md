# Pagination on Liquid Tags

## Introduction

Pagination refers to the process of assigning multiple pages to website content.

It is an important thing to consider when building a website, especially if you are fetching dynamic data from a database.

## Outputting Pagination

### Default Pagination

When you output a List Layout it will fetch results based on the parameters you've given it.&#x20;

The parameter `per_page` will decide how many items will initially display in the List. By default, this value will be 20.

&#x20;If more results were fetched than the `per_page` value,  Pagination controls will be added to allow the User to change page and view the rest of the data.

### How to remove Pagination Controls

Set the parameter  `show_pagination: 'false'` to remove pagination controls.

### How to move Pagination Controls

Firstly remove the default Pagination controls, as above.  Secondly, add the following Liquid where you'd like the controls to sit within your HTML structure: `<div data-gb-custom-block data-tag="-" data-0='modules/siteglide_system/get/get_pagination'></div>`

## Specifying a Pagination Layout

### Choose Your Layout File

Layouts for Pagination should be stored in Code Editor at the following path: `layouts/pagination/my_pagination_layout_name.liquid`

### Add a Pagination Layout to a WebApp or Module "include" tag

```liquid
{%- include 'webapp'
    id: '3'
    layout: 'default'
    per_page: '20'
    sort_type: 'properties.name'
    sort_order: 'asc'
    pagination_layout: 'my_pagination_layout_name'
-%}
```

### Add a Pagination Layout to a Pagination "include" tag

```liquid
{%- include 'modules/siteglide_system/get/get_pagination', pagination_layout: 'my_pagination_layout_name' -%}
```

## Customise the Layout

[Learn to create your own Pagination layout in Liquid](pagination-layouts.md)
