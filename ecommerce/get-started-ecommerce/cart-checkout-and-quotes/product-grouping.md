---
title: >-
  How can I set up Product grouping and allow customers to switch views to
  another Product in the group?
slug: TfVM-
createdAt: 2021-02-18T13:08:26.000Z
updatedAt: 2023-04-11T07:38:27.000Z
---

# 📋 Steps - Alternatives to Product Grouping

## Prerequisites

In this tutorial we'll be using both Categories and Collections, if you're unfamiliar with either of these we'd recommend refreshing your memory:

* [Categories - Introduction](/cms/categories/quickstart-categories.md)
* [Webapp Collections](/developer-tools/liquid/using-collections-with-webapps-and-modules.md)

## Introduction

Often in eCommerce, you will have Products that are similar to one another. e.g. You might have a brand of chocolate with certain different flavours available. Or you might have different sized packs.

### What are Product Attributes?

On Siteglide, we provide the Attributes feature- which allows you to merge these multiple varieties into a single Product with options. Users choose which Attributes to select as they add the Product to the Cart, and the Price can be adjusted accordingly. [outputting them as options Front End](/ecommerce/get-started-ecommerce/cart-checkout-and-quotes/product-views/attribute-selection/attribute-layouts.md).

### What was Product Grouping?

Adobe Business Catalyst, on the other hand, also allowed Users to "group" these similar Products instead. Product Grouping treated the Product variations as separate entities which could show up in Product Lists independently. Meanwhile, the Product Detail Page for one variation would display a list of alternate Products in the group, allowing you to switch to view the different information. Many partners have expressed an interest in re-creating this Product Grouping feature on their Siteglide Site.

There are several ways to achieve this:

* Use Categories to group the Products
* Use Datasources to build a relationship between a Product and similar Products in the Group
* Convert an existing Product Grouping setup to use single Products with [Attributes](/ecommerce/get-started-ecommerce/cart-checkout-and-quotes/product-views/attribute-selection/attribute-layouts.md) instead.

In this Article, we'll demonstrate how to group the products using Categories.

## How to use Siteglide Categories to build a Product Grouping eCommerce Site

### Step 1) Create a Category for the Group

First, create a Category that will link the products together.

If you will also have some non-grouped Products, you may wish to create a "Product Groups" Category as well as a parent to organise all your product grouping Categories inside- bellow I'll explain how you can ensure that only Categories within the parent Category are used.

Here's how I've structured my Categories, "Chocolate" and "Crisps" each represent separate groups of Products, the parent Category "Product-group" will be used to identify them as Product grouping Categories, allowing you to keep them separate from the other Categories your Products may have:

Now let's look at how we can ensure only the Categories within "Product-group" are used when outputting our related Products. First I assign an object containing all the Categories on my Site (this gives us access to all the Categories fields, rather than just the ID):

```liquid
{% raw %}
{% assign categories = context.exports.categories.items %}
{% endraw %}
```

Next loop over all of our Products categories, at each iteration we'll store the "full\_slug" of the Category (this will include the parent Categories slug, which we can use to check the Category is being used for Product grouping).

Note: "this" contains one of the Category IDs assigned to our Product, we then use that ID to find all of the Categories details in "`context.exports.categories.items`":

```liquid
{% raw %}
{% for category in this.properties.category_array %} 
  {% assign full_slug = categories[category].full_slug | split: '/' %}
{% endfor %}
{% endraw %}
```

We've now created an array of all the individual "parameters" in our "full\_slug" field, next we'll loop over this and check none of the parameters equal "product-group"- if they do then we know that Category is being used for Product Grouping and store its ID. Add this code to the for loop above:

```liquid
{% raw %}
{% for category in this.properties.category_array %} 
  {% assign full_slug = categories[category].full_slug | split: '/' %}
  {% for p in param %}
    {% if p == "product-group" %}
      {% assign group_category = this %}
    {% endif %}
  {% endfor %}
{% endfor %}
{% endraw %}
```

This will check all of the parameters, make sure you replace "product-group" with whichever slug your wrapping Category is using. If it is a Product grouping Category, we store the ID in the variable "group\_category". We'll use this ID later to output our Related Products.

### Step 2) Add the Group Category to all Products in the Group

Now add all the related Products to this Category. You can do this in the Categories tab when editing your Product. In this example- we'll be selecting the "Crisps" Category to add to our "Ready Salted" flavour Product.

Repeat step 2 for all the Products you'd like to be linked together.

### Step 3) Output the Related Products on the Product Detail Page

On the Detail Page of each Product in the group, we'll next need to List the other Products in the group.

There are now two ways we could output the related Products. You can choose one of the following methods:

* Include the other Products in group by nesting a filtered Product List Layout inside the Product Detail Layout.
* Keep all the code tidy inside the Detail Layout using a Collection to fetch the same data.

We'll demonstrate how you can use method 3) b).

#### Option 3) a) Output the Related Products within a List Layout

If you'd like to use a separate Layout to output your products, add this include to the Layout you're working in:

```liquid
{% raw %}
{% for category in this.properties.category_array %} 
  {% assign full_slug = categories[category].full_slug | split: '/' %}
  {% for p in param %}
    {% if p == "product-group" %}
      {% assign group_category = this %}
    {% endif %}
  {% endfor %}
{% endfor %}
{% endraw %}



{%- include 'ecommerce/products'
    layout: 'custom_layout'
    per_page: '20'
    show_pagination: 'true'
    sort_type: 'properties.name'
    sort_order: 'asc'
    category_ids: group_category
    type: 'list' 
-%}

```

...where `group_category` contains the ID of the category containing the related Products. In your chosen Layout, you would be able to add Content regarding the Related Products.

#### Option 3) b) Output the Related Products within a Collection

Now we know which Products are related to one another, we can output them. For this demo, I'll be outputting them within the Detail Layout.

To do this we'll use a Collection (read more here: [Collections](/developer-tools/liquid/using-collections-with-webapps-and-modules.md)) which will be filtered by the parameter "category\_id", meaning only items within the specified category are included (please follow step 1 for instructions on how we can do this dynamically).

```liquid
{%- include 'ecommerce/products'
    layout: 'default'
    per_page: '20'
    show_pagination: 'true'
    sort_type: 'properties.name'
    sort_order: 'asc'
    category_ids: 'category_id'
    type: 'list'
    collection: 'true' 
-%}



```

If you're in a Detail layout, make sure to include the `type: 'list'` parameter. Also, ensure `collection: 'true'` is added to the include, along with your Category ID.

### Create an object containing the included Products

The Collection will call all the specified items into `{{context.exports}}`, to save us writing the whole path to the item each time we output something, we'll store them in an Object:  
`{% raw %}{% assign items = context.exports['module_14/product'].data.result.items %}{% endraw %}`

Now loop over the object, at each iteration we'll check that the ID doesn't equal the ID of the Product being displayed on the Detail Page (this will stop the Product on the Detail page being displayed as related). We'll use `{{this.id}}` to do this:

```liquid
{% raw %}
{% for item in items %}
  {% if item.id != this.id %}
    <!-- Add content relating to the Related Product here -->
  {% endif %}
{% endfor %}
{% endraw %}


```

## Step 4) Optional - Output the Related Products within a dropdown

Many partners who have expressed interest in the Product Grouping feature have also requested a demonstration of how to include a dropdown menu which allows easy access to links to other products in the Product group.

As always when using custom JavaScript, you may wish to adjust the simplified examples in order to add in improvements to SEO and accessibility.

#### Option 4) a) Using a Collection method _if you followed step 3) a) above_

For this demo, I've chosen to output my Related Products using `<select> & <option>`, and some Javascript that will redirect the Page.

```liquid
{% raw %}
<label for="options">Related Products</label>                          
<select name="options" class="form-control" onChange="handleOption(this)">
  <option>---Select alternative Product---</option>  
  {% for item in items %}
    {% if item.id != this.id %}
      <option value="/{{item['module_slug']}}/{{item['slug']}}"> 
      {{item.name}}</option>
    {% endif %}
  {% endfor %}                          
</select>
{% endraw %}
```

This will output `---Select alternative Product---` as the placeholder for the options, then will loop over all the items in the Object we've just created, each iteration will output another `<option>` where the value contains a relative link to that Products Detail Page.

Lastly, we'll need to add the Javascript for the "handleOption" function above, this will simply redirect to the slug within the options value attribute:

```javascript
<script>
  function handleOption(elm) { 
    window.location = elm.value; 
  } 
</script>
```

#### Option 4) b) Including a separate Product List Layout if you followed step 3) b) above

If you used the method 3) b) above, you'll need to move some of the code from 4) a) inside the products Layout.

#### Wrapper

Make sure your Wrapper still includes the items inside the `<select>` element:

```liquid
{% raw %}
<label for="options">Related Products</label> 
<select name="options" class="form-control" onChange="handleOption(this)">
  <option>---Select alternative Product---</option>  
  {%- include 'modules/siteglide_ecommerce/ecommerce/get/get_products', item_layout: 'item' -%}
</select>
{% endraw %}
```

#### Item

The HTML and Liquid for each option should then be included inside the `item.liquid` file: `<option value="/{{item['module_slug']}}/{{item['slug']}}">{{item.name}}</option>`

### Add JavaScript

As above, you'll need to include a JavaScript function to make the dropdown functional.

```javascript
<script>
  function handleOption(elm) { 
    window.location = elm.value; 
  } 
</script>
```

## The Solution

Alright, that's everything we need to link our Products. Here is a screenshot of the solution:
