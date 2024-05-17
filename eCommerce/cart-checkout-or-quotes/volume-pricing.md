---
title: Volume Pricing
slug: 2m_1-
createdAt: 2021-02-19T16:08:21.000Z
updatedAt: 2023-03-03T08:10:04.000Z
---

# Volume Pricing

Offer your customers better prices when they purchase in bulk. This feature lets you define as many levels of Volume Pricing as you like.

## Introduction

Volume Pricing allows your Client to offer better prices to customers who buy products in greater quantities.

Let's say for example a product normally costs £5, but to encourage larger sales , the following table of prices are available:

| **Quantity Threshold** | **Price** |
| ---------------------- | --------- |
| 1                      | £5        |
| 100                    | £4        |
| 1000                   | £3.50     |

If the customer orders 105 items, they will have passed the quantity threshold of 100, so will have access to the price of £4 per product for all 105 items. They did not order a high enough quantity to get the best available price.

## Attributes

At the present, when two alternate versions of the same Product with different attributes are present in the Cart, both their quantities will be added up and counted towards the Volume Pricing Calculation.

## Setting up Volume Pricing

There is no need to implement any front-end code in order to start using Volume Pricing. All you need to do is define the pricing in the Admin against individual products and those prices will become available.

## Outputting Volume Price Information in Product Layouts

![](https://downloads.intercomcdn.com/i/o/294801815/27f4f1076899d9efc3f57b82/image.png)

You may wish Front End to dynamically display the available prices for a product. To do so, you can loop over each pricing threshold and display the prices in a table, list or format of your choice.

Inside the Product List/ Detail Page item.liquid file, you'll have access to the following fields:

| **Field Name / Liquid Tag**           | **Example**                | **Notes**                                                                                                                                                                                             |
| ------------------------------------- | -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \{{this\['Volume pricing Enabled']\}} | true                       | Contains a boolean. If false, normal pricing will be used.                                                                                                                                            |
| \{{this\['Volume Pricing']\}}         | { "100": 400, "1000": 350} | Contains a JSON object of the currency thresholds for this product set in Admin. When stored in the database, this is organised by currency, but front-end we'll fetch the relevant currency for you. |

When looping over an object like `this['Volume Pricing']`, `.first` allows you to access the key (here the quantity threshold) and `.last` allows you to access the value (here the price).

First though, we use logic in the first line to check if the pricing has been enabled- to avoid confusion and disappointment.

```liquid
{% raw %}
{% if this.['Volume Pricing Enabled'] == true %}
  <h3>Volume Pricing Options Available</h3>
  <ul>
    {% for volume_price in this['Volume Pricing'] %}
      <li>Purchase more than {{volume_price.first}} and pay only {{this.price.currency_symbol}}
        {% include 'modules/siteglide_ecommerce/ecommerce/price_formatter'
                    price_data: volume_price.last 
        -%}</li>
    {% endfor %}
  </ul>
{% endif %}
{% endraw %}

```

## Accessing Volume Prices in the Order Confirmation Email

![](https://downloads.intercomcdn.com/i/o/294826902/b9182c8aa3c14a63189b8c6d/image.png)

Inside the Order Confirmation Email, you'll have access to the following relevant fields.

| **Field Name / Liquid Tag**                       | **Example** | **Notes**                                                                                                                                                                                              |
| ------------------------------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| \{{product.volume\_pricing\_original\_price\}}    | 60.00       | A formatted price representing the price of the row, had the better volume price not been applied.                                                                                                     |
| \{{product.volume\_pricing\_threshold\_reached\}} | 4           | The highest quantity threshold reached. If no volume pricing was accessed, this will have the value nil. You can use it in logic to check if Volume Pricing has been applied - see code example below. |
| \{{product.currency\_symbol\}}                    | £           |                                                                                                                                                                                                        |
| \{{product.price\}}                               | 19.00       | This formatted price shows the actual price of the order row. This will either be the default price, or a volume price if available.                                                                   |

The following example shows how the Volume Pricing can be shown inside a \<td> element in an Order Confirmation Email.

```liquid
<td style="padding: 5px 5px 5px 15px; font-weight: 200;" align="right">
  {% raw %}
{% if product.volume_pricing_threshold_reached != blank %}
    <span style="color: red; text-decoration: line-through;">
      {{ product.currency_symbol }}{{product.volume_pricing_original_price}}</span>
    {{ product.currency_symbol }}{{product.price}}
  {% else %}
    {{ product.currency_symbol }}{{ product.price }}
  {% endif %}
{% endraw %}
</td>
```

See the [Order Confirmation Email](https://developers.siteglide.com/order-confirmation-emails) documentation for more.
