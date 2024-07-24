## Syntax

```liquid
{% raw %}
{%- include 'module'
    id: '10'
    layout: 'design_system/2'
    per_page: 20
    sort_type: 'created_at'
    sort_order: 'desc' 
-%}
{% endraw %}
```

## Parameters

*   `id` - the Module's ID

*   `item_ids` - output one or more module items, comma seperated

*   `category_ids` - output all items in one or more categories, comma seperated

*   `layout` - default is default.liquid - 'layout' values are relative to the folder: layouts/modules/FAQ (module\_10)/\[layout name]

*   `per_page` - defines the number of items outputted on the page

*   `show_pagination` - default is true - defines if items should be paginated when the per\_page is met.

*   `sort_type` - defines the type by which items are ordered
    *   `properties.name` - name of the Module item (alphabetical)

    *   `created_at` - date the Module item was created

    *   `updated_at` - date the Module item was last edited

    *   `properties.weighting` - weighting of the Module item

    *   `properties.release_date` - date the item is set to be released

*   `sort_order` - defines the order in which the type is sorted
    *   `asc` - sort items in ascending order

    *   `desc` - sort items in descending order

*   `collection` - default is 'false' - If you set it as collection: 'true' then any layout is suppressed.Data is accessible via `{{context.exports.webapp_1.data}}`. For Example, name would be: `{{context.exports.webapp_1.data.result.items[0]['name']}}`

## Liquid Tags

| **Field Name** | **Liquid Tag**                | **Description**                  |
| -------------- | ----------------------------- | -------------------------------- |
| Item Name      | {{ this\['name'] }}           | name of the FAQ                  |
| Weighting      | {{ this\['weighting'] }}      | weight of item, used for sorting |
| Release Date   | {{ this\['release\_date'] }}  | release date of the item         |
| Expiry Date    | {{ this\['expiry\_date'] }}   | expiry date of the item          |
| Enabled        | {{ this\['enabled'] }}        | enable/disable the item          |
| Question       | {{ this\['question'] }}       | FAQ question                     |
| Answer         | {{ this\['answer'] }}         | FAQ answer                       |

## Layout Files

FAQ Module layouts are stored in the following folder structure, which you can view via Code Editor: `layouts/modules/FAQ (module_10)/`

Within this module folder you will find the following layout folders:

*   `default/` - the default layout folder
    *   `detail/` - full page layouts folder
        *   `item.liquid` - detail item content file

        *   `wrapper.liquid` - detail item wrapper file

    *   `list/` - page section layouts folder
        *   `item.liquid` - list item content file

        *   `wrapper.liquid` - list item wrapper file
