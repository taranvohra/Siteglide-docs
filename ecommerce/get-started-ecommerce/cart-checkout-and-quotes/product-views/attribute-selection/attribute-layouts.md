---
title: Attribute Layouts
slug: QdZn-
createdAt: 2021-02-18T16:28:25.000Z
updatedAt: 2023-04-06T15:17:02.000Z
---

# 🔹 Attribute Layout - Presenting the Choice to the Customer

Product Attribute Layouts allow you to customise the way that you present users with a choice of which variation of a Product they want.

Product Attribute Layouts allow you to customise the way that you present users with a choice of which variation of a Product they want.

## Prerequisites

* You have [created Products](https://help.siteglide.com/article/196-products-introduction) in the Admin
* You have [created a Product Detail View](https://developers.siteglide.com/detail-layouts)

## Introduction

This Tutorial will show you how to use Attributes to let Users pick Variants on the Product's automatically-generated Detail Page.

It will cover how to:

* Find where Product layouts are stored on Code Editor
* Develop a my\_attribute\_layout.liquid file
* Allow the User to select Attribute Options before adding to Cart

## Folder Structure

In `SITE MANAGER/Code Editor`, the folder structure for product attributes layouts is as below:

```
marketplace_builder
└───views
    └───partials
        └───layouts
            └───modules
                └───module_14
                    ├───product
                    │   collection.liquid
                    │   └───custom_product_layout
                    │       ├───detail
                    │       │   item.liquid
                    │       │   wrapper.liquid
                    │       └───list
                    │           item.liquid
                    │           wrapper.liquid
                    └───product_attributes
                        └───custom_attributes_layout.liquid
```

See a more complete Cart & Checkout Folder Structure here:

{% content-ref url="../../../cart-and-checkout-folder-structure.md" %}
[cart-and-checkout-folder-structure.md](../../../cart-and-checkout-folder-structure.md)
{% endcontent-ref %}

### Creating a new set of Product Layouts

To create a new set of Product layouts- create your folder at the level of "name\_of\_my\_layout". Inside that, the folders and files should be created as shown above.

## Including a Single Known Attribute on a Detail Page

If you are making a layout where you know exactly which Attribute a Product has, you can include an Attribute layout to display an Attribute with a given name: `detail/item.liquid` (including a single Attribute)

```liquid
{% include 'ecommerce/product_attributes'
   name: attribute
   layout: 'demo_site_attributes'
   attribute_name: "Size" 
-%}


```

## Looping Over Multiple Attributes

If your Products have multiple Attributes, or you want to write code which can dynamically display any Attribute given to the Product, you can use liquid to loop over all Attributes. We've recently updated this example to be much simpler and easier to use.

### Steps:

1. Loop over all Attribute Options
2. Check if the Attribute is enabled
3. If so, include the relevant Attribute layout, dynamically filling in the "name" parameter.

### Full example:

`detail/item.liquid` -- (looping over all Attributes linked to this Product)

```liquid
{% raw %}
{% for attribute in this.product_attributes %}
  {% if attribute.properties.enabled == true %}
    {% include 'ecommerce/product_attributes'
       name: attribute.properties.name
       layout: 'demo_site_attributes' 
    -%} 
  {% endif %}
{% endfor %}
{% endraw %}




```

## Attribute Layout Development

There is no need to create a wrapper file for Attributes, as they are already included inside an item.liquid file. Your Attribute layout can be given a name of your choice. Different Attributes for the same Product may use different Attribute layouts, e.g. "Colour" may include colour swatches.

You can output the name of the Attribute that the current Layout displays: `{{this_attribute.properties.name}}`

The following liquid outputs an array of the options that have been created for this Attribute: `{{product_attribute_options}}`

You can loop over this array with the following liquid code, (where the example has the variable "option", you could choose any variable name):

```liquid
{% raw %}
{% for option in product_attribute_options -%}
  {{option.name}} ({{this.price.currency_symbol}}{{option.price}})
{% endfor %}
{% endraw %}




```

To get the full benefits of Attribute functionality, including the user's choice of Attribute affecting what is added to the Cart, the data-attributes and function calls in the example should be included:

```liquid
<select name="attr1" class="form-control" data-attribute-control="{{product_attribute_id}}" onchange="s_e_update_price()">
  
{% raw %}
{% for option in product_attribute_options %}
    <option value="{{option.id}}" data-attribute-price-control="{{option.price_raw}}">
      {{option.name}} {{this.price.currency_symbol}}{{option.price}})
    </option>
  {% endfor %}
{% endraw %}
</select>
```

As you can see in the example, inside the loop it is possible to access the specific Attribute Option in this iteration via the "option" variable you created when setting up the loop, but you can also still access the "this" object specific to the Detail Layout that wraps around and includes the Attribute Layout. See the [Product Layout Liquid Reference](https://developers.siteglide.com/liquid-reference-for-product-and-attribute-layouts) to see the fields available in the "this" object and those specific to Attributes and Attribute Options.
