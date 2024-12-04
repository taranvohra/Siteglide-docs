---
title: Tax Code Changer
slug: 0ify-tax-code-changer
createdAt: 2021-03-16T09:25:47.000Z
updatedAt: 2023-03-03T08:10:34.000Z
---

## What it does


Our Tax Code Changer will allow you to output a list of all Tax Codes on your site that are linked to the current session's currency. You can then set a new Tax Code for that session.

The JS function must be sent a valid Tax Code ID. See the layout named `default` for an example of how this is achieved via a `<select />` dropdown.

***

## How to add the Tax Code Changer to your view


You can add a Tax Code Changer to your site using the following include:

```
{% raw %}
{%- include 'ecommerce/tax_code_changer', layout: 'default' -%}
{% endraw %}
```

***

## Layouts


You can find layouts at `layouts > modules > module_14 (eCommerce) > components > tax_code_changer > your_layout_name_here`

The layout will require a `wrapper` and `item` file, which you can see in place in the layout named `default` that comes installed with the eCommerce Module.


