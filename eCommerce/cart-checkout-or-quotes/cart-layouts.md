---
title: Cart Layouts
slug: vU7g-
createdAt: 2021-02-18T16:04:43.000Z
updatedAt: 2024-01-30T12:41:48.974Z
---

# Cart Layouts

How to customise the Shopping Cart Layout

## Prerequisites

* You have completed [How to Create a Shopping Cart and Guest Checkout](https://help.siteglide.com/article/163-how-to-set-up-a-shopping-cart-and-guest-checkout-tutorial)

## Folder Structure

Cart layouts are stored in the following structure.

* `layouts`
  * `modules`
    * `module_14`
      * `product`
        * `name_of_my_cart_layout`
          * `list`
            * `wrapper.liquid`
            * `item.liquid`

To create a new layout, right-click on the product folder to add a folder with the name of your layout, then create the list folder and wrapper and liquid files inside it as shown.

## wrapper.liquid

The wrapper.liquid file should contain the code for the main section of code that wraps around the loop of Products in the Cart. It should include the following liquid to insert the loop of Products:

```liquid
{%- include 'modules/siteglide_ecommerce/ecommerce/get/get_products'
    item_layout: 'item' 
-%}

```

### Hiding the Cart when Empty

It's strongly recommended to hide the Cart using Liquid logic when it is empty. This logic can either go inside your `wrapper.liquid` file, or directly in the Page.

```liquid
{% raw %}
{% assign cart_parsed = context.session.cart | parse_json %}
{% if cart_parsed.size > 0 %}
  <!-- Your Layout here -->
{% else %}
  <!-- Message to say Cart is empty -->
{% endif %}
{% endraw %}


```

### Empty the Cart

`<button onclick="s_e_cart_empty(true)>Empty Cart</button>`

### Updating the Cart's Total

See the full Article on [updating the Cart's quantity here](https://developers.siteglide.com/updating-the-quantity-of-items-in-the-cart).

### Link to the Checkout Page

Of course, this is just an ordinary link. It will need updating with the slug of your Checkout Page: `<a href="/checkout>Proceed to checkout</a>`

The following reference shows how to output useful data about your Cart as a whole:

| **Field Name** | **Liquid Tag**                                   |
| -------------- | ------------------------------------------------ |
| Total Quantity | \{{context.exports.cart\_total\_quantity.data\}} |
| Shipping Price |                                                  |

\| | Shipping Price Before Tax || | Shipping Price Tax Amount || | Total Item Price || | Total Item Price Before Tax || | Total Item Tax Amount || | Total Price Reduction (due to Discounts) || | Final Total Price Before Tax || | Final Total Tax Amount || | Final Total Price ||

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

\`

\`

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
