# 👀 Form Reference

## Including a Form

```liquid
{% raw %}
{% include 'form', id: '1', layout: 'default' %}
{% endraw %}
```

* The id refers to the specific form you wish to output.&#x20;
* Layout refers to either the:
  * The default layout which is created automatically by the system - this should not be edited directly as every time you modify the form fields, the default layout will automatically be updated. Any changes you make using CLI will be overwritten.
  * A custom layout allows you to decide which fields to output and how. You can fully customise it. In the parameter, you should include the file name with no extension, and any subfolders relative to the folder form\_1 where the number matches the form ID.&#x20;

Often you can save time by starting with a default layout and copying it to build your custom layout.

If you output two forms with the same ID, but different layouts, they may display different fields and look visually different, but they would use the same settings and their cases will be stored in the same database table.

## Form Layouts

### Custom Field Sets

For each type of field, you will need to use a slightly different syntax to include a Custom Field Set field in a Form Layout.

When it comes to adding the `data-cfs`HTML attribute, the first number should be the CFS ID and the second number the CFS Field ID. Finally, the type should be specified and preceded by the string "input\_".

E.g. `data-cfs="5-1-input_text"`

If you're not sure where to find these, see:

[how-to-output-custom-field-set-fields-in-a-forms-custom-layout.md](how-to-output-custom-field-set-fields-in-a-forms-custom-layout.md "mention")

#### Text

A text input should have the `data-cfs` attribute inside the `<input>` element.

```liquid
<input
  class="form-control"
  name="{{ form_builder.fields.properties.form_field_13_1.name }}"
  data-cfs="5-1-input_text"
  type="text"
/>

```

#### Textarea

The same applies for textarea inputs.

```liquid
<textarea
  class="form-control"
  name="{{ form_builder.fields.properties.form_field_13_6.name }}"
  data-cfs="5-4-textarea"
  rows="5"
  cols="30"
>
</textarea>

```

#### Checkbox

A Checkbox group should have the `data-cfs` attribute on the container for the entire group. `<input>` elements should be the grandchildren of this group.

```liquid
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

#### Radio

The same applies to a `radio` field.

```liquid
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

#### Dropdown

The `data-cfs` attribute should go on the `<select>` element itself, not on `<option>`s.

```liquid
<select 
  class=""
  name="{{ form_builder.fields.properties.form_field_14_5.name }}"
  data-cfs="5-5-select"
>
  <option value="Dropdown 1">Dropdown 1</option>
  <option value="Dropdown 2">Dropdown 2</option>
</select>

```

#### File

The `data-cfs` attribute is on the hidden field, not on the element with `type="file"`.

```liquid
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
