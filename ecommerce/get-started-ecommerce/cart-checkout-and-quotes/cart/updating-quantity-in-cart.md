---
title: Updating the Quantity of Items in the Cart
slug: KulF-
createdAt: 2021-02-19T10:28:45.000Z
updatedAt: 2024-01-30T12:31:43.224Z
---

# Updating Quantity in Cart

In this Article we'll take an in-depth look at the JavaScript needed to update the quantity of items in the Cart Layout.

## Introduction

In this Article we'll take an in depth look at the JavaScript needed to update the Cart when the customer makes changes in the Cart itself.

There are two main flows you can implement:

| **Use Case**                                                         | **Step 1)**                                                                      | **Step 2)**                                     |
| -------------------------------------------------------------------- | -------------------------------------------------------------------------------- | ----------------------------------------------- |
| Change Cart Quantity with a single action                            | Run the `s_e_cart_update_quantity()` function with the 4th argument set to true  |                                                 |
| Change Cart Quantity by: 1) Making a change 2) Confirming the change | Run the `s_e_cart_update_quantity()` function with the 4th argument set to false | Run the `s_e_cart_update()` function to confirm |

A second choice is between whether you want to reload the Page to get new values or have our JavaScript function live update them for you.

We'll take a look at the key functions involved and the different ways they can be used within your Layout.

## The s\_e\_cart\_update\_quantity() function

### What it does

The function will queue a change to the Cart in your local storage, but will not yet confirm the change- unless you explicitly ask it to.

### Where it's commonly used

This function is designed to work as a callback function to Events triggered on the element which controls the quantity of items in the currently viewed Cart e.g. it could be added to this element in the Cart Layout `item.liquid` file.

```liquid
<label for="quantity">Quantity</label>
<input type="number" id="quantity" name="quantity" value="{{this.cart_data.quantity}}">

```

Like so:

```liquid
<label for="quantity">Quantity</label>
<input type="number" id="quantity" name="quantity" value="{{this.cart_data.quantity}}" 
onchange="s_e_cart_update_quantity(event.target.value,{{this.cart_data.cart_id}}
'{{context.authenticity_token}}', false);">
```

### Arguments and Usage

You must pass the arguments 1-3. Argument 4 is optional.

`s_e_cart_update_quantity(value, cart_id, token, update_entire_cart);`

1. `value` - The quantity required of this Item. Usually set to `event.target.value` if the event was triggered on a target input element.
2. `cart_id` - Set to `{{this.cart_data.cart_id}}` to get the ID referring to the current Item in the `item.liquid` file.
3. `token` - Set to '`{{context.authenticity_token}}`'
4. `update_entire_cart` - Boolean - defaults to `false`. If you pass true, we'll automatically run the `s_e_cart_update()` function (see below) as a further callback, confirming the Cart update immediately.

```javascript
s_e_cart_update_quantity(event.target.value, {{this.cart_data.cart_id}}
'{{context.authenticity_token}}', false);
```

Your choice of which event is watched will affect the User Experience e.g. `onkeyup` as opposed to `onchange`.

In conclusion, this function prepares an update to the Cart quantities. In the next section, we'll look at how to apply those changes.

## The s\_e\_cart\_update() function

### What it does

This function will apply the changes in the Cart quantities that you have already queued using the previously discussed `s_e_cart_update_quantity();`

### Where it's commonly used

You can either use this function directly to confirm Cart changes when the User is ready, or indirectly.

1. If true is passed for the 4th argument of the previously discussed `s_e_cart_update_quantity()` function, we'll run this function immediately. In this case, you won't need to directly call this function yourself.
2. Normally this function will be used as a callback to an event triggered on a button on your Cart `wrapper.liquid` file. E.g.

```javascript
<button class="btn btn-primary" 
        onclick="s_e_cart_update(false,'{{context.authenticity_token}}')">Update cart</button>
```

### Arguments and Usage

You must pass the arguments 1-2.

`s_e_cart_update(reload, token);`

1. `reload` - Boolean - `true` will refresh the Page after updating; `false` will not. This can also be overridden by passing in a `success_cb` function.
2. `token` - Set to '`{{context.authenticity_token}}`'
3. `check_inventory_after` - Boolean - `false` - will check inventory stock levels without refreshing the page if set to true.
4. `success_cb` - function - `s_e_cart_update_cb_default`- optionally pass in a callback function which will be called after the cart has finished updating. Your function will be passed the parameters: `reload`, `check_inventory_after` - both are Booleans which can be used to modify behaviour or ignored.

```javascript
s_e_cart_update(false,  '{{context.authenticity_token}}', false, function(reload, check_inventory_after) {
 //Do something after cart update
} );

```

## Live Updating Cart Values when Reload is set to `false`

When passing in a `false` reload argument, you will need to follow additional steps to update the following:

* The total quantity
* The total price
* The price of the line item that was just updated.
* -optional- the currency symbol

### Live Updating Total Quantity

You can use our [Live Cart Update feature](../../../../eCommerce/get-started-ecommerce/cart-checkout-and-quotes/cart/cart-live-updates.md) to get the new total quantity of items in the Cart.

The `s_e_cart_update()` function will automatically call the `s_e_live_cart_update()` function for you- but you'll need to wrap your displayed total in a \<span> class with the following data-attribute: `<span data-s-e-live-cart-quantity>{{items_in_cart}}</span>`

### Live Updating Total Price

In the `wrapper.liquid` file, wrap the following element and data-attribute around the Liquid value for the total Cart Price: `<span data-s-e-live-cart-total></span>`

e.g.

```javascript
<p><strong>TOTAL PRICE:</strong> 
    <span data-s-e-live-cart-total>
    {% include 'ecommerce/price_total'
                format_type: 'formatted' -%}</span></p>
```

### Live Updating Item Price

In the `item.liquid` file for your Cart Layout, wrap the following element and data-attribute around the Liquid value for the item's price: `<span data-s-e-live-cart-item-price="{{this.cart_data.cart_id}}"></span>`

e.g.

```javascript
<td>{{this.price.currency_symbol}}
        <span data-s-e-live-cart-item-price="{{this.cart_data.cart_id}}">
            {{this.cart_data.price}}
            </span>
            </td>
```

It is necessary to add this item's Cart ID as the attribute's value, in order to locate the correct record within the Cart. This will continue to use the Liquid value on initial Page load, but will now replace it with the live value when needed.

### Live Updating Currency - Optional

Depending on your HTML structure, you may already be displaying the currency symbol. If the JavaScript is overwriting it, you can add the following HTML to have the JavaScript return it when the function runs: `<span data-s-e-live-cart-currency></span>`

## Troubleshooting Enter Button Presses

If you want to allow Users to press the enter button in the quantity input to trigger the event, you may need to modify your `wrapper.liquid` file so that the Cart is no longer wrapped in a `<form>` element but a `<div>` instead. Make sure to adapt your stylesheets if you do this.

We'd recommend against any solution which stops the default submit behaviour on the Cart buttons that should press on focus and enter keypress- as this will negatively impact Accessibility.

## Conclusion

If you want Users to be able to instantly update the Cart by changing values in the quantity input, you can run just the `s_e_cart_update_quantity();` function with the 4th argument set to true. You may wish to use the `onkeyup` event for even more instant feedback.

If you want Users to have the option to confirm Cart Quantity updates before they are applied- you'll need to first run `s_e_cart_update_quantity()` when each input is changed and afterwards run `s_e_cart_update()` when the User is ready to confirm.
