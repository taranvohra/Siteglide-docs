---
title: Currency Changer
slug: Mg4A-currency-changer
createdAt: 2021-03-16T09:25:47.000Z
updatedAt: 2023-03-03T08:10:34.000Z
---

## What it does


Our Currency Changer will allow you to output a list of all currencies on your site, and then set a new currency for that session.

The JS function must be sent a valid currency code in lowercase. See the layout named `default` for an example of how this is achieved via a `<select />` dropdown.

When changing currency, then default Tax Code for that currency is also automatically applied.

***

## How to add the Currency Changer to your view


You can add a Currency Changer to your site using the following include:

```liquid
{% raw %}
{%- include 'ecommerce/currency_changer', layout: 'default' -%}
{% endraw %}
```

***

## Layouts


You can find layouts at `layouts > modules > module_14 (eCommerce) > components > currency_changer > your_layout_name_here`

The layout will require a `wrapper` and `item` file, which you can see in place in the layout named `default` that comes installed with the eCommerce Module.


