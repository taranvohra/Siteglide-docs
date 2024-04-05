---
title: Outputting Related Products
slug: B2Kt-
createdAt: 2021-02-19T11:33:08.000Z
updatedAt: 2023-04-06T15:08:02.000Z
---

How to use Module Custom Fields to output similar, related products

![](https://downloads.intercomcdn.com/i/o/282006861/82f4131eb2ac45152fa9e3b8/image.png)

# Pre-requisites&#x20;

*   Your [eCommerce Module](https://help.siteglide.com/article/200-getting-started-with-siteglide-ecommerce) is updated to at least version 1.2.0

*   You have already [created eCommerce Products](https://help.siteglide.com/article/196-products-introduction) and outputted them in List or Detail Layouts on the Site

# Introduction

Module Custom Fields allow a wide range of use cases for connecting up different areas of your Site.&#x20;
In this Article we'll look at how you can create a new Custom Field for your eCommerce products to store similar, related Products which could be displayed on the Product's Detail Page.

You could of course use this same technique with the Blog Module or any other Module or WebApp.&#x20;

# Step By Step

## Step 1) Add a new Custom Field to Products

&#x20;To add a Custom Field to Products, first select Edit Module Structure from the Products List in Admin.

![](https://downloads.intercomcdn.com/i/o/281984488/5ab9d9681291cb70dde3d46c/image.png)

At the bottom of the available fields, you can find the Custom Fields section, and press the "Add new field" button.

![](https://downloads.intercomcdn.com/i/o/281984986/aed1745b9182c9e7edff26db/image.png)

The name of your field can be whatever you want, here we'll call it Related Products.
The Datasource Multi type prompts us to choose a Module or WebApp that we will be able to select Items from.

![](https://downloads.intercomcdn.com/i/o/281985832/a72882b3c513f02cc2a4f086/image.png)

When you're ready, press save and your new Custom Field will be set up. You'll then be able to use this field when creating and editing Products.

## Step 2) Add related Products to a Product

In this example, we'll edit the new Custom Field on an existing Product to create a relationship with another Product.
From the Product Edit Page, select the Custom Fields tab:

![](https://downloads.intercomcdn.com/i/o/281987097/8e3642f605365b4746aa0832/image.png)

As we used the Datasource Multi field type and selected Products as the Module to be linked to, Siteglide knows what we're trying to do and will help us find the related Items. By clicking in the select box and starting to type "Crow" I should be able to find other Products with a similar name to this band easily.&#x20;

![](https://downloads.intercomcdn.com/i/o/281988102/152a8e8eba1012153c651ff0/image.png)

Select as many as you need. Each Product's unique ID will be stored in array format in your Custom Field.&#x20;

![](https://downloads.intercomcdn.com/i/o/281988481/48748f56ec8636e028fdc9c2/image.png)

When you're ready, save the Product.

## Step 3) From the Product Detail Layout access the Related Product IDs

&#x20;For the next steps (3 - 6), we'll be navigating to Code Editor to develop custom Layouts to display the Related Products Front End. We'll start by working in the "item.liquid" file of the Layout you're using for the Product Detail View. We'll nest a new List of Related Products inside this Detail Layout.

![](https://downloads.intercomcdn.com/i/o/281989251/855f8a163df27a3811a6f93c/image.png)

Inside the item.liquid file, we can access the Custom Field by name:

```html
<h2>Related Products</h2><br><br>
{{this['Related Products']}}<br><br>
```

&#x20;This outputs an array of the IDs of each of the related Products stored against our current Product. It should look something like this: `["55","75","147"]`

## Step 4) Convert the Related Product IDs to a comma-separated String format

&#x20;In Step 5, we'll need to nest a new List Layout of Products inside the Detail Layout and filter this by the IDs of our Related Products. However, the IDs are currently in an Array format and the `{% include %}` tag's `item_ids` parameter expects a comma separated String.

We can change the type by assigning a new variable:`{% assign related_products = this['Related Products'] | join: "," %}`

## Step 5) Add a Product List Layout which Datasources to the Related Products

&#x20;Next, we need to output a Product List, nested within our existing Product Detail Layout.&#x20;

```html
<h2>Related Products</h2>
{% assign related_products = this['Related Products'] | join: "," %}
{%- include 'ecommerce/products'
    layout: 'default'
    per_page: '3'
    show_pagination: 'false'
    sort_type: 'properties.name'
    sort_order: 'asc'
    datasource: 'true'
    item_ids: related_products 
-%} 
```

***Item Ids Parameter***
Without the `item_ids` parameter, our List outputs only the first few Products alphabetically, instead of fetching our dynamic Related Products.&#x20;

We can change that by adding the item\_ids parameter and feeding in our comma-separated String of IDs (that we stored in a new Liquid variable):`item_ids: related_products`

***Datasource Parameter
***`datasource: 'true'
`When you output an include inside a Detail Layout, by default Siteglide will try to fetch a Detail Layout. This is one reason why it's important to set the `datasource: 'true'` parameter, which will then cause Siteglide to look for a List type Layout.

Another benefit of the `datasource: 'true'` parameter is that if no Related Product IDs are available, the List will return empty, instead of returning an unfiltered List. This prevents the List from showing unrelated Products in this situation.

***Per Page Parameter
***`per_page: '3'
`In the example, the per\_page has been set to 3. In some cases, you may wish to limit the number of "related" results in this way, so they don't distract from the main subject of the Page. It is completely optional.

***Layout Parameter
***Select the name of a Product List Layout you'll use to style how the dynamic Related Products List will look (see Step 7).

## Step 6) Hide content when no Related Products exist

&#x20;Optionally, you can add Liquid logic to only display the subtitle and Related Products content when the field is not empty.
As the field contains an array, a safe way to check if it holds a value is to check its size (Liquid for the length of the array).&#x20;

```html
{% if this['Related Products'].size > 0  %}
  <h2>Related Products</h2>
  {% assign related_products = this['Related Products'] | join: "," %}
  {%- include 'ecommerce/products'
      layout: 'default'
      per_page: '3'
      show_pagination: 'false'
      sort_type: 'properties.name'
      sort_order: 'asc'
      datasource: 'true'
      item_ids: related_products 
  -%} 
{% endif %}
```

## Step 7) Optional - Develop a Custom Layout for the Related Products

&#x20;You can style and write Liquid for the Related Products List Layout in the same way you do for any [Product List](https://developers.siteglide.com/list-layouts). For example, you could provide a link to the Detail Pages of those Related Products using the Slug property.&#x20;

You've now completed the Step by Step guide for adding Related Products.&#x20;