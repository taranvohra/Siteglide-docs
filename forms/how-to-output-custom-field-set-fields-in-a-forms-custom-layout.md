# 📋 Steps to Using Custom Field Set fields in a Form's Custom Layout

Custom Field Sets are a great time-saving feature, as they allow you to create a reusable group of fields that can be added to any:

* Form (for saving against Case and User in the CRM)
* eCommerce Product

In order to use Custom Field Sets, set them up in the Siteglide Admin: first you define the fields you would like to include in the set and second, you attach the Custom Field Set to a Siteglide Feature (from the list above).

Custom Field Sets will automatically include a hidden field Parent ID, which links them to the feature.

Default Form Layouts should be automatically updated with any Custom Field Set fields which have been added to the form in the Admin UI. However, custom Form Layouts will need further syntax.

## Prerequisites

Before reading this Article you should have already:

* Created a Custom Field Set
* Created a Form
* Added your Custom Field Set to the Form

## Introduction

This Article shows you the extra syntax needed to include Custom Field Sets in a custom Form Layout. Updating the Form in Admin will automatically add the Custom Field Sets to your `default.liquid` Layout, so these will not need any maintenance.

The easiest way to make sure your Custom Form Layout is displaying Custom Field Sets correctly may be to copy the code straight from your `default.liquid` Layout.

## Step 1) Identifying your Custom Field Set ID and Field ID

Each Custom Field set has an unique ID. You can find this ID by viewing the Custom Field Set in the Admin, and reading the last number in the URL.

Each field within that Custom Field Set also has it's own ID. You can work this out by the position of the fields in the List when you inspect your Custom Field Set in Admin.

In the example below- I have a Custom Field Set with an ID of 1 (displayed in the last slug of the URL)- and two fields:

<figure><img src="../.gitbook/assets/Screenshot 2024-05-20 175014.png" alt=""><figcaption><p>Noting the ID of the CFS and the field</p></figcaption></figure>

* Pizza Topping appears first in the List- so has an ID of 1
* Gelato appears second in the List, so has an ID of 2

## Step 2) Add code for each Custom Field Set Field to the Layout

The key HTML attribute will be located on different elements depending on the field type.&#x20;

Check the Reference to see the syntax for each type:

{% content-ref url="forms-reference.md" %}
[forms-reference.md](forms-reference.md)
{% endcontent-ref %}

If the type does not fit any of the types here, you can use text.

When it comes to adding the `data-cfs`HTML attribute, the first number should be the CFS ID and the second number the CFS Field ID. Finally, the type should be specified and preceded by the string "input\_".

E.g. `data-cfs="5-1-input_text"`
