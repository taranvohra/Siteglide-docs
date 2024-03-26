# How to output Custom Field Set fields in a Form's Custom Layout

Default Form Layouts should be automatically updated with Custom Field Set fields. However, custom Form Layouts will need further syntax.

## Prerequisites

Before reading this Article you should have already:

* Created a [Custom Field Set](https://help.siteglide.com/article/207-custom-field-sets)
* Created a [Form ](https://help.siteglide.com/article/99-forms-getting-started)
* Added your Custom Field Set to the Form

## Introduction

This Article shows you the extra syntax needed to include Custom Field Sets in a custom Form Layout. Updating the Form in Admin will automatically add the Custom Field Sets to your `default.liquid` Layout, so these will not need any maintenance.

The easiest way to make sure your Custom Form Layout is displaying Custom Field Sets correctly may be to copy the code straight from your `default.liquid` Layout.

### Identifying your Custom Field Set

Each Custom Field set has an unique ID. You can find this ID by viewing the Custom Field Set in the Admin, and reading the last number in the URL.

Each field within that Custom Field Set also has it's own ID. You can work this out by the position of the fields in the List when you inspect your Custom Field Set in Admin.

In the example below- I have a Custom Field Set with an ID of 5 (displayed in the last slug of the URL)- and two fields:

* Pizza Topping appears first in the List- so has an ID of 1
* Gelato appears second in the List, so has an ID of 2

![](https://downloads.intercomcdn.com/i/o/179982454/6fb960ab529d9a53943d1153/image.png)

## Syntax

We'll structure the sections of the Article by the type of field which needs to be displayed, because the key HTML attribute will be located on different elements depending on the field type. If the type does not fit any of the types here, you can use text.

When it comes to adding the `data-cfs`HTML attribute below, the first number should be the CFS ID and the second number the CFS Field ID. Finally, the type should be specified and preceded by the string "input\_".

E.g. `data-cfs="5-1-input_text"`&#x20;

### Text

A text input should have the `data-cfs` attribute inside the `<input>` element.&#x20;

```html
<input
    class="form-control"
    name="{{ form_builder.fields.properties.form_field_13_1.name }}"
    data-cfs="5-1-input_text"
    type="text"
/>
```

### Textarea

The same applies for textarea inputs.

```html
<textarea
    class="form-control"
    name="{{ form_builder.fields.properties.form_field_13_6.name }}"
    data-cfs="5-4-textarea"
    rows="5"
    cols="30"
></textarea>
```

### Checkbox

A Checkbox group should have the `data-cfs` attribute on the container for the entire group. `<input>` elements should be the grandchildren of this group.&#x20;

```html
<div class="checkbox-container" data-cfs="6-1-input_checkbox">
  <div class="checkbox">
    <input
      id="form_field_13_3_Rare"
      name="{{ form_builder.fields.properties.form_field_13_3.name }}[]"
      type="checkbox"
      value="Rare"
    />
    <label for="form_field_13_3_Rare">Rare</label>
  </div>
  <div class="checkbox">
    <input
      id="form_field_13_3_medium"
      name="{{ form_builder.fields.properties.form_field_13_3.name }}[]"
      type="checkbox"
      value="Medium"
    />
    <label for="form_field_13_3_medium">Medium</label>
  </div>
</div>
```

### Radio

The same applies to a `radio` field.&#x20;

```html
<div class="radio-container" data-cfs="5-3-input_radio">
  <div class="radio">
    <input
      id="form_field_14_3_radio_1"
      name="{{ form_builder.fields.properties.form_field_14_3.name }}"
      type="radio"
      value="Radio 1"
    />
    <label for="form_field_14_3_radio_1">Radio 1</label>
  </div>
  <div class="radio">
    <input
      id="form_field_14_3_radio_2"
      name="{{ form_builder.fields.properties.form_field_14_3.name }}"
      type="radio"
      value="Radio 2"
    />
    <label for="form_field_14_3_radio_2">Radio 2</label>
  </div>
</div>
```

### Dropdown

The `data-cfs` attribute should go on the \<select> element itself, not on options.

```html
<select 
  class=""
  name="{{ form_builder.fields.properties.form_field_14_5.name }}"
  data-cfs="5-5-select"
>
  <option value="Dropdown 1">Dropdown 1</option>
  <option value="Dropdown 2">Dropdown 2</option>
</select>
```

### File

The `data-cfs` attribute is on the hidden field, not on the element with `type="file"`.

```html
<label for="form_field_14_6">File</label>
<input
    class="form-control"
    name="{{ form_builder.fields.properties.form_field_14_6.name }}"
    data-cfs="5-6-file"
    type="hidden"
>
<input 
    class="form-control"
    id="form_field_14_6_file"
    type="file"
>
```
