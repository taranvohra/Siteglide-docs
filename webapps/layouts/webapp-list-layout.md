# ℹ️ WebApp List Layout

## Syntax

When placed onto a page or a template, this liquid displays the WebApp items using the defined list Layout.

```html
{%- include 'webapp'
    id: '3'
    layout: 'default'
    per_page: '20'
    sort_type: 'properties.name'
    sort_order: 'asc' 
-%}
```

## Parameters

| **Parameter**         | **Description**                                                                                                                                                                                                                                                                                             |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id                    | the WebApp's ID                                                                                                                                                                                                                                                                                             |
| item\_ids             | output one or more WebApp items. For multiple ids comma separate them like so: `item_ids: '17559,17546'`.                                                                                                                                                                                                   |
| category\_ids         | output all items in one or more categories. Comma separate category ids to filter by multiple categories e.g: `category_ids: '17559,17546'`.                                                                                                                                                                |
| show\_all\_sub\_items | default is `'true'` - When setting a category, this defines whether or not items should be shown if they are in sub-categories                                                                                                                                                                              |
| layout                | default is `'default'` - layout values are relative to the folder: `layouts/webapps/My WebApp (webapp_1)/[layout name]`                                                                                                                                                                                     |
| per\_page             | defines the number of items outputted on the page                                                                                                                                                                                                                                                           |
| show\_pagnation       | default is `'true'` - defines if items should be paginated when the per\_page is met.                                                                                                                                                                                                                       |
| ignore\_pagination    | default is `'false'` - defines if the output should ignore pagination in the URL. This is useful when outputting fixed WebApp/Module items in a sidebar, that don't need to be affected when moving page number.                                                                                            |
| sort\_type            | defines the type by which items are ordered. This can be a field (e.g. `sort_type: 'properties.name'` or `sort_type: 'properties.webapp_field_1_2'`) or you can choose to sort by your array of 'item\_ids' if you are outputting specific items (`sort_type: 'item_ids'`)                                  |
| sort\_order           | defines the order in which the type is sorted                                                                                                                                                                                                                                                               |
| collection            | default is `'false'` - If you set it as `collection: 'true'` then any layout is suppressed.                                                                                                                                                                                                                 |
| use\_wrapper          | default is `'false'` - If you set it as `use_wrapper: 'true'` then your layout will be `layouts/webapps/My WebApp (webapp_1)/[layout name]/list/wrapper` and the wrapper file needs to contains Liquid to output the items: `{%- include 'modules/siteglide_system/get/get_items', item_layout: 'item' -%}` |

## Sorting by Custom Fields

When sorting by Custom fields, you'll need to refer to the field by its `Custom Field ID`. e.g. to sort by the 2nd Custom Field created on `webapp_1`, you should set the Sort Type to: `sort_type: "properties.webapp_1_2"` We use this syntax to access the field directly in the database, in order to help increase Page Load performance.

Learn more about Custom Field IDs here: [Understanding Custom Field Names and IDs - and when to use them](../../developer-tools/configuration/custom_fields.md)

## Default Fields

| **Field Name** | **Liquid Tag**                 | **Description**                                 |
| -------------- | ------------------------------ | ----------------------------------------------- |
| Item Name      | \{{ this\['name'] \}}          | name of the FAQ                                 |
| Slug           | \{{ this\['full\_slug'] \}}    | url of the current item, relative to the layout |
| Weighting      | \{{ this\['weighting'] \}}     | weight of item, used for sorting                |
| Release Date   | \{{ this\['release\_date'] \}} | release date of the item                        |
| Expiry Date    | \{{ this\['expiry\_date'] \}}  | expiry date of the item                         |
| Enabled        | \{{ this\['enabled'] \}}       | enable/disable the item                         |

## Folder Structure

When you create a WebApp, default files are automatically created for you. WebApp list layouts are stored in the following folder structure, which you can view via Code Editor: `layouts/webapps/My WebApp (webapp_ID)/`

Within this folder you will find the following:

* `list/`- the list layouts, used when outputting items as a section on a page
  * `default.liquid` - the default list layout

To create a custom layout file, right click on the list folder. Alternatively, you can edit the default file. All layout files must use the `.liquid` file extension, for example `mylayout.liquid`. Any files created within this folder will automatically become available in the dropdown selector when outputting a WebApp from the Toolbox
