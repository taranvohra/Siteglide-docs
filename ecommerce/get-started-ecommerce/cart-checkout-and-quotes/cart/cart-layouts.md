---
title: Cart Layouts
slug: vU7g-
createdAt: 2021-02-18T16:04:43.000Z
updatedAt: 2024-01-30T12:41:48.974Z
---

# 🔹 Cart Layouts

How to customise the Shopping Cart Layout

## Prerequisites

* You have completed [How to Create a Shopping Cart and Guest Checkout](../../../../eCommerce/get-started-ecommerce/cart-checkout-and-quotes/steps-to-implement-a-guest-checkout-flow.md)

## :deciduous\_tree: Folder Structure

Cart layouts are stored in the following structure:

```bash
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

See the full Cart & Checkout folder structure here:

{% content-ref url="../../cart-and-checkout-folder-structure.md" %}
[cart-and-checkout-folder-structure.md](../../cart-and-checkout-folder-structure.md)
{% endcontent-ref %}

## wrapper.liquid

The wrapper.liquid file should contain the code for the main section of code that wraps around the loop of Products in the Cart. It should include the following liquid to insert the loop of Products:

```liquid
{% raw %}
{% assign cart_parsed = context.session.cart | parse_json %}
{% if cart_parsed.size > 0 %}
  {%- include 'modules/siteglide_ecommerce/ecommerce/get/get_products' item_layout: 'item' -%}
{% else %}
  Sorry, your cart is empty.
{% endif %}
{% endraw %}


```

#### Empty the Cart

`<button onclick="s_e_cart_empty(true)">Empty Cart</button>`

#### Link to the Checkout Page

Of course, this is just an ordinary link. It will need updating with the slug of your Checkout Page: `<a href="/checkout>Proceed to checkout</a>`

### Reference

The following reference shows how to output useful data about your Cart as a whole:

| **Field Name** | **Liquid Tag**                                 |
| -------------- | ---------------------------------------------- |
| Total Quantity | `{{context.exports.cart_total_quantity.data}}` |
| Shipping Price | \`                                             |

\` | | Shipping Price Before Tax | \`\` | | Shipping Price Tax Amount | \`\` | | Total Item Price | \`\` | | Total Item Price Before Tax | \`\` | | Total Item Tax Amount | \`\` | | Total Price Reduction (due to Discounts) | \`\` | | Final Total Price Before Tax | \`\` | | Final Total Tax Amount | \`

`| | Final Total Price | \`\{% include 'ecommerce/price\_total', format\_type: 'formatted' -%\} |

\` |

If you have added Product Attributes to the Products in the Siteglide Admin, you can also access the `cart_product_attributes` with the following liquid: `{{ context.exports.cart_product_attributes }}`

Normally though, Attributes will be handled in the next step- the item.liquid file.

### item.liquid

The cart layout will iterate in a loop, outputting the item.liquid file for each line in the customer's cart.

{% hint style="info" %}
**`cart_id`**

Each line in the cart has a `cart_id` accessible at `{{this.cart_data.cart_id}}.`\
\
When modifying the cart with JS, this `cart_id` will be needed.\
\
Multiple lines in the cart may refer to the same product if a different combination of attributes is selected.
{% endhint %}

Building the Cart's item.liquid file is similar to building an item.liquid layout file for a Product List View. Learn more about the available fields [here](../product-views/product-liquid-reference.md).

There are some additional points to bear in mind when creating a cart layout's item.liquid file:

#### Removing an individual Product from the Cart:

The `s_e_cart_remove` function can be used to remove a line from the cart.

If the cart has several lines containing the same product, but with different attributes, only the targeted line and its attributes will be removed.

In this example, the function is called when a button is clicked and Liquid is used to pass the cart ID into the function:

#### item.liquid

```liquid
<button onclick="s_e_cart_remove(true,{{this.cart_data.cart_id}})">
  Remove Item from Cart
</button>
```

You can optionally pass in a callback function to the third argument to be called after the row has been removed from the cart. In order for this to work, you need to set `reload` (the first argument) to `false`.

#### item.liquid

```liquid
<button onclick="s_e_cart_remove(false,{{this.cart_data.cart_id}},removeCallback)">
  Remove Item from Cart
</button>
```

#### JavaScript

```javascript
function removeCallback() {
  //Do something
}
```

#### Increasing the Quantity of a Product in the Cart:

See the full Article on [updating Product quantities here](updating-quantity-in-cart.md).

#### item.liquid

```liquid
<!-- Step 1 -->

<input 
  type="number"
  name="quantity"
  min="1"
  value="{{this.cart.data.quantity}}"
  onchange="s_e_cart_update_quantity(event.target.value,{{this.cart_data.cart_id}},'{{context.authenticity_token}}',false)"
>

```

#### wrapper.liquid

```liquid
<!-- Step 2 -->

<button onclick="s_e_cart_update(false,'{{context.authenticity_token}}')">Update Cart</button>

```

Note that, after updating this input field, the User will also have to click the "Update Cart" button. Following the link above will lead to a more detailed article.

#### Outputting the Attributes the User chose for this item:

```liquid
{% raw %}
{% include 'ecommerce/cart_product_attributes' %}
{% endraw %}


```

#### Controlling Inventory

In order to make sure Users do not increase the quantity of items in their Cart, when the Product is out of stock, you could add a "max" attribute to the quantity input:

```liquid
<input type="number" 
       name="quantity" 
       min="1" 
       max="{{this.inventory.quantity}}" 
       value="{{this.cart_data.quantity}}" 
       onchange="s_e_cart_update_quantity(event.target.value,{{this.cart_data.cart_id}},'{{context.authenticity_token}}')"
/>


```

{% hint style="info" %}
Items added to a Cart in Siteglide are not reserved. It is possible for two or more customers to add the last product in stock to their cart at once.
{% endhint %}
