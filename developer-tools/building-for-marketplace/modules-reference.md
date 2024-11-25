---
description: >-
  In this section, we'll add reference code which is relevant across Modules.
  Specific Modules may have further relevant reference material in their own
  sections of the docs.
---

# 💻 Reference

## Standard Module Fields

These Fields are available to all standard modules:

<table data-header-hidden data-full-width="true"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Field Name</strong></td><td><strong>Liquid Tag</strong></td><td><strong>Description</strong></td></tr><tr><td>Item Name</td><td>{{ this['name'] }}</td><td>name of the Blog Post</td></tr><tr><td>Item Slug</td><td>{{ this['slug'] }}</td><td>item URL</td></tr><tr><td>Weighting</td><td>{{ this['weighting'] }}</td><td>weight of item, used for sorting</td></tr><tr><td>Release Date</td><td>{{ this['release_date'] }}</td><td>release date of the item</td></tr><tr><td>Expiry Date</td><td>{{ this['expiry_date'] }}</td><td>expiry date of the item</td></tr><tr><td>Enabled</td><td>{{ this['enabled'] }}</td><td>enable/disable the item</td></tr></tbody></table>

## Output a Module Layout

### List Layouts

```liquid
{% raw %}
{% include 'module', id: '3', layout: 'default' %}
{% endraw %}
```

### Detail Layouts

```liquid
{% raw %}
{% include 'module', id: '3', layout: 'default', type: 'detail', item_ids: insert_item_id %}
{% endraw %}
```
{% hint style="info" %}
Usually this is not outputted directly. Instead, a detail page is dynamically generated for you by the Siteglide Admin at the chosen slug, however, it can be useful in some situations to output manually!
{% endhint %}

#### Liquid Include Parameters

* `id` - the Module's ID
* `item_ids` - output one or more module items, comma separated
* `category_ids` - output all items in one or more categories, comma separated
* `layout` - default is /default/ - 'layout' values are relative to the folder: layouts/modules/Blog (module\_3)/\[layout name]
* `per_page` - defines the number of items outputted on the page
* `show_pagination` - default is true - defines if items should be paginated when the per\_page is met.
* `sort_type` - defines the type by which items are ordered
  * `properties.name` - name of the Module item (alphabetical)
  * `created_at` - date the Module item was created
  * `updated_at` - date the Module item was last edited
  * `properties.weighting` - weighting of the Module item
  * `properties.release_date` - date the item is set to be released
  * `properties.module_field_3_1` - Sort by a core or custom field
* `sort_order` - defines the order in which the type is sorted asc - sort items in ascending order desc - sort items in descending order
* `collection` - default is 'false' - If you set it as collection: 'true' then any layout is suppressed.Data is accessible via \{{context.exports.webapp\_1.data\}}. For Example, name would be: \{{context.exports.webapp\_1.data.result.items\[0]\['name']\}}
* `use_search` - Allows the Module to be searched by keyword parameter in URL
* `use_adv_search` - Allows the Module to be filtered by core/custom field IDs in URL parameters
* `datasource` - `true`/`false` - When outputting a "nested" module inside another, the inner module tag can be given this parameter to prevent it from inheriting parameters which would change its page etc.

{% hint style="info" %}
If you nest any more Module or WebApp layouts inside this Module Layout, they will inherit the type parameter. This means if you want to input a nested list layout, you may need to reset the type parameter back to list with `type: 'list'`.
{% endhint %}

### Output the Most Recent Item

To get the most recently "released" item, you can use the `sort_type` parameter to sort by `properties.release_date`. You can alternatively use `created_at` to sort by the Item you most recently added to the Admin.

\`

\`

Then just output one post- to get the first Item. To do this, set `per_page` to `1`.

Use the `sort_order` to control whether you get the first or last item. To get the latest Item by date, the date will have a higher value, so use `'desc'` (starts with highest number) rather then `'asc'` .
