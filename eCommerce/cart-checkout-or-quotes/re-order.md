---
title: Add Items from a Previous Order to the Cart
slug: yX7s-
createdAt: 2021-02-18T16:16:14.000Z
updatedAt: 2023-03-03T08:09:58.000Z
---

Help customers find regular purchases and favourite products with the reorder button.

# Introduction

Help customers find regular purchases and favourite products with the reorder button.
The button can be added to a [`user_orders`](https://developers.siteglide.com/cart-checkout-and-orders-flow-with-secure-zones-module-tutorial) Layout or any other Layout where you have access to an Order ID.&#x20;

For this reorder feature to work, the User:

*   Must be logged in

*   Must have been logged in when they originally made the Order

The feature fetches all Products from that Order and adds those that are still available to the Cart. This gives the User a chance to review and adjust quantities before Checkout.&#x20;

A message can also be displayed to the User to detail any Products from that previous Order which are no longer available. Though, this is only possible where an Order still exists in the database and has not been deleted.&#x20;

# Developing the Order Button

## Including the Button

The following Liquid will output the reorder button:`{% include 'ecommerce/reorder_button', layout: 'default', order_id: this.id %}`

Parameters:

*   `layout`

*   `order_id`

The button can be added in any Liquid Layout, but you'll need to have access to the ID for an Order belonging to that User- which is most easily available in the [User Orders](https://developers.siteglide.com/cart-checkout-and-orders-flow-with-secure-zones-module-tutorial) Layout or the [Order Details](https://developers.siteglide.com/order-confirmation-emails) Layout (note that a User can't be logged in when reading an email, so this feature will not work from an Order Details Layout in an email).&#x20;

In the User Orders Layout, the exact Liquid for the ID will depend on the variable you've set in the loop. In the following example, the variable assigned to each iteration of the loop is this. so the Order ID is available inside the loop as this.id.

```liquid
{% raw %}
{% for this in orders %}

  {% include 'ecommerce/reorder_button'
     layout: 'default'
     order_id: this.id 
  %}

{% endfor %}
{% endraw %}
```

The button will only work if the User is logged in, so you may wish to add the following logic to an Order Details Layout to make sure the User is logged in before displaying:

```liquid
{% raw %}
{% if context.current_user.id %}
<!-- Code only runs if User is logged in -->
{% endif %}
{% endraw %}
```

## The Button Layout

Adding the button will load a small button layout.&#x20;
You can find the default Layout or create a custom Layout at the following path: `layouts/modules/module_14/components/reorder_button/my_layout_name.liquid`

***Adding the function
***The styling of the button is completely up to you.&#x20;
To carry out its main functionality, the button requires an event to be attached to it which will run a JavaScript function:

```liquid
{% raw %}
onclick="s_e_reorder({ order_id: '{{order_id}}'
                        token: '{{token}}'
                        cart_url: '/cart'
                        error_cb: error
                        success_cb: success})"
{% endraw %}
```

The function takes a single argument containing an options object. The available arguments are as follows:

| **Option**  | **Purpose**                                      | **Example/ Default** | **Required?** |
| ----------- | ------------------------------------------------ | -------------------- | ------------- |
| order\_id:  | The Order ID to be looked up and added to Cart   | '{{order\_id}}'      | Yes           |
| token:      | Access token from Liquid                         | '{{token}}'          | Yes           |
| cart\_url:  | Cart URL for redirection after successful result | '/cart'              | Yes           |
| error\_cb:  | Custom Error Function Name                       | error                | Optional      |
| success\_cb | Custom Success Function Name                     | success              | Optional      |

***Adding a Custom Error Function
***The Custom Error function will be called in the following circumstances (the table also shows the value of the "error" parameter passed back when this occurs):

| **Error**                                                                     | `error`** parameter value**                        |
| ----------------------------------------------------------------------------- | -------------------------------------------------- |
| Order found but does not belong to this User, or User is not logged in.&#x20; | "Unauthorized."                                    |
| Order does not exist                                                          | "Order was not found."                             |
| All associated products are disabled, expired, unreleased or deleted.         | "Order was found, but no products were available." |
| Any other error                                                               | "Could not reorder."                               |

Parameters returned:

1.  `error` - see above

2.  `reorder_unavailable_products` - an object containing all Products which could not be added to the Cart from the Order. Looping over this object can allow you to display the ID and/or name of these Products. Expiry dates are also provided, where they exist, for context.

The default error behaviour is to display an "alert" containing the error message.

***Adding a Custom Success Function
***If you add a Custom Success Function, you must add a Custom Error Function.

The custom success function will run if an Order was successfully found and at least one Product was successfully added to the Cart. Not all Products related to the Order may have been available.

Parameters returned:

1.  `cart_url` - The URL of the Cart that you passed into the function originally.

2.  `reorder_unavailable_products` - An Object containing the Products which are no longer available and couldn't be added to the Cart.&#x20;

3.  `reorder_added`- an integer representing the number of unique products with either a different Product ID or the same Product ID but different Attributes, that were successfully added to Cart. The number ignores the actual quantity of each product added and is more useful as a measure of successfully added rows.

The default success behaviour is to re-direct the Page to the Cart URL.&#x20;

You can choose whether to display a message about the unsuccessful items before that, using JavaScript or display that information via Liquid when the User arrives at the Cart.&#x20;

# Adding a Message to the Cart to List the Unavailable Products

Successfully added Products are automatically added to the User's Cart. When they arrive at their Cart Page- they can review the quantities and Check Out when ready.

The following Liquid tags can be used to either confirm the Order ID which has been added to the Cart, or present a detailed breakdown of the Products which were not successfully added; this is an alternative to showing this information in the Custom Success Function.&#x20;

| **Liquid Tag**                                                                                                                                                                                | **Purpose**                                                                                                                                                                                              | **Example Output**                                                                        |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| {{context.session.reorder\_added\_to\_cart}}&#xA;&#xA;                                                                                                                                        | The ID of the ( at least partially ) successfully added Order. &#xA;&#xA;This can be used in Logic to decide whether to display feedback at all- as if it equals blank, there will be no recent reorder. | "345"                                                                                     |
| {{context.session.reorder\_unavailable\_products}}                                                                                                                                            | An Object containing details on unsuccessful Products- if there were any.&#x20;This contains the same information returned to the Custom JavaScript Callback Functions.                                  | {"173":{"product\_id":"173","name":"Classical Summer Album","expiry\_date":"2145916800"}} |
| &#xA;{% for this in context.session.reorder\_unavailable\_products %}   {{this\[0]}}{% endfor %}&#xA;&#xA;&#xA;&#xA;                                                                          | By looping over the unavailable Products and accessing the \[0] index, you can access their key:&#xA;&#xA;- the Product ID.                                                                              | "123"                                                                                     |
| {% for this in context.session.reorder\_unavailable\_products %}     {{this\[1].name}}&#xA;{{this\[1].expiry\_date}}&#xA;{{this\[1].expiry\_date \| date: "%d/%m/%Y" }}&#xA;&#xA;{% endfor %} | By looping over the unavailable Products and accessing the \[1] index, you can access their fields:&#xA;&#xA;- the Name- the expiry date of the Product- the expiry date of the Product (formatted)      | *   "Classical Summer"

*   "2145916800"

*   "01/11/2020"                                |
| {% session reorder\_unavailable\_products = null %} &#xA;&#xA;                                                                                                                                | Clear the reorder\_unavailable\_products data from the session&#xA;&#xA;This would only happen automatically if another Order is reordered, the Cart is emptied, or Checkout is completed.               |                                                                                           |
| {% session reorder\_added\_to\_cart = null %} &#xA;&#xA;                                                                                                                                      | Clear the reorder\_added\_to\_cart data from the session.This would only happen automatically if another Order is reordered, the Cart is emptied, or Checkout is completed.                              |                                                                                           |

The above Liquid tags are accessing the User's session. This means they are temporary messages for that User. Each time an order is reordered the old message will be replaced.

## Example of Cart Liquid after Partially or Fully Successful Reorder

This example will, if an Order was successfully reordered -display a message to Users confirming the Order ID which was reordered.
If any Products were not available, these are displayed in a table.
Finally, the session is cleared, so the User only sees this once.&#x20;

```liquid
{% raw %}
{% if context.session.reorder_added_to_cart != blank %} 
  <div class="alert alert-warning">

    <h3>Previous Order #{{context.session.reorder_added_to_cart}} added to Cart</h3> 
    <p>You can review quantities and head to Checkout to complete the Order.</p>

    {% if context.session.reorder_unavailable_products != blank %} 
      <h4>Unavailable Products</h4>

      <p>Sorry, the following Products were no longer available:</p>

      <table>

        <tr>

          <th>Product ID</th>

          <th>Name</th>
 
        </tr>

        {% for this in context.session.reorder_unavailable_products %} 
          <tr>

            <td>{{this[0]}}</td>

            <td>{{this[1].name}}</td>
 
          </tr>

        {% endfor %}

      </table>

    {% endif %}

  </div>

{% endif %}
{% endraw %}
```



