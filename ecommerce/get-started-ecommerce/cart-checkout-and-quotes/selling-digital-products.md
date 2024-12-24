---
title: How to Sell Digital Products
slug: bMsv-
createdAt: 2021-02-18T14:27:17.000Z
updatedAt: 2023-04-11T07:33:27.000Z
---

# Selling Digital Products

In this article I'll explain how you can use our Media Download and eCommerce Modules to sell digital products

Prerequisites

* You have installed the [Secure Zone](/crm/quickstart-crm.md) Module's latest version
* You have installed the [Media Downloads](https://help.siteglide.com/article/131-modules-getting-started#2-introduction) and [eCommerce Modules](https://help.siteglide.com/article/200-getting-started-with-siteglide-ecommerce)
* You have created [Products](https://help.siteglide.com/article/196-products-introduction).
* You have followed our document on [Cart, Checkout and Orders Flow with the Secure Zone Module](/ecommerce/get-started-ecommerce/cart-checkout-and-quotes/how-to-set-up-a-shopping-cart-and-guest-checkout-tutorial.md)

## Introduction

In this article, I'll explain how you can datasource to a Media Download Item to a Product- allowing the Product to be downloaded after it has been purchased.

To ensure that the Media Download can only be accessed after the Product has been purchased we'll output it within a User Orders Layout.

## Create a Media Download Item

Firstly, let's create our downloadable Product, to do this we'll create a new Media Download Item, you'll need to repeat this step for every product that can be downloaded. We'll be using an image for this example, but you can use any file type that the Media Download Module supports:

## Add Datasource Field to your Products

Now we've added our downloadable product, let's Datasource it to the Product it is related to, we'll need to add a new Custom Field to our Products- to do this go to: eCommerce > Products > Edit Module Structure.

Then add a new field and set the type to 'Datasource (Single item)':

Finally, let's link each of our Media Download items to the Products they're associated with, to do this head to eCommerce > Products > Your product > Custom Fields. You should see a dropdown containing all the Media Download items, select the one that matches your Product:

## Output the Media Download link within your User Orders layout

Now we've got everything needed for our Products to be downloadable, let's output the download somewhere it can only be accessed after being purchased.

Locate the \`user\_orders\` layout within the Secure Zone Module: Code Editor > Modules > Module\_5 (Secure Zones) > user\_orders.

Within this layout we'll have access to the \`orders\` object, containing all of the User's previous purchases, this should also contain a `order_products` (old) or `order_products_flat` (new) object (depending on your eCommerce Module version) within each order. This contains information about the Product purchased, we'll have access to the Media Download Item ID from here.

We can output the Products data like so

```liquid
{% raw %}
{%- for this in orders -%}

  {{this.order_products[0].product.properties}}

{%- endfor -%}
{% endraw %}




```

However, we just need the Media Download Item ID which can be outputted like so, if you have other Custom Fields you'll need to replace 'product\_1' with the field name

```liquid
{% raw %}
{%- for this in orders -%}

{%- assign media_download_id = this.order_products[0].product.properties['module_field_custom_14/product_1'] -%}

{%- endfor -%}
{% endraw %}




```

If there are multiple Products in one Order, we'll need to create an array of the Media Download Item IDs for each Product, we'll nest another loop within the loop above over \{{orders\}} - here's how this would look:

```liquid
{% raw %}
{%- assign media_download_id = '[]' | parse_json -%}

{%- for this in orders -%} 
 
  {% for model in this.order_products%}
       
    {%- assign media_download_id = media_download_id | add_to_array: model.product.properties['module_field_custom_14/product_1'] -%}
      
  {% endfor %}

  {%- assign media_download_id = media_download_id | join: ',' -%}

{%- endfor -%}
{% endraw %}


```

So no we've assigned all of our Media Download IDs to '`media_download_id`'- we'll use this within the 'item\_ids' parameter on our Media Download Layout include:

```liquid
{%- include 'module'
    id: '17'
    layout: 'my-layout'
    item_ids: media_download_id 
-%}


```

Now, locate your Media Download layouts- these can be found under: Code Editor > Modules > Module\_17 (Media Downloads).

From here you can either use an existing layout or copy the default layout structure to create your own (ensure you've added a 'list' folder within the folder for your layout, the 'list' folder should then contain item and wrapper layouts).

We'll only need to include the Media Download Items within the 'wrapper' file, here's how this looks:

```liquid
{%- include 'modules/siteglide_media_downloads/get/get_items'
    item_layout: 'item' 
-%}
```

Then within the 'item' layout, we'll add an anchor to allow the items to be downloaded- we'll also output the name of the Media Download Item as the anchor's text: `<p><a href="{{this['url']}}">{{this['name']}}</a></p>`
