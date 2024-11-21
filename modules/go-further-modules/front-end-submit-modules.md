# ℹ️ Front-end Submit Modules

When you install a Module, a front-end form file is automatically generated within your Module, in a folder called `form`. It automatically contains all fields from the Module. You can view this folder using Code Editor, it is next to the `detail` and `list` folders for your Module.

## Syntax

### Creating New Items

Output your Module form on a page to create new items:

```
{% raw %}
{%- include 'module_form', id: '3', layout: layout, enabled: 'true'-%}
{% endraw %}

```

### Editing Existing Items

Edit forms should be outputted inside a standard Module layout's item.liquid file, to make sure it has access to the \{{this.id\}} variable. It will need this to load the form with the correct resource\_id.

#### item.liquid file

```
{% raw %}
{%- include 'module_form_edit', id: '3', layout: layout, enabled: 'true'-%}
{% endraw %}
```

Note when developing a layout for an edit form, be sure to use the HTML value attribute to give the fields their current values from the database.

```
<input name="{{form_builder.fields.properties.module_field_3_1.name}}" value="{{form_builder.fields.properties.module_field_3_1.value}}">
```

Using a SiteBuilder form layout will save you this step.

#### Options

Toolbox has support for Module input forms, and the following options will be given in the modal, or you can set them yourself:

* `enabled` - default is `false` - Boolean - Determines if items are auto-enabled or not
* `expiry_date` - default is `never expires` - Timestamp - When the new item will expire
* `release_date` - default is `as soon as the form is submitted` - Timestamp - When the new item will be released
* `upload_dir` - String - default is `documents/form_uploads/module_1/` Where uploaded files will be stored. Must follow this format - 'folder/optional\_folder/'

## Standard Fields

Some fields are required for the form to be able to set up the Module items correctly. These fields are for 'enabled', 'expiry\_date', 'release\_date', 'upload\_dir', and 'slug'. They stay the same each form, and don't have a Module specific ID attached to them.

```html
<input class="form-control" 
       name="{{ form_builder.fields.properties.enabled.name }}" 
       value="{{_enabled}}" 
       type="hidden"
/>
<input class="form-control" 
       name="{{ form_builder.fields.properties.expiry_date.name }}" 
       value="{{_expiry_date}}" 
       type="hidden"
/>
<input class="form-control" 
       name="{{ form_builder.fields.properties.release_date.name }}" 
       value="{{_release_date}}" 
       type="hidden"
/>
<input id="s_redirect" 
       value="/home" 
       type="hidden"
/>
<input class="form-control upload_dir" 
       value="{{_upload_dir}}" 
       type="hidden"
/>
<input class="form-control" 
       name="{{ form_builder.fields.properties.slug.name }}" 
       type="hidden"
/>

```

All forms should be wrapped in a Liquid form tag: `<div data-gb-custom-block data-tag="form"></div>` All forms need a submission button:`<button onClick="s_form_submit_v2(this,'module_1')">Submit</button>`

## Category Field (optional)

#### Example 1

This example can be used for a Module Submit form that is displayed within a the layout of another WebApp or Module.

```html
<input class="form-control" 
       name="{{ form_builder.fields.properties.category_array.name }}" 
       value="{{this.category_array[0]}}" 
       type="hidden"
/>
```

`this.category_array[0]` - finds the first category the current item is categorised to and can be changed to be a full array, or specific category ID.

#### Example 2

This example can be used on pages other than WebApp and Module layouts.

```html
<input class="form-control" 
       name="{{ form_builder.fields.properties.category_array.name }}" 
       value="123456" 
       type="hidden"
/>
```

`123456` - replace with the ID of a category of your choice.

Location Field (optional)

You can submit a Location value for a Module item as shown in the following example:

```html
<input class="form-control" 
       name="{{ form_builder.fields.properties.location.name }}" 
       value='{"type": "Point","coordinates": [-0.10045,51.49495]}' 
       type="hidden"
/>
```

The value should be a stringified JSON object.
