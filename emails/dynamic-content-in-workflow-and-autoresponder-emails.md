# 👀 Automations Reference

## Introduction - The Body of the Automation Supports Liquid, with some Limitations

The body of an Automation, whether it is an Email Notification, Custom Liquid Action or API call is a Liquid file, so they can include includes/partials. You can also output fields that were submitted in the Form.

There are a few limitations of this Liquid rendering environment:

* The `export`, `content_for` and `yield` tags are not supported in this environment, which means:
  * The ordinary constants file we include on Pages to make variables like [Company Information](../company-information/company-information.md) work, won't work here. See here instead: [constants\_json](../includes/miscellaneous-siteglide-includes/constants\_json.md)
  * Many Module and WebApp layouts won't work in this context, as they rely on the export tag to pass data between sections of the layout.

You can however use other [Liquid Includes / Partials](../includes/about-includes-partials.md) like Content Sections and Code Snippets to organise code within an automation. This is especially useful for code which needs to run in multiple automations.&#x20;

## Outputting Form Fields, or Using Them in Logic

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

