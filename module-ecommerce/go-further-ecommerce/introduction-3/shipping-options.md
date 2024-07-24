---
title: Shipping Options
slug: wZDQ-
createdAt: 2021-02-19T11:59:47.000Z
updatedAt: 2023-03-03T08:09:58.000Z
---

# Shipping Options Layout

Shipping Options let customers choose how fast they'd like eCommerce Products delivered and prices are added onto the price at Checkout.

## Introduction

Shipping Options let customers choose how fast they'd like eCommerce Products delivered and prices are added onto the price at Checkout.

Here's what it does:

* Admin Users can add and remove Shipping Options e.g. "Free Delivery", "Premium"
* You can output the Shipping Options in your Cart with their own sub-layout
* Once chosen, the Shipping Option will be saved alongside the customer's Cart and the price of shipping will be added to the total price displayed.
* When an Order is made, the customer will pay for the price of Shipping and the option chosen will be displayed against their Order in the Admin.

## Managing in the Admin

You can add, edit and remove Shipping Options in the Admin. Go to ECOMMERCE/Shipping Options in the left-hand menu.

## Including the Options

The Options are designed to be included in an HTML Select box in the Cart.

![](https://downloads.intercomcdn.com/i/o/171837620/31235fa143bf9f5c05a01e15/image.png)

### Syntax

You'll need to add the following Liquid where in your Cart you want to include your Shipping sub-layout: `<div data-gb-custom-block data-tag="include" data-0='ecommerce/shipping_option' data-1='siteglide_example'></div>`

The only parameter you'll need to include is your Layout.

You won't need to do anything else to implement this feature. Any options selected by the customer will have their prices added to the price total in Checkout.

## Custom Layouts

### File Structure

Include your Custom Layout alongside my\_layout:

* `layouts`
  * `modules`
    * `module_14 (eCommerce)`
      * `shipping_option`
        * `siteglide_example.liquid`
        * `my_layout.liquid`

Here's an example:

```liquid
<div class="form-group">
	<select onchange="s_e_cart_shipping(this);">
		<option value="">--Please select--</option>
		{% raw %}
{%- for this in shipping_options -%}
			{% assign currency = this.price.properties["module_field_14/price_2"] %}
			<option {% if this.id == current_cart_shipping_id %}selected{% endif %} 
					value="{{this.id}}">{{this.name}} {{this.currency_symbol}}{{this.price}} 
					</option>
		{%- endfor -%}
{% endraw %}
	</select>
</div>


```

Some key points to note from the example:

* You'll need to put the `onchange` attribute on the HTML Select element itself and use the Siteglide function.
* You'll need to loop over the shipping\_options array we've created for you to build your HTML Option elements.
* You can use a Liquid if statement to mark an option as the Shipping Option currently selected by the User: \`

\`
