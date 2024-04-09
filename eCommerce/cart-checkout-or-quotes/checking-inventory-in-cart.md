---
title: Checking Available Inventory in the Cart Layout
slug: fO7p-
createdAt: 2021-02-19T11:44:50.000Z
updatedAt: 2023-03-03T08:09:58.000Z
---

Use the s\_e\_cart\_inventory\_check function to check the stock levels of items in the Cart and take appropriate action before Checkout.

![](https://downloads.intercomcdn.com/i/o/265736581/3daa8d263ca4120032453e6f/image.png)

# Introduction

&#x20;To give the customer the best experience and avoid disappointment, you'll want to make them aware of any problems with their Order as soon as possible.

&#x20;Using the `s_e_cart_inventory_check` function in the Cart Layout, you can check each row in the current Cart to check that the required quantity is available. Items will remain in the Cart, but a warning message will display.&#x20;

The function will also check for any Products which have been been disabled, expired or have a selected Attribute which has been disabled. These products will be automatically removed from the Cart and a warning message will be displayed to explain this.

One way to use this function is as immediate feedback when the User loads the Page or adjusts quantity in their Cart.&#x20;
Alternatively, you can run the function on the "Checkout" button press, to run a final check and redirect the User to the Checkout if successful.&#x20;

# Setting up the Cart Layout

In order for the JavaScript to read the up-to-date quantities in the Cart, you'll need to add the following attributes to your Layouts:

## Step 1) Add the Cart ID to each item

In the `item.liquid` file of your Cart Layout, add `data-s-e-cart-id="{{this.cart_data.cart_id}}"` to the highest level element.&#x20;

## Step 2) Check each item has a quantity input

In the `item.liquid` file of your Cart Layout, check that the `<input>` element containing the up to date quantity for this row has the `name` attribute with the value `quantity`. e.g. `<input name="quantity">`

## Step 3) Add the function - see next section for options

Add the `s_e_cart_inventory_check({})` function - we'll document which Event Listeners and arguments can be used later in this Article.

A common starting point would be to add the function to a button on a click event e.g.&#x20;

```liquid
{% raw %}
<button class="btn btn-success" 
        onclick="s_e_cart_inventory_check({checkout_url: '/checkout'})">
        Confirm and Checkout
        </button>
{% endraw %}
```

## Step 4) Set up an element to display a message when any Cart Items are no longer for sale

&#x20;If any Products in the Cart are no longer 'enabled' or have been deleted- or if the Product is enabled, but one of the selected Attributes is not, we'll automatically remove these rows from the Cart when the function is run.&#x20;

Adding the following data-attribute to an element will display a message explaining this when it happens: `data-s-e-cart-has-removed-products`

Meanwhile you can use the following Liquid to fetch the same message. This is useful if the Page is refreshed after running the function and you wish to keep the message up:

```liquid
{% raw %}
<p data-s-e-cart-has-removed-products>
    {% if context.session.cart_has_removed_products == true %}
        Sorry, some Products in your Cart have been removed because they are no longer for sale.
    {% endif %}
</p>
{% endraw %}
```

You can clear the message from the session when you believe the User has had a chance to read it and it will no longer be relevant. (In most cases, you'd display this straight after the Liquid version of the message). We'll clear this automatically if the function is run again without removing any products. `{% session cart_has_removed_products = null %}`

We'll explain how you can customize the message itself later in the function options.&#x20;

# How it Works

The function loops over every row in the Cart, and checks the desired Quantity against available Inventory.&#x20;

Any disabled, expired or deleted Products are removed from the Cart. So are any Products whose selected Attributes have been disabled or deleted.

An item callback function is then run to handle each remaining row of the Cart, carrying out a different behaviour whether that Item is in stock or not.&#x20;

If every Item in the Cart is in stock, a success callback function will be run, which may for example optionally redirect the User to the Checkout Page.&#x20;

## Handling Products with Different Attributes

&#x20;As Attributes do not currently have their own Inventory tracking, the function will share out available inventory between all Items in the Cart with the same Product ID.&#x20;

This means the quantities of each variation of the Product in the Cart will be added up- and if the total is greater than the Global Inventory, all of the rows with this Product ID will return as "out of stock".

Note that where two rows in the Cart list the same Product with different Attributes, the inventory will be shared between them.&#x20;

# s\_e\_cart\_inventory\_check  Options

&#x20;The `s_e_cart_inventory_check` function accepts a single argument containing a settings object. For example:

```liquid
{% raw %}
s_e_cart_inventory_check({checkout_url: '/checkout'
                                        item_cb: my_function_name
                                        success_cb: undefined });
{% endraw %}
```

&#x20;The table below details the available settings. Leave the setting `undefined` or remove the setting from the object if you desire to keep default behaviour:

| **Setting key**                 | **Example**                                                                                | **Optional**                                                                                                                                                    |
| ------------------------------- | ------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| checkout\_url:                  | '/checkout'                                                                                | Yes                                                                                                                                                             |
| item\_cb:                       | exampleItemFunctionName                                                                    | Yes                                                                                                                                                             |
| success\_cb:                    | exampleSuccessFunctionName                                                                 | Yes                                                                                                                                                             |
| no\_longer\_available\_message: | 'Sorry, some Products in your Cart have been removed because they are no longer for sale.' | Yes&#xA;&#xA;Note: the attribute data-s-e-cart-has-removed-products must be added to an element in the Cart Layout in order to display the message when needed. |

## `checkout_url`

Passing a `checkout_url` option to the function allows the function to redirect the Page to the Checkout if the inventory check is successful.

If you use a custom success function, this will be available in your parameters. Else, the default success function will use this to redirect the Page.&#x20;

***Default Behaviour***
Leaving `checkout_url`  undefined means the default Success Function will not redirect to the Checkout.

## item\_cb

&#x20;This option allows you to define a custom callback function which runs against each row in the Cart, telling you whether the Item is in stock or not.

The main function will loop over every row of Items in the Cart. For each Item, the default error function will be run.&#x20;

***Available Parameters***

| **Number** | **Parameter** | **Purpose**                                                                                                                                                                                                                   | **Example**                                                 |
| ---------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| 1st        | element       | A DOM element referencing the element with the data-attribute data-s-e-cart-id where not enough quantity is available. &#xA;&#xA;You can target elements inside this when adding and removing error messages.&#xA;&#xA;&#x20; | \<tr data-s-e-cart-id="{{this.cart\_data.cart\_id}}">\</tr> |
| 2nd        | in\_stock     | A Boolean telling you if this Item is in stock or not. &#xA;&#xA;If true, you may wish to remove previously added error messages.&#x20;If false, you should display the error message to the User.&#x20;                      | true or false                                               |
| 3rd        | quantity      | An Integer for the quantity desired by the customer.                                                                                                                                                                          |  5                                                          |
| 4th        | inventory     | An Integer for the inventory available for this Product.                                                                                                                                                                      |  4                                                          |
| 5th        | name          | The name of the Product in this row.&#x20;                                                                                                                                                                                    |  "T-Shirt"                                                  |

***Default Behaviour
***For all items:

*   The "max" attribute of the quantity `<input>` will be adjusted to match the available inventory.

If the item in the row is out of stock:

*   The class `.s-e-cart-out-of-stock` is added to the row element with the data-attribute `data-s-e-cart-id`

*   The following HTML will be added as a sibling element to the quantity

```html
 <input>: 
 <p class="s-e-cart-inventory-warning">
     Sorry we can't supply this many items of ${name}- only ${inventory} in stock.
 </p>
```

If the Item in the row is in stock:

*   The class `.s-e-cart-out-of-stock` is removed from the row element with the data-attribute `data-s-e-cart-id`

*   Previous error message elements with the class `'s-e-cart-inventory-warning'` in this row will be removed.

## success\_cb

&#x20;The `success_cb` function runs only if all Cart rows contain a lower quantity than the available inventory, in other words, it runs if all items remaining in the Cart are in stock.&#x20;

***Available Parameters***

| **Number** | **Parameter** | **Purpose**                                                                                                                                                                 | **Example** |
| ---------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| 1st        | checkout\_url | A String containing the value of checkout\_url originally passed as an option to the main function.&#x20;Can be used to redirect to the Cart, if available.&#xA;&#xA;&#x20; | '/checkout' |

&#x20;***Default Behaviour***

*   Any  `.s-e-cart-out-of-stock` classes will be removed from all Cart rows

*   Previous error message elements with the class `'s-e-cart-inventory-warning'` in all rows will be removed.

*   If a value for `checkout_url` is available, the Page will be redirected to the Checkout. Otherwise, it will not refresh the Page.

# Using Event Listeners with s\_e\_cart\_inventory\_check

## On Page Load

This can be useful so that as soon as the User arrives at the Cart they can be updated on whether items are in stock.
In this example, we don't want to refresh the Page on success because the User has just arrived on the Cart Page and will need time to review:

***Example&#x20;
***To be added to the wrapper.liquid file:

```javascript
<script>

  document.addEventListener('DOMContentLoaded', function() { s_e_cart_inventory_check({}) });

</script>

```

## On Change

This is useful if you want the Inventory checked immediately after the User changes the desired quantity.&#x20;
In the example we want to time this function straight after the [updated quantity is saved to the Cart](https://developers.siteglide.com/updating-the-quantity-of-items-in-the-cart). Instead of running the function directly then, we'll set the `check_inventory_after` option against the `s_e_cart_update_quantity` function.&#x20;

***Example
***To be added to the item.liquid file:

```javascript
<input type="number" 
       id="quantity" 
       name="quantity" 
       min="1" 
       max="{{this.inventory.quantity | default: 1}}" 
       value="{{this.cart_data.quantity}}" 
       onchange="
s_e_cart_update_quantity(event.target.value,{{this.cart_data.cart_id}}
'{{context.authenticity_token}}'
{confirm_immeditately: true
check_inventory_after: true });
">
```

## On Click

This is useful if the Customer has clicked the "Checkout" button and you wish to run a final Inventory check first.&#x20;
Here we make use of the `checkout_url` option and the default Success function:

***Example:
***To be added to the wrapper.liquid file:

```javascript
<button class="btn btn-success" 
        onclick="s_e_cart_inventory_check({checkout_url: '/checkout'})">
        Confirm and Checkout
        </button>
```
