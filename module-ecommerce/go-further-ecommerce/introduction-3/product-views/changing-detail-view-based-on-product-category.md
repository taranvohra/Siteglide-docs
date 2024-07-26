---
title: How can I change the Detail View for Products based on their category?
slug: 32Iw-
createdAt: 2021-02-18T14:25:34.000Z
updatedAt: 2023-04-11T07:35:09.000Z
---

# 🔹 Dynamic Product Layouts based on Categories

Wondering how to adjust the Product Detail Page based on Category?

## Answer:

As a User navigates to your Product Detail Page, Siteglide will load the Detail View you have specified in your eCommerce Settings. However, it is perfectly possible to customise this based on [Categories](../../../../categories/about-categories.md), using Liquid logic! You can read more about using Categories on the Layout of the WebApp or Module Item they belong to [here](../../../../categories/go-further-categories/filtering-webapps-and-modules-by-categories.md).

In this example, you'd need to know the ID of a category you want to display; this can be found in Admin when you select a category. E.g. let's say we want to display something special when something has the category "Featured" and you know it has an ID of "111111":

```liquid
{% raw %}
{% assign featured_id = "111111" %}
{% for category_id in this.category_array -%}
  {% if category_id == featured_id %}
    <!-- Add Featured Content Here -->
  {% endif %}
{% endfor %}
{% endraw %}
```
