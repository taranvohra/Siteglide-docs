# 🔧 Automations Reference

## Introduction - The Body of the Automation Supports Liquid, with some Limitations

The body of an Automation, whether it is an Email Notification, Custom Liquid Action or API call is a Liquid file, so they can include includes/partials. You can also output fields that were submitted in the Form.

There are a few limitations of this Liquid rendering environment:

* The `export`, `content_for` and `yield` tags are not supported in this environment, which means:
  * The ordinary constants file we include on Pages to make variables like [Company Information](../../company-information/company-information.md) work, won't work here. See here instead: [constants\_json](../../miscellaneous-siteglide-includes/constants\_json.md)
  * Many Module and WebApp layouts won't work in this context, as they rely on the export tag to pass data between sections of the layout.

You can however use other [Liquid Includes / Partials](../../includes-partials/about-includes-partials/) like Content Sections and Code Snippets to organise code within an automation. This is especially useful for code which needs to run in multiple automations.&#x20;

## Outputting Form Fields, or Using Them in Logic

{% hint style="info" %}
Note- this won't work with WebApps and Modules, see section below!
{% endhint %}

Outputting all available submission data as JSON tree for testing purposes:\
\
`{{form}}`\
\
Output the User's core fields:

```liquid
{{form.properties.name}}

{{form.properties.email}}
```

Output a custom field (note, this includes CRM fields and Custom Field Set fields, as they will always have a corresponding field in the case which contains a snapshot of the submission data):

```liquid
{{form.properties.form_field_1_2}}
```

Note, only the database IDs of your fields can be used here, not their human-friendly field names. These can be found in the form\_configurations folder if you use Siteglide-CLI. Or you can output the `{{form.properties}}` JSON to see all of the options available.

## Outputting WebApp and Module Fields

These code suggestions are intended for when you add an automation for WebApp or Module create or edit.&#x20;

### On Item Create

Outputting all available module/webapp data as JSON tree for testing purposes:\
\
`{{data}}`

Output a core field:

`{{data.module_field_3_1}}`

Output a custom field:

`{{data.module_field_custom_3_1}}`

### On Item Update

Outputting data is slightly different when the trigger is an updated WebApp or Module item, because you have access to both the orginal data and the newly updated data.

Outputting all available module/webapp data as JSON tree for testing purposes:

`{{data.originalData}} <!-- Original Data-->`\
`{{data.data}} <!-- New Data-->`

Output a core field:

`{{data.originalData.module_field_3_1}}`

`{{data.data.module_field_3_1}}`

Output a custom field:

`{{data.originalData.module_field_custom_3_1}}`

`{{data.data.module_field_custom_3_1}}`

Make a Comparison

```liquid
{% raw %}
{% if  data.originalData.module_field_custom_3_1 != data.data.module_field_custom_3_1 %}
    {% comment %}Field module_field_custom_3_1 has changed. Do something{% endcomment %}
{% else %}
    {% comment %}Field module_field_custom_3_1 has not changed. Do something{% endcomment %}
{% endif %}
{% endraw %}
```

