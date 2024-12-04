---
title: Customising the Add to Cart Button Component
slug: NPi3-
createdAt: 2021-02-18T15:01:22.000Z
updatedAt: 2023-03-03T08:09:58.000Z
---

# 🔹 Add to Cart Button

Customise the "Add to Cart" button to keep customers on the Page or redirect them straight to the Checkout Flow with a "Buy Now" button.

## Prerequisites

This Article assumes you've already:

* Added a "cart\_add" button to a Layout.

If you've not already done this, you can read the following Articles to learn more:

* [Product List Layouts](product-lists.md)
* [Product Detail Layouts](product-detail.md)

## Introduction

Although we've had an "Add to Cart" button for a while now, we've recently added the ability to add a custom Layout for this component.

This will allow you to:

* Change the style of the button
* Change the style of the button when the Product is out of stock
* Change the behaviour of JavaScript when adding to the Cart is successful

### Specifying a Layout

You can add a Layout to the Cart Add Button by adding a `component_layout` parameter to the Liquid:

```liquid
{% raw %}
{% include 'ecommerce/cart_add', component_layout: 'custom_layout' -%}
{% endraw %}
```

This feature is backwards compatible, so if you have a Site which does not specify a Layout for these buttons, the default Layout will be chosen automatically- and this will be identical to the style and behaviour you are used to.

## Layout Files

We store these Layout files at the following path: `layouts/modules/module_14/components/add_to_cart_button/my_custom_layout.liquid`

You can either edit the default Layout or create your own by right-clicking on the "my\_custom\_layout" folder.

## Code

Looking at the default layout, you can see that it has some key characteristics you may wish to keep in your new Layout:

* Checking if the Product is in stock
* Running the JavaScript function

### Checking if the Product is In Stock (or no inventory limit is set)

You can use a Liquid If Statement to check if the Product is in stock.

```liquid
{% raw %}
{% if this.inventory.id == blank or this.inventory.quantity != '0' -%}
  <!-- Product is in stock - or no inventory limit is set.-->
{% else -%}
  <!-- Product is out of stock. -->
{% endif -%}
{% endraw %}
```

### Running the JavaScript Function

To achieve the functionality of adding a Product to the Cart, you'll need to run a JavaScript function when the button is clicked. The first argument is mandatory- you must pass in the ID of the Product using Liquid: `onclick="s_e_cart_add({{this.id}})"`

## Customising the Success Alert

### Adding your own Function

The second argument in the JavaScript function is optional. If you like, you can add in the name of a function you've defined on your Page. This will run instead of the default "alert" message when a Product is successfully added:

```javascript
<button class="btn btn-primary" 
        onclick="s_e_cart_add({{this.id}}, my_success_function)">Add to cart</button>

<script>
  function my_success_function() {
    alert('Ajouter au Panier.');
  }
</script>
```

As in the example above, you can use this to add a different alert message with a different message. Or you could run any other JavaScript you like instead.

### Customising the Success Alert along with Live Cart Update

Remember, you also have access to the function: `s_e_live_cart_update()`which will return the number of Items now in the Cart. You could incorporate this number into the message.

```javascript
<button class="btn btn-primary" 
        onclick="s_e_cart_add({{this.id}}, my_success_function)">Add to cart</button>

<script>
  function my_success_function() {
    var cartTotal = s_e_live_cart_update();
    alert('Success! You now have '+cartTotal+' items in your Cart');
  }
</script>
```

### Buy Now Button

Some eCommerce Sites require a "Buy Now" button which adds the Product to the Cart and then sends them directly into the Checkout Flow. You can turn your "Add to Cart" button into a "Buy Now" button using customisation options:

```javascript
<button class="btn btn-primary" 
        onclick="s_e_cart_add({{this.id}}, my_success_function)">Buy it now!</button>

<script>
  function my_success_function() {
    window.location.href = "/cart";
  }
</script>
```
