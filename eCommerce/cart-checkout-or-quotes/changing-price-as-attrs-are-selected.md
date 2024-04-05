---
title: Changing Price as Attributes are Selected
slug: 79lr-
createdAt: 2021-02-19T10:42:21.000Z
updatedAt: 2023-04-11T07:25:02.000Z
---

This Article will look in detail at the JavaScript function which updates the Product price as the customer selects Attributes.

# Prerequisites

*   Your [eCommerce Module](https://help.siteglide.com/article/200-getting-started-with-siteglide-ecommerce) should be updated to version 1.0.5 to get the latest version of this feature described by this Article. Earlier versions of the Module will have limited support for this feature on Product List views.&#x20;

*   You have [created Attributes](https://help.siteglide.com/article/188-products-attributes) on some of your Products and [included an Attributes sub-Layout](https://developers.siteglide.com/attribute-layouts) nested inside your Product Layout.&#x20;

# Introduction

&#x20;On the Product List and Detail Views you can provide customers with an option to select Product Attributes- changing features like "size" or "colour", depending on the Product.&#x20;

This Article will look in detail at the JavaScript function which achieves this and adjusts the displayed Price of the Product appropriately.&#x20;

A note on security: the prices we are working with in this topic are cosmetic only. There's no need to worry about malicious users "choosing their own prices" at this stage, as prices will be calculated afresh securely on the server if and when an Order is created.&#x20;

# The s\_e\_update\_price() Function

## What it does

&#x20;This function will update the currently displayed price of a Product to take into account any selected Attributes.&#x20;

## Where it's commonly used

&#x20;To optionally set the initial prices to be displayed on:

*   Product Detail View

*   Product List View (support added in eCommerce version 1.0.5)

To update the prices to be displayed on:

*   Product Detail View

*   Product List View (support added in eCommerce version 1.0.5)

## Arguments and Usage

&#x20;***Optional - To Display the Initial Price
***To display the initial price of a Products on the Product List, or Detail View, on Page Load, you can run the function within the following Event Listener. No arguments are required.

```javascript
<script>

   window.addEventListener('load', function() {

      s_e_update_price();

   });

</script>
```

&#x20;***To Update the Price on Attribute Select&#x20;
***To watch an Attribute for change, add the listener: `onchange="s_e_update_price()"`to the `<select>` element in your chosen Attributes Layout:

```html
<label for="{{attribute_name | slugify}}">{{name}}</label>
<select name="attr1" 
        class="form-control" 
        data-attribute-control="{{this_attribute.id}}" 
        onchange="s_e_update_price()">
{% for option in product_attribute_options -%}
<option {% if forloop.first %}selected{% endif %} value="{{option.id}}" 
            data-attribute-price-control="{{option.price_raw}}">
{{option.name}} (+{{this.price.currency_symbol}}{{option.price}})
</option>
{% endfor -%}
</select>
```

# Usage Notes

&#x20;The JavaScript looks for data in the HTML attributes in order to make its calculations. In the usage notes below we'll detail everything you need to provide for this function to do it's work.&#x20;

## Usage note 1 - Define the element which will dynamically display the product price

&#x20;The purpose of this function is to dynamically update the displayed Price, but the choice of where this should be within the Layout is up to you.&#x20;

To mark an element within the `item.liquid` file as being the element which will receive the dynamic price as its text content when calculated, add the following HTML attributes:

*   `data-price-control`

*   `data-currency-control `

The value of these Attributes should be set using Liquid to the Product's initial price and currency:

```html
<p class="product-price" 
   data-price-control="{{this.price.price_charge}}" 
   data-currency-control="{{this.price.currency_symbol}}">
   {{this.price.currency_symbol}}{{this.price.price_charge_formatted}}</p>
```

&#x20;In this example above- we also add the initial Price to the text content of the element using Liquid on Page Load. Instead, you can run the function on Page Load to display the initial price, should you choose.&#x20;

## Usage note 2 - Define the prices of Attribute Options

&#x20; In order to add the prices of Attributes to the base price- you'll need to define the prices against the `<option>` element that contains a selectable Attribute Option: `data-attribute-price-control="{{option.price.raw}}"`

For example:&#x20;

```javascript
<option value="{{option.id}}" data-attribute-price-control="{{option.price_raw}}">

      {{option.name}} {{this.price.currency_symbol}}{{option.price}})

</option>
```

## Usage note 3 - When using this Function on the Product List View, add the data-product-group attribute to your `item.liquid` file

&#x20;If you're using this function on the Product List View, you'll need to carry out additional steps to define the container for each Product. This helps the JavaScript to smoothly identify relationships between Products, their Prices and their Attributes.

The HTML attribute `data-product-group` should be added to the highest level HTML element in your Product Layout `item.liquid` file. Which type of tag this element is doesn't matter- the important thing is that all Prices and Attributes related to this Product are nested inside this element.

![](https://downloads.intercomcdn.com/i/o/248796334/de1f80c3303e3012fd1d464e/image.png)

If you do not add this Attribute- the JavaScript will treat the Product List like a Detail view- and you may experience unexpected behaviour like all prices changing at once.&#x20;

# Conclusion

This function is useful for updating the displayed price of a Product when new Attribute Options are selected- or removed- by the User / Customer.&#x20;