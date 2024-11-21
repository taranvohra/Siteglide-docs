---
title: Liquid Reference for Product and Attribute Layouts
slug: Qd8v-
createdAt: 2021-02-18T15:09:17.000Z
updatedAt: 2023-04-06T15:09:36.000Z
---

# 🔹 Product Layouts

While building Product and Attribute Layouts, a large range of dynamic data is available- here is a full reference guide.

## "This" Object Fields

The "this" object can be accessed on Product detail/item.liquid, list/item.liquid and attribute layout files. It contains the properties of the current Product and contains further relevant objects e.g. Price.

The entire "this" object can be outputted on the page for reference: `{{this | json}}` The following fields are available:

| **Field Name** | **Liquid Tag**              | **Description**                                                                                                                                         |
| -------------- | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Item Name      | \{{this.name\}}             | The Product's name                                                                                                                                      |
| Item Slug      | \{{this.slug\}}             | The part of the URL for this Product's Detail Page which refers directly to this Product                                                                |
| Creation Date  | \{{this.create\_date\}}     | The date the Product was created in Admin                                                                                                               |
| Last Edit Date | \{{this.last\_edit\_date\}} | The date this Product was last edited in Admin                                                                                                          |
| Release Date   | \{{this.release\_date\}}    | The date this Product is scheduled for release, or was first released on the Site. (A Product will not appear in the list if it has not been released.) |
| Expiry Date    | \{{this.expiry\_date\}}     | The date this Product will be no longer visible on the Site. (A Product will not appear in the list if it has expired.)                                 |
| Enabled        | \{{this.enabled\}}          | A "true" or "false" boolean value. If "false", the Product will not appear in the list.                                                                 |
| Category Array | \{{this.category\_array\}}  | An array of ids of categories associated with this Product.                                                                                             |
| Description    | \{{this.Description\}}      | A description of the Product.                                                                                                                           |
| Image          | \{{this.Image\}}            | This is the main image for the Product, but more can be added with Custom Field Sets.                                                                   |

## Accessing Custom Field Sets

Custom Field Set data linked to Products is available in Product detail/item.liquid, list/item.liquid and attribute layout files.

Any Custom Field Sets that have been associated with the product will be stored under: `{{this.cfs_data}}`

You can output the above liquid in the item.liquid file to see all of Custom Field Sets associated with the Product. Each of these will have the key "cfs\_1", "cfs\_2" etc. For example, a developer has created just one Custom Field Set to store information about the Guarantee on the Product. The field can be accessed via: `{{this.cfs_data.cfs_1.Guarantee}}`

See more information about Custom Field Sets [here](https://help.siteglide.com/article/207-custom-field-sets).

## The Price Object

The Price object contains all the information you need to display the Product's price in the format you want. It is available in Product detail/item.liquid, list/item.liquid and attribute layout files.

| **Field Name**                    | **Liquid Tag**                                         | **Description**                                                                                                                                                                                                    |
| --------------------------------- | ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Price ID                          | \{{this.price.id\}}                                    | The unique ID of this Product's price.                                                                                                                                                                             |
| Product ID                        | \{{this.price.product\_id\}}                           | The unique ID of the Product this Price belongs to.                                                                                                                                                                |
| Currency                          | \{{this.price.currency\}}                              | The currency code for the currency used by this Product e.g. "GBP".                                                                                                                                                |
| Price Charge                      | \{{this.price.price\_charge\}}                         | The price of the Product as an integer e.g. for the price "£200.00" this field will display "20000"                                                                                                                |
| Display Price                     | \{{this.price.price\_display\}}                        | If the optional field Display Price was filled out when the Product was created, this will show that price as an integer, else, it will output null. This could be for example the RRP or price before tax.        |
| Currency Symbol                   | \{{this.price.currency\_symbol\}}                      | The HTML entity for the currency symbol. e.g. "£" outputted on the page will display "£" when HTML is rendered.                                                                                                    |
| Price Display Formatted           | \{{this.price.price\_display\_formatted\}}             | If the optional field Display Price was filled out when the Product was created, this will show that price as an decimal number, else, it will output null. This could be for example the RRP or price before tax. |
| Price Charge Formatted            | \{{this.price.original\_price\_charge\_formatted\}}    | This is the price that will be charged to the user, formatted into dollars and cents.                                                                                                                              |
| Price Charge Before Tax Formatted | \{{this.price.price\_charge\_before\_tax\_formatted\}} | This is the price before any tax is applied, formatted into dollars and cents.                                                                                                                                     |

## The Inventory Object

The Inventory object contains the fields related to the current Inventory of this Product. It is available in Product detail/item.liquid, list/item.liquid and attribute layout files.

| **Field Name** | **Liquid Tag**                       | **Description**                                                                                                                                |
| -------------- | ------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Inventory ID   | \{{this.inventory.id\}}              | The unique ID of the object containing the Product's Inventory.                                                                                |
| Enabled        | \{{this.inventory.enabled\}}         | A "true" or "false" boolean, defaults to true.                                                                                                 |
| Product ID     | \{{this.inventory.product\_id\}}     | The unique ID of the Product this Inventory Object belongs to.                                                                                 |
| Quantity       | \{{this.inventory.quantity\}}        | The number of products in the inventory.                                                                                                       |
| Inventory Type | \{{this.inventory.inventory\_type\}} | The type of Inventory. Currently, only "Global" is available.                                                                                  |
| Display Type   | \{{this.inventory.display\_type\}}   | This stores the policy on what to do when the Inventory reaches zero. Either the Product can not be ordered, or it should be hidden from view. |

## The Attributes Object

These are available once Attributes have been added against the Product in Admin and you are inside a detail/item.liquid file or an Attribute layout file.

You can access the Attributes Object via the following liquid output: `{{ this.product_attribute_options }}`

### Inside the Attribute Layout

#### Output Options for this Layout

Inside the Attribute Layout, you can access just the Options for that specific Attribute: `{{ product_attribute_options }}`

#### Output this Attribute's Name

You can also access the name of the Attribute this Layout is currently displaying: `{{this_attribute.properties.name}}`

#### Looping Over Attribute Options and Accessing Option Fields

As explained in the Attributes Layout Doc, we recommend you loop over the object and access the fields via the "option" liquid variable.

```liquid
<select name="attr1" class="form-control" data-attribute-control="{{product_attribute_id}}" onchange="s_e_update_price()">
  {% raw %}
{% for option in product_attribute_options %}
    <option value="{{option.id}}" data-attribute-price-control="{{option.price_raw}}">{{option.name}} this.price.currency_symbol}}{{option.price}})</option>
  {% endfor %}
{% endraw %}
</select>


```

Assuming the above example liquid forloop has been implemented, you can access the fields in the table below. Remember the "option" liquid variable can be renamed, so if you have done this, replace "option" with the name you have given the variable. The Object contains Attribute Options and each of these contains information on the Attribute it is linked with.

| **Field Name**                             | **Liquid Tag**                                | **Description**                                               |
| ------------------------------------------ | --------------------------------------------- | ------------------------------------------------------------- |
| Attribute Option ID                        | \{{ option.id \}}                             | The unique ID of this Attribute Option                        |
| Attribute Option Name                      | \{{ option.name \}}                           | The name of this Attribute Option                             |
| Attribute Option Chargable Price           | \{{ option.price\_charge \}}                  | Chargable price for this Attribute Option                     |
| Attribute Option Chargable Price Formatted | \{{ option.price\_charge\_formatted \}}       | Formatted chargable price for this Attribute Option           |
| Attribute Option Display Price             | \{{ option.price\_display \}}                 | Display price for this Attribute Option                       |
| Attribute Option Display Price Formatted   | \{{ option.price\_display\_formatted \}}      | Formatted display price for this Attribute Option             |
| Attribute Option Image                     | \{{ option.image\}}                           | The image for this Attribute Option                           |
| Attribute ID                               | \{{ option.product\_attribute.id \}}          | The Unique ID of this Attribute                               |
| Attribute Name                             | \{{ option.product\_attribute.name \}}        | The Name of the Attribute e.g. Size or Colour                 |
| Attribute                                  | \{{ option.product\_attribute.product\_id \}} | The Unique Product ID that this Attribute is associated with. |

## Volume Pricing

Information about how to output information about volume pricing can be found here:

{% content-ref url="../volume-pricing.md" %}
[volume-pricing.md](../volume-pricing.md)
{% endcontent-ref %}
