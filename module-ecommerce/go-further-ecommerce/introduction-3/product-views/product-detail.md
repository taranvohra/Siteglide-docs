---
title: Detail Layouts
slug: bA2a-
createdAt: 2021-02-19T09:17:21.000Z
updatedAt: 2023-04-06T15:15:58.000Z
---

# 🔹 Product Detail Layout

Customise the way Products look on their automatically generated Detail Pages and add functionality for adding the Product to the Cart.

## Prerequisites

* You have [created Products](https://help.siteglide.com/article/196-products-introduction) in the Admin

## Getting Started

This Tutorial will show you how to output information about a Product on its automatically-generated Detail Page.

It will cover how to:

* Find where Product layouts are stored on Code Editor
* Develop a wrapper.liquid file
* Include an item.liquid file
* Add functionality for a User to add the Product to Cart

## File Structure

In `SITE MANAGER/Code Editor`, the folder structure for eCommerce layouts is as below:

* `layouts`
  * `modules`
    * `module_14`
      * `product`
        * `name_of_my_layout`
          * `list`
            * `wrapper.liquid`
            * `item.liquid`
          * `detail`
            * `wrapper.liquid`
            * `item.liquid`
      * `product_attributes`
        * `my_attribute_layout.liquid`

See more:

{% content-ref url="../../../reference-ecommerce/cart-and-checkout-folder-structure.md" %}
[cart-and-checkout-folder-structure.md](../../../reference-ecommerce/cart-and-checkout-folder-structure.md)
{% endcontent-ref %}

### Creating a new set of Product Layouts

To create a new set of Product layouts- create your folder at the level of "name\_of\_my\_layout". Inside that, the folders and files should be created as shown above.

## Detail Layout Development

As with list views, the detail folder inside your new layout folder should contain a wrapper.liquid and an item.liquid file. Refer to the folder structure at top of the document for reference. You also have the option of creating an attribute layout which can be included inside your item.liquid file to show Product Variations.

### wrapper.liquid

wrapper.liquid -- detail view example

```liquid
<section class="large detail-view ecommerce">
  <div class="container">
    <div class="row">
      {%- include 'modules/siteglide_ecommerce/ecommerce/get/get_products'
          item_layout: 'item' 
      -%}
    </div>
  </div>
</section>

```

This is the file for the main section code e.g. a section title or padding. You will need to use the following liquid to include your item.liquid file inside the wrapper and give it access to information about the Product:

```liquid
{%- include 'modules/siteglide_ecommerce/ecommerce/get/get_products'
    item_layout: 'item' 
-%}

```

### item.liquid

item.liquid -- detail view example

```liquid
<div class="col-lg-6"> <img src="{{this['Image'] | asset_url}}" class="img-fluid"></div>
<div class="col-lg-5 offset-lg-1">
  <div>
    <h2 class="product-title">{{this['name']}}</h2>
    <p class="product-price" data-price-control="{{this.price.price_charge}}" 
       data-currency-control="{{this.price.currency_symbol}}"></p>
    <div class="row">
      <div class="col-md-4">
        <div class="form-group">
          <label>Quantity</label>
          <input type="number" min="1" value="1" class="form-control" data-quantity-control="">
        </div>
      </div>
    </div>
  </div>
  <hr class="mt-4 mb-4">
  
{% raw %}
{% if this['Description'] %} <h4>Product Description</h4> {{this['Description']}} {% endif %}
  <hr class="mt-4 mb-4">
  <div class="row product-detail-buttons">
    <div class="col-12 col-md-6"> {% include 'ecommerce/cart_add' -%}
{% endraw %}

 </div>
    <div class="col-12 col-md-6">
      <a class="btn btn-primary" href="/cart">View my Cart</a>
    </div>
  </div>
</div>

```

Unlike the List View, the code in the item.liquid file in the Detail folder will only be displayed once instead of looped. Inside the `item.liquid` file, you'll have access to the "this" object, which contains the fields you'll need. See [reference](https://developers.siteglide.com/liquid-reference-for-product-and-attribute-layouts) for available fields or output `{{this | json}}` in the item.liquid file to see the exact data available to you.

#### Add to Cart

To create a button to add the current Product to the Cart use the following Liquid code

```liquid
{% raw %}
{%- include 'ecommerce/cart_add', component_layout: 'name_of_my_layout' -%}
{% endraw %}


```

See more:

{% content-ref url="add-to-cart-button.md" %}
[add-to-cart-button.md](add-to-cart-button.md)
{% endcontent-ref %}

#### Quantity to Add to Cart

In order to use the "Add to Cart" Button, you'll also need to have an input element where Users can select the quantity they'd like to add. Make sure it has the correct data-attribute.

```liquid
<label for="quantity">Quantity</label>
<input type="number" min="1" value="1" data-quantity-control id="quantity" />
```
