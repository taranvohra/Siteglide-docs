---
title: How to format price and output currency?
slug: how-to-format-price-and-output-currency-dHjB8
createdAt: 2020-10-26T01:14:32.000Z
updatedAt: 2023-03-03T08:07:47.000Z
---

### Formatting Price

In the eCommerce Module, a formatted price is generated so partners can quickly output the correct price. However, you may sometimes need to convert a "raw" price integer to a currency format.

Instead, we can include `price_formatter`, which will convert the price from cents to dollars (or your currency's equivalent)

```liquid
{% raw %}
{%- include 'modules/siteglide_ecommerce/ecommerce/price_formatter'
    price_data: my_price_variable 
-%}
{% endraw %}
```

Here `my_price_variable` is the variable containing a price you'd like to format. This will then output the formatted price.