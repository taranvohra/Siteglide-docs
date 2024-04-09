---
title: How do I get the Name or other details of a Product to Change when an Attribute is selected?
slug: Prx6-
createdAt: 2021-02-19T15:38:05.000Z
updatedAt: 2023-03-03T08:10:04.000Z
---

When a User selects a Product Attribute, the Price changes, but what if you want to change the Product Name or Product Code?

# Answer

![](https://downloads.intercomcdn.com/i/o/197120935/ed05f68ec92f7466ffeb0342/image.png)

*Step 1) HTML - Add an element at the end of the name. We'll be targeting this by its ID and we'll be changing its content later:
*`<h1>{{this['name']}} <span id="selectedAttribute"></span></h1>`

*Step 2) Liquid - Make sure the Attributes are correctly outputted on the Product Detail Page, then inside the \<option> element in the Layout, add a data-attribute containing the field you want to use to update the Name. *

```liquid
{% raw %}
<!-- Add data-option-name="{{option.name}}" -->

<option value="{{option.id}}" 
        data-option-name="{{option.name}}" 
        data-attribute-price-control="{{option.price_raw}}">
        {{option.name}} 
        {% unless option.price == "0.00" %}
        ({{this.price.currency_symbol}}{{option.price}})
        {% endunless %}
        </option>
{% endraw %}
```

For a reminder on how to output Attribute Layouts correctly, check out the doc [here](https://developers.siteglide.com/attribute-layouts)

*Step 3) JavaScript - Add it to the wrapper.liquid Layout, or before the end of the \</body> tag.*

```javascript
<script>
  function updateName() {
    var selectedAttribute = document.querySelector("[data-attribute-control]").selectedIndex;
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

## Solution

When the Attribute Changes, or the Page is loaded, the JavaScript finds the name of the currently selected Attribute. It changes the textContent of our new \<span> element to have the value of the Attribute's name. 