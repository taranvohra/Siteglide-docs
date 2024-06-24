---
title: Cart Layouts
slug: vU7g-
createdAt: 2021-02-18T16:04:43.000Z
updatedAt: 2024-01-30T12:41:48.974Z
---

# 🔹 Cart Layouts

How to customise the Shopping Cart Layout

## Prerequisites

* You have completed [How to Create a Shopping Cart and Guest Checkout](../../ecommerce-module/introduction-2/steps-to-implement-a-guest-checkout-flow.md)

## :deciduous\_tree: Folder Structure

Cart layouts are stored in the following structure:

```
marketplace_builder
└───views
    └───partials
        └───layouts
            └───modules
                └───module_14
                    └───product
                        collection.liquid
                        └───custom_cart_layout
                            └───list
                                item.liquid
                                wrapper.liquid
```

See the full Cart & Checkout folder structure here:&#x20;

{% content-ref url="../../ecommerce-module/introduction-2/cart-and-checkout-folder-structure.md" %}
[cart-and-checkout-folder-structure.md](../../ecommerce-module/introduction-2/cart-and-checkout-folder-structure.md)
{% endcontent-ref %}

## wrapper.liquid

The wrapper.liquid file should contain the code for the main section of code that wraps around the loop of Products in the Cart. It should include the following liquid to insert the loop of Products:

{% tabs %}
{% tab title="product/custom_cart_layout/list/wrapper.liquid" %}
<pre class="language-liquid"><code class="lang-liquid"><strong>{% assign cart_parsed = context.session.cart | parse_json %}
</strong>{% if cart_parsed.size > 0 %}
  &#x3C;!-- Your Layout here -->
  {%- include 'modules/siteglide_ecommerce/ecommerce/get/get_products'
    item_layout: 'item' 
  -%}
{% else %}
  &#x3C;!-- Message to say Cart is empty -->
{% endif %}
</code></pre>
{% endtab %}
{% endtabs %}

{% hint style="info" %}
It's strongly recommended to hide the Cart using Liquid logic when it is empty. This logic can either go inside your `wrapper.liquid` file, or directly in the Page.
{% endhint %}

### Empty the Cart

`<button onclick="s_e_cart_empty(true)>Empty Cart</button>`

### Updating the Cart's Total

See the full Article on [updating the Cart's quantity here](https://developers.siteglide.com/updating-the-quantity-of-items-in-the-cart).

### Link to the Checkout Page

Of course, this is just an ordinary link. It will need updating with the slug of your Checkout Page: `<a href="/checkout>Proceed to checkout</a>`

## Reference

The following reference shows how to output useful data about your Cart as a whole:

<table data-full-width="true"><thead><tr><th>Field Name</th><th>Liquid Tag</th></tr></thead><tbody><tr><td>Total Quantity</td><td>{{context.exports.cart_total_quantity.data}}</td></tr><tr><td>Shipping Price</td><td></td></tr><tr><td>Shipping Price Before Tax</td><td></td></tr><tr><td>Shipping Price Tax Amount</td><td></td></tr><tr><td>Total Item Price</td><td></td></tr><tr><td>Total Item Price before Tax</td><td></td></tr><tr><td>Total Item Tax Amount</td><td></td></tr><tr><td>Total Price Reduction (due to discounts)</td><td></td></tr><tr><td>Final Total Price before Tax</td><td></td></tr><tr><td>Final Total Tax Amount</td><td></td></tr><tr><td>Final Total Price</td><td></td></tr></tbody></table>

If you have added Product Attributes to the Products in the Siteglide Admin, you can also access the `cart_product_attributes` with the following liquid: `{{ context.exports.cart_product_attributes }}`

Normally though, Attributes will be handled in the next step- the item.liquid file.

## item.liquid

The item.liquid file should contain the code which is rendered for each iteration of the loop of Products. Building the Cart's item.liquid file is similar to building an item.liquid layout file for a Product List View. Learn more about the available fields [here](https://developers.siteglide.com/liquid-reference-for-product-and-attribute-layouts).

There are some additional points to bear in mind when creating a cart layout's item.liquid file:

### Removing an individual Product from the Cart:

The `s_e_cart_remove` function can be used to remove a line from the cart.

If the cart has several lines containing the same product, but with different attributes, only the targeted line and its attributes will be removed.

In this example, the function is called when a button is clicked and Liquid is used to pass the cart ID into the function:

`<button onclick="s_e_cart_remove(true,{{this.cart_data.cart_id}})"></button>`

You can optionally pass in a callback function to the third argument to be called after the row has been removed from the cart. In order for this to work, you need to set `reload` (the first argument) to `false`.

### Increasing the Quantity of a Product in the Cart:

See the full Article on [updating Product quantities here](https://developers.siteglide.com/updating-the-quantity-of-items-in-the-cart).

```liquid
<input type="number" 
       name="quantity" 
       min="1" 
       value="{{this.cart_data.quantity}}" 
       onchange="s_e_cart_update_quantity(event.target.value,{{this.cart_data.cart_id}},'{{context.authenticity_token}}')"
/>


```

Note that, after updating this input field, the User will also have to click the "Update Cart" button, though this is covered in the wrapper.liquid file- as it covers the whole Page.

### Outputting the Attributes the User chose for this item:

```liquid
{% raw %}
{% include 'ecommerce/cart_product_attributes' -%}
{% endraw %}
```

## Controlling Inventory

In order to make sure Users do not increase the quantity of items in their Cart, when the Product is out of stock, you could use a liquid if statement:

```liquid
{% raw %}
{% if this.inventory.id != blank and this.inventory.quantity == '0' -%}
  <!-- Code here -->
{% endif %}
{% endraw %}

```

To improve this so that the User cannot increase the value by a greater number than is allowed by the stock level, you could add a "max" attribute to the quantity input:

```liquid
<input type="number" 
       name="quantity" 
       min="1" 
       max="{{this.inventory.quantity}}" 
       value="{{this.cart_data.quantity}}" 
       onchange="s_e_cart_update_quantity(event.target.value,{{this.cart_data.cart_id}},'{{context.authenticity_token}}')"
/>
```
