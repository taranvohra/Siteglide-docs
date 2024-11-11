---
title: Front-end Submit WebApps
slug: bf70-
createdAt: 2021-01-29T11:23:35.000Z
updatedAt: 2023-04-11T10:09:44.000Z
---
# WebApp - Front End Submit Forms - Create

When you make a new WebApp, a front-end form file is automatically generated within your WebApp, in a folder called `form`. It automatically contains all fields from your WebApp. You can view this folder using Code Editor, it is next to the `detail` and `list` folders for your WebApp.

# Syntax

Output your WebApp form on a page:
```
{% raw %}
{%- include 'webapp_form', id: 'custom_webapp_1' -%}
{% endraw %}
```

Toolbox has support for WebApp input forms, and the following options will be given in the modal, or you can set them yourself:

- `enabled`  - default is false  - Boolean - Determines if items are auto-enabled or not
- `expiry_date`  - default is `never expires`  - Timestamp - When the new item will expire
- `release_date`  - default is `as soon as the form is submitted`  - Timestamp - When the new item will be released
- `upload_dir` - String - default is `documents/form_uploads/webapp_1/`  Where uploaded files will be stored. Must follow this format - 'folder/optional\_folder/'

# Standard Fields

Some fields are required for the form to be able to set up the WebApp items correctly. These fields are for 'enabled', 'expiry\_date', 'release\_date', 'upload\_dir', and 'slug'. They stay the same each form, and don't have a WebApp specific ID attached to them.

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

All forms should be wrapped in a Liquid form tag: `{% form -%}{% endform -%}`
All forms need a submission button:`<button onClick="s_form_submit_v2(this,'webapp_1')">Submit</button>`

# Category Field (optional)

### Example 1 

This example can be used for a WebApp Submit form that is displayed within a the layout of another WebApp or Module.

```liquid
{% raw %}
<input class="form-control" 
  name="{{ form_builder.fields.properties.category_array.name }}" 
  value="{{this.category_array[0]}}" 
  type="hidden"
/>
{% endraw %}
```

`this.category_array[0]`  - finds the first category the current item is categorised to and can be changed to be a full array, or specific category ID. 

### Example 2

This example can be used on pages other than WebApp and Module layouts. 

```liquid
{% raw %}
<input class="form-control" 
       name="{{ form_builder.fields.properties.category_array.name }}" 
       value="123456" 
       type="hidden"
/>
{% endraw %}
```

`123456`  -  replace with the ID of a category of your choice.

#### Location Field (optional)

You can submit a Location value for a WebApp item as shown in the following example:

```liquid
{% raw %}
<input class="form-control" 
  name="{{ form_builder.fields.properties.location.name }}" 
  value='{"type": "Point","coordinates": [-0.10045,51.49495]}' 
  type="hidden"
/>
{% endraw %}
```

The value should be a stringified JSON object.
