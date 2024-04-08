---
title: Testimonials
slug: okYu-
createdAt: 2021-02-16T15:01:30.000Z
updatedAt: 2023-04-11T10:07:59.000Z
---

This Module lets you add [Testimonials](https://help.siteglide.com/article/131-modules-getting-started#2-introduction) to your Site dynamically, so you can keep them updated in the Admin.

## Syntax

```html
{%- include 'module'
    id: '8'
    layout: 'design_system/10'
    per_page: 20
    sort_type: 'properties.name'
    sort_order: 'asc' 
-%}
```

## Parameters

*   `id` - the Module's ID

*   `item_ids` - output one or more module items, comma seperated

*   `category_ids` - output all items in one or more categories, comma seperated

*   `layout` - default is default.liquid - 'layout' values are relative to the folder: layouts/modules/Testimonials (module\_8)/\[layout name]

*   `per_page` - defines the number of items outputted on the page

*   `show_pagination` - default is true - defines if items should be paginated when the per\_page is met.`sort_type` - defines the type by which items are ordered
    *   `properties.name` - name of the Module item

    *   `created_at` - date the Module item was created

    *   `updated_at` - date the Module item was last edited

    *   `properties.weighting` - weighting of the Module item

    *   `properties.release_date` - date the item is set to be released

*   `sort_order` - defines the order in which the type is sorted
    *   `asc` - sort items in Ascending order
        *   `desc` - sort items in descending order

*   `collection` - default is 'false' - If you set it as collection: 'true' then any layout is suppressed.Data is accessible via `{{context.exports.webapp_1.data}}`. For Example, name would be: `{{context.exports.webapp_1.data.result.items[0]['name']}}`

### Liquid Tags

| **Field Name** | **Liquid Tag**                            | **Description**                         |
| -------------- | ----------------------------------------- | --------------------------------------- |
| Item Name      | {{ this\['name'] }}                       | name of the staff member                |
| Weighting      | {{ this\['weighting'] }}                  | weight of item, used for sorting        |
| Release Date   | {{ this\['release\_date'] }}              | release date of the item                |
| Expiry Date    | {{ this\['expiry\_date'] }}               | expiry date of the item                 |
| Enabled        | {{ this\['enabled'] }}                    | enable/disable the item                 |
| Image          | {{ this\['Image']\| asset\_url }}         | image of the staff member               |
| Job Title      | {{ this\['Job Title'] }}                  | job title of the staff member           |
| Quote          | {{ this\['Quote'] }}                      | quote provided by the staff member      |
| Company Name   | {{ this\['Company Name'] }}               | name of the company of the staff member |
| Company Logo   | {{ this\['Company Logo'] \| asset\_url }} | logo of the company                     |

## Layout Files

Testimonials Module layouts are stored in the following folder structure, which you can view via Code Editor: `layouts/modules/Testimonials (module_8)/`

Within this module folder you will find the following layout folders:

*   `default/` - the default layout folder   
    *   `detail/` - full page layouts folder (default not in use)
        *   `item.liquid` - detail item content file 
        *   `wrapper.liquid` - detail item wrapper file
    *   `list/` - page section layouts folder
        *   `item.liquid` - list item content file
        *   `wrapper.liquid` - list item wrapper file