---
title: >-
  How do I get the Name or other details of a Product to Change when an
  Attribute is selected?
slug: Prx6-
createdAt: 2021-02-19T15:38:05.000Z
updatedAt: 2023-03-03T08:10:04.000Z
---

# 📋 Steps to Change Product Details after a Customer Selects an Attribute

When a User selects a Product Attribute, the Price changes, but what if you want to change the Product Name or Product Code?

## Step 1) Add HTML selectors in the product item.liquid detail layout file

Add an element at the end of the name. We'll be targeting this by its ID and we'll be changing its content later:&#x20;

{% tabs %}
{% tab title="product/custom_layout/detail/item.liquid" %}
```liquid
<h1>{{this['name']}} <span id="selectedAttribute"></span></h1>
```
{% endtab %}
{% endtabs %}

## Step 2) Add a data-attribute to options to store the suffix you which to append to the Product title when this is selected

&#x20;Make sure the Attributes are correctly outputted on the Product Detail Page, then inside the \<option> element in the Attributes Layout, add a data-attribute containing the field you want to use to update the Name.&#x20;

{% tabs %}
{% tab title="product_attributes/custom_layout.liquid" %}
```liquid
<option value="{{option.id}}" 
        data-option-name="{{option.name}}" 
        data-attribute-price-control="{{option.price_raw}}">
        {{option.name}} 
        {% raw %}
{% unless option.price == "0.00" %}
        ({{this.price.currency_symbol}}{{option.price}})
        {% endunless %}
{% endraw %}
</option>
```
{% endtab %}
{% endtabs %}

For a reminder on how to output Attribute Layouts correctly, check out the doc [here](attribute-layouts.md)

## _Step 3) Add a JavaScript Event Listener and Callback Function_

{% hint style="info" %}
:genie: If you're using SiteBuilder eCommerce layouts which leverage the Live Updates API, the page will not reload when an Attribute is changed. You may need to use a "change" event instead and figure out which option currently has the "selected" property, rather than relying on the selected attribute.&#x20;
{% endhint %}

```javascript
<script>
  function updateName() {
    var selectedAttribute = document.querySelector("[data-attribute-control]");
    var attributeOptions = document.querySelectorAll("[data-attribute-control] option");
    var selectedAttributeName = attributeOptions[selectedAttribute].getAttribute("data-option-name");
    var newName = document.querySelector("#selectedAttribute");
    newName.textContent = selectedAttributeName;
  }
  window.addEventListener('load', 
  function() { 
    updateName();
    var selectedAttribute = document.querySelector("[data-attribute-control]");
    selectedAttribute.addEventListener("change", updateName);
  }, false);
</script>
```

### Solution

When the Attribute Changes, or the Page is loaded, the JavaScript finds the name of the currently selected Attribute. It changes the textContent of our new \<span> element to have the value of the Attribute's name.
