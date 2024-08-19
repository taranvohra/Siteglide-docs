# ℹ️ Layouts

## Outputting List Views on the Front-End

Like with other Modules, you will use a Liquid Tag to output a list of Module Items on a Page, Page Template, Email or Partial Liquid File of your choice.

```html
{%- include 'module'
    id: '17'
    layout: 'default'
    per_page: '20'
    show_pagination: 'true'
    sort_type: 'properties.name'
    sort_order: 'asc' 
-%}
```

You can use the following parameters:

* `ID` - This must be set to `17` as this refers to the ID of the Media Downloads Module
* `layout` - The Layout Folder containing the List Layout
* `per_page` - How many Items should be outputted on each Page. If more Items are available than this, Pagination controls will display.
* `show_pagination` - if set to `'true'` , pagination controls will display in the default position when more than one Page of results is available.
* `sort_type` - The field you'd like to sort by e.g. "properties.name", or "created\_at"
* `sort_order` - Choose `asc` for ascending values or `desc` for descending
* `category_ids` - Pass in a string of comma-separated IDs of Categories to filter the List so only Items assigned to those Categories can be displayed.
* `item_ids` - Control exactly which Items can be displayed by passing in a string of comma-separated IDs. You can find the Items' IDs in the Admin.
* `expiry` - The number of seconds that the link is valid for after the page has finished loading. Default is 600 (10 minutes). Note this is different from
* `expiry_date`, see Available Fields.

## Media Downloads Layouts

There will be a default layout once you install the module but you can create your own.

### Creating a Layout File

Layouts can be created at the following path: `layouts/modules/module_17/my_layout_name/`

### Developing a List Layout

You'll need to create a `list` folder in your layout folder and fill it with the following files:

* wrapper.liquid
* item.liquid

Your `wrapper.liquid` file should contain the following Liquid which determines where the list of Items will go:

```html
{%- include 'modules/siteglide_media_downloads/get/get_items'
    item_layout: 'item' 
-%}
```
