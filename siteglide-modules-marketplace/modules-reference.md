---
description: >-
  In this section, we'll add reference code which is relevant across Modules.
  Specific Modules may have further relevant reference material in their own
  sections of the docs.
---

# 👀 Modules Reference

## Output a Module Layout

### List Layouts

`{%- include 'module', id: '3', layout: 'default', per_page: 1, sort_type: 'properties.release_date', sort_order: 'asc' -%}`

### Detail Layouts

`{%- include 'module', id: '3', layout: 'default', per_page: 1, sort_type: 'properties.release_date', sort_order: 'asc', type: 'detail' -%}`

{% hint style="info" %}
If you nest any more Module or WebApp layouts inside this Module Layout, they will inherit the type parameter. This means if you want to input a nested list layout, you may need to reset the type parameter back to list with `type: 'list'`.
{% endhint %}

### Output the Most Recent Item

To get the most recently "released" item, you can use the `sort_type` parameter to sort by `properties.release_date`. You can alternatively use `created_at` to sort by the Item you most recently added to the Admin.

`{%- include 'module', id: '3', layout: 'default', per_page: 1, sort_type: 'properties.release_date', sort_order: 'asc' -%}`

Then just output one post- to get the first Item. To do this, set `per_page` to `1`.

Use the `sort_order` to control whether you get the first or last item. To get the latest Item by date, the date will have a higher value, so use `'desc'` (starts with highest number) rather then `'asc'` .
