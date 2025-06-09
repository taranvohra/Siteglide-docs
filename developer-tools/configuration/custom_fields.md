# ℹ️ Custom Field IDs

Each WebApp and Module has specific custom fields. Each field has a human-readable name and a database ID.

## Introduction

WebApp custom fields are designed to be used by Agencies and Clients to store whatever they need.

Each field is designed to be flexible and reliable. To achieve this we give each field two names by which they can be referred to in the code:

* `Custom Field ID` e.g. `"webapp_field_1_2"`. Usually in the syntax, you refer to this prefixed by `properties` e.g. `properties.webapp_field_1_2`.
* `Name` - the human-readable, editable name. e.g. `"Manufacturer's Instructions"`

#### How do I find a field's Custom Field ID?

\*\*\*With the Siteglide Admin \*\*\*In Admin, you can find the `Custom Field ID` by navigating to any WebApp Item in the WebApp. You can then display the `Custom Field ID` against each field by turning on the toggle at the top of the page.

The `Custom Field ID` will always have the following format:

`webapp_field_x_y`

...where x is the ID of the WebApp the custom field belongs to and y is given to the field in the order the Custom Field was created. For example, the third field created on webapp\_5, would have the Custom Field ID of `webapp_field_5_3`.

\*\*\*With Liquid \*\*\*Inside your WebApp Layout, you can output the entire JSON data structure for the Item using:`{{this}}` Inside this, the Custom Field IDs tend to be stored inside the properties object- this shows the original structure of fields in the results. Outputting the following will show you a list of Custom Field IDs and their values for this item: `{{this.properties}}`

Using your favourite JSON parsing/ prettifier tool, you can read this JSON and identify each field by its contents. You can see a third party comparison of JSON tools here, to help you pick your favourite: [https://geekflare.com/json-online-tools/](https://geekflare.com/json-online-tools/). You can also install a VSCode extension to do this.

#### Why do we need two ways to refer to the field?

The actual name of the field in the Database is the `Custom Field ID`. This fulfils an important functional role. The key points are:

* It always stays the same - meaning you can always reliably access the data stored in the field
* It has a format easily accessed by code- which in some specific cases can mean using it will make your Pages faster. (We'll list some common Use Cases later.)

We also provide a human-readable `Name` for each field. That's what is chosen when Agency or Client create the WebApp. This lets you:

* Know exactly what the field is for when managing your WebApp items in Admin and outputting them in Layouts.
* Change the Name whenever you like
* Use spaces in the name

#### When is the Custom Field ID useful?

Most of the time when you're working in Layouts, you can refer to the field by its name. This is easier for the developer as it becomes self-evident what the field's role is.

However, when you're working on some features, the documentation will ask you to refer to the field by its `Custom Field ID`. This is because for some features, better Page load speed is achieved using this more direct way to refer to a field and we want to pass on the benefits of this advantage to you. Here are examples of some of the Articles where we'll ask you to use the `Custom Field ID`:

* When sorting WebApps
* When filtering WebApps with "use\_adv\_search"
* When pre-fetching Datasources

#### What about Modules, Custom Fields, and Custom Field Sets?

When working with Modules and their Custom Fields; you can use the Toolbox within Code Editor to find these Custom Fields and their associated code.

Many of their fields will also have `Custom Field IDs`. These are also used when sorting and filtering for better performance.

The main difference is in the format:

`module_field_x_y` instead of `webapp_field_x_y`.

[Custom Field Sets](../../crm/users/editing-a-users-crm-record-front-end-with-custom-field-sets.md) also have `Custom Field IDs` which are commonly used when accessing them.
