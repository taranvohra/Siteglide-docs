---
title: List Layouts
slug: qQA5-
createdAt: 2021-02-19T09:29:06.000Z
updatedAt: 2023-04-06T15:14:13.000Z
---

Similar to WebApp List Layouts, a Product List Layout can allow users to browse Products. It can be filtered and sorted too!

![](https://siteglide-52c14a1a8a9b.intercom-attachments-1.com/i/o/163490181/725ceee413d826167274bb97/list_layout.jpg)

# Prerequisites

*   You have [created Products](https://help.siteglide.com/article/196-products-introduction) in the Admin

# Getting Started

This Tutorial will show you how to output a list of Products on your site.

It will cover how to:

*   Find where Product layouts are stored on Code Editor

*   Develop a wrapper.liquid file

*   Develop an item.liquid file

# Add a List of Products to a Site

```html
{%- include 'ecommerce/products'
    layout: "products"
    category_ids: current_category_id
    type: 'list',
    show_pagination: 'true'
-%}
```

## Parameters:

*   `layout` - choose the layout file for this list.

*   `category_ids` - filter the List by these category ids

*   `sort_type`  - the field you wish the sort by

*   `sort_order` - 'asc' or 'desc' - the order you wish to sort by.

*   `use_search` - See [WebApp Search On The Front](https://developers.siteglide.com/search-and-filtering)

*   `type` - Should be `list`, for a List View layout. This can also be used to display different types of layouts, like a Cart in a different context. 

*   `show_pagination` - if pagination should be displayed after the products. Default is `'true'`&#x20;

# Folder Structure

In `SITE MANAGER/Code Editor`, the folder structure for eCommerce layouts is as below:

*   `layouts`
    *   `modules`
        *   `module_14
            `
            *   `product`
                *   `name_of_my_layout`
                    *   `list`
                        *   `wrapper.liquid`

                        *   `item.liquid`

                    *   `detail`
                        *   `wrapper.liquid`

                        *   `item.liquid
                            `

            *   `product_attributes`
                *   `my_attribute_layout.liquid`

## Creating a new set of Product Layouts

To create a new set of Product layouts- create your folder at the level of "name\_of\_my\_layout". Inside that, the folders and files should be created as shown above.

## List Layout Development

A list view for products is made up of two parts.

### wrapper.liquid

&#x20;wrapper.liquid -- list view example

```html
<div class="row">
  <div class="card-deck"> {%- include 'modules/siteglide_ecommerce/ecommerce/get/get_products'
                              item_layout: 'item' 
                          -%}
  </div>
</div>
```

The wrapper contains the code for the main part of the section you are building. For example, the section title or some margin or padding that separates your list from other sections.

In the wrapper.liquid file, it is important to include the liquid file which loops over the Product items:

```html
{%- include 'modules/siteglide_ecommerce/ecommerce/get/get_products'
    item_layout: 'item' 
-%}
```

The item\_layout parameter should be the name of a liquid file in the same folder as the current file. Usually this will be "item", but you could have an alternative Layout.

### item.liquid

&#x20;item.liquid -- list view example

```html
<div class="card">
  <div class="card-img">
    <a href="/{{this.module_slug}}/{{this.slug}}">
      <img src="{{this.Image | asset_url}}" alt="{{this.name}}" class="card-img-top">
    </a>
  </div>
  <div class="card-body">
    <a style="height: 100%" href="/{{this.module_slug}}/{{this.slug}}">
      <h3 class="card-title">{{this['name']}}</h3>
      <p>{{this.price.currency_symbol}}{{this.price.price_charge_formatted}}</p>
    </a>
  </div>
</div>
```

This file contains the code for each iteration of the loop that displays the Products. You should expect this code to be rendered multiple times; once for each product displayed in the list. (Hint: Try not to run any GraphQL calls inside a loop or item.liquid file, as they would have an impact on performance. It is better to run these inside the wrapper.)

As it is inside the loop, the item.liquid file has access to the "this" object and dynamic information specific to an individual product. A full reference for the fields you can use can be found [here](https://developers.siteglide.com/liquid-reference-for-product-and-attribute-layouts) or you may find it convenient to output the "this" object on the page you are developing:

Output all data available in the "this" object: `{{this | json}}`

# Adding to Cart on the List View

![](https://downloads.intercomcdn.com/i/o/202766316/777e7671a15e0108c77c9f0e/image.png)

## Update&#x20;

Previously, adding Products from a List View to the Cart was only partially supported.&#x20;

&#x20;What we did support on the List View:

*   Adding one of each Product at a time

What we now also support, with some small code changes:

*   Choosing the Quantity before adding to Cart

*   Choosing Attributes before adding to Cart

## Marking Separate Products to support the Advanced Features of Adding to Cart on a Product List View

In order to help the JavaScript understand which Quantity and Attribute Control belongs to which Product, we've added a new requirement to Product List Layouts. Please add the following data-attribute on the highest-level HTML element in your `item.liquid` file.&#x20;

In this example, the highest level element in the file is a `<div>` element which is wrapped around the rest of the content in the file, but yours could be any element. The important thing is that this element is wrapped around any controls in the File.

```html
<div class="card" data-product-group>
  <div class="card-img">
    <a href="/{{this.module_slug}}/{{this.slug}}">
      <img src="{{this.Image | asset_url}}" alt="{{this.name}}" class="card-img-top">
    </a>
  </div>
  <div class="card-body">
    <a style="height: 100%" href="/{{this.module_slug}}/{{this.slug}}">
      <h3 class="card-title">{{this['name']}}</h3>
      <p>{{this.price.currency_symbol}}{{this.price.price_charge_formatted}}   </p>
    </a>
  </div>
</div>
```

For old sites which do upgrade the eCommerce Module, but do not add this data-attribute, we'll add a console log in dev-tools to act as a reminder, but any functionality which worked previously will continue to work.

## Adding to Cart on the List View

As with Detail Layouts, you'll need to include the following Liquid and HTML code within the `item.liquid` file. It's also now important that these elements lie within the element with the `data-product-group` Attribute, when you're building a List Layout. See the section above for details.

***The "Add to Cart" Button
***`{% include 'ecommerce/cart_add' -%} `

***The Quantity Control***

```html
<input type="number" 
       min="1" 
       max="{{this.inventory.quantity}}" 
       data-quantity-control id="quantity" />  
```

This is mandatory, but can be hidden and hard-coded to have a value of 1, if you want to simplify the UI:

```html
<input readonly hidden type="number" 
       min="1" 
       max="1" 
       value="1"  
       data-quantity-control id="quantity" />
```

***Attribute Control
***As this code can be complex, so please refer to the [Attributes Layout ](https://developers.siteglide.com/attribute-layouts)doc for further information, or take a look at the full example below.

***Full Example:***
Example of an `item.liquid` file in a Product Layout which supports Adding to Cart:

```html
<div class="card" data-product-group>
    <div class="card-img">
        <a href="/{{this['module_slug']}}/{{this['slug']}}" 
           title="">
           <img src="{{this['Image'] | asset_url}}" alt="{{this['name']}}"></a>
    </div>
    <div class="card-body">
        <h2 class="card-title">
            <a href="/{{this['module_slug']}}/{{this['slug']}}" 
            title="">{{this['name']}}</a></h2>
        <p>{{this.price.currency_symbol}}{{this.price.price_charge_formatted}}</p>
    </div>
    {% include 'ecommerce/cart_add' -%}
    <label for="quantity">Quantity</label>
    <input type="number" min="1" value="1" data-quantity-control id="quantity" />
    {% comment %}-----The following liquid code block loops over all attributes on this Product
                 ----{% endcomment %}
    {% for attribute in this.product_attributes %}
      {% if attribute.properties.enabled == true %}
        {% include 'ecommerce/product_attributes'
                    name: attribute.properties.name
                    layout: 'demo_site_attributes' 
        -%} 
      {% endif %}
    {% endfor %}
    <div class="card-footer">
        <p class="tag">
            {% for category in this.category_array %}
                <a class="btn btn-primary" 
                href="{{context.exports.categories.items[category].full_slug}}" 
                title=""><i class="fas fa-tag">
                    </i>{{context.exports.categories.items[category].name}}
                </a>
            {% endfor %}
        </p>
    </div>
</div>  
```
