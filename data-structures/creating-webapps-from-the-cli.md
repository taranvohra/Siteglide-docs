# Creating WebApps from the CLI

{% hint style="info" %}
We are using `99` as an example WebApp ID in this doc. Depending on the WebApp ID that you'd like to use, replace `99` with the correct ID. Keep in mind that if you already have WebApps in the site you are working on then then some WebApp IDs may already be reserved.
{% endhint %}

WebApps in Siteglide rely on 3 different files to work correctly.

1. **JSON Structure** - Used by Siteglide Admin and front-end to define structure of the WebApp with user-friendly names, and other UI metadata.
2. **Schema** - Used to define the database structure itself
3. **Form Configuration** - Used when submitting WebApp items front-end

There are 2 ways to create/edit a WebApp via CLI.

1. _Safest_ - Create/Edit the JSON structure file (`marketplace_builder/views/partials/tables/webapps/99.liquid`), and then in Siteglide Admin simply click 'Save' in the Table Builder view. This will generate a matching Form Configuration and Schema file. We recommend then using CLI to pull the saved files immediately afterwards, otherwise you may accidentally overwrite them.
2. _Most flexible_ - Create/Edit each of the 3 files manually. However, this relies on you keeping all 3 files in sync.

#### JSON Structure

This is used by Siteglide Admin to output WebApp field data with user-friendly names and other UI options (order, field type, etc.)

Location: `marketplace_builder/views/partials/tables/webapps/99.liquid`

Contents:

```json
{
	"id": 99,
	"type": "webapp",
	"name": "My CLI WebApp",
	"slug": "my-cli-webapp",
	"detail": true,
	"detail_template": "templates/1",
	"detail_default_layout": "default",
	"sz": false,
	"sz_updated": true,
	"sz_display_type": "404",
	"system_fields": {
		"name": {
			"type": "string",
			"editable": true,
			"hidden": false,
			"live": true,
			"order": 0,
			"required": false
		},
		"slug": {
			"type": "string",
			"editable": true,
			"hidden": false,
			"live": true,
			"order": 0,
			"required": false
		},
		"weighting": {
			"type": "integer",
			"editable": true,
			"hidden": false,
			"live": true,
			"order": 0,
			"required": false
		},
		"release_date": {
			"type": "integer",
			"editable": true,
			"hidden": false,
			"live": true,
			"order": 0,
			"required": false
		},
		"expiry_date": {
			"type": "integer",
			"editable": true,
			"hidden": false,
			"live": true,
			"order": 0,
			"required": false
		},
		"enabled": {
			"type": "boolean",
			"editable": true,
			"hidden": false,
			"live": true,
			"order": 0,
			"required": false
		},
		"category_array": {
			"type": "array",
			"editable": true,
			"hidden": false,
			"live": true,
			"order": 0,
			"required": false
		},
		"meta_title": {
			"type": "string",
			"editable": true,
			"hidden": false,
			"live": true,
			"order": 0,
			"required": false
		},
		"meta_desc": {
			"type": "string",
			"editable": true,
			"hidden": false,
			"live": true,
			"order": 0,
			"required": false
		},
		"og_title": {
			"type": "string",
			"editable": true,
			"hidden": false,
			"live": true,
			"order": 0,
			"required": false
		},
		"og_desc": {
			"type": "string",
			"editable": true,
			"hidden": false,
			"live": true,
			"order": 0,
			"required": false
		},
		"og_type": {
			"type": "string",
			"editable": true,
			"hidden": false,
			"live": true,
			"order": 0,
			"required": false
		},
		"twitter_type": {
			"type": "string",
			"editable": true,
			"hidden": false,
			"live": true,
			"order": 0,
			"required": false
		},
		"secure_zone_array": {
			"type": "array",
			"editable": true,
			"hidden": false,
			"live": true,
			"order": 0,
			"required": false
		},
		"location": {
			"type": "geojson",
			"editable": true,
			"hidden": false,
			"live": true,
			"order": 0,
			"required": false
		},
		"address": {
			"type": "string",
			"editable": true,
			"hidden": false,
			"live": true,
			"order": 0,
			"required": false
		},
		"og_image": {
			"type": "string",
			"editable": true,
			"hidden": false,
			"live": true,
			"order": 0,
			"required": false
		},
		"og_url": {
			"type": "string",
			"editable": true,
			"hidden": false,
			"live": true,
			"order": 0,
			"required": false
		}
	},
	"custom_fields": {
		"webapp_field_99_1": {
			"name": "Custom Field",
			"type": "input_text",
			"live": true,
			"order": 1,
			"editable": true,
			"hidden": false,
			"required": false
		}
	},
	"automations": {},
	"install_to_site": true,
	"use_standard_fields": true
}
```

Please see the [Field Types](https://developers.siteglide.com/field-types) document for all the relevant types.

#### YML Schema File

This is what defines the database table structure, and how data will be stored.

Location: `marketplace_builder/custom_model_types/webapps/webapp_99.yml`

Contents:

```yaml
---
name: webapp_99
properties:
- name: name
  type: string
- name: slug
  type: string
- name: weighting
  type: integer
- name: release_date
  type: integer
- name: expiry_date
  type: integer
- name: enabled
  type: boolean
- name: category_array
  type: array
- name: meta_title
  type: text
- name: meta_desc
  type: text
- name: og_title
  type: text
- name: og_desc
  type: text
- name: og_image
  type: text
- name: og_type
  type: string
- name: twitter_type
  type: string
- name: full_slug
  type: string
- name: secure_zone_array
  type: array
- name: location
  type: geojson
- name: address
  type: text
- name: webapp_field_99_1
  attribute_type: string
---
```

The above are all the default fields that are needed, the last field is an example of a standard text field. Please see the [Field Types](https://developers.siteglide.com/field-types) document for all the relevant types.

#### Form Configuration

This is used when submitting a WebApp item front-end and if you are using SiteBuilder, to power dynamic form layouts. This file was also previously used to output WebApp structure data in Siteglide Admin, but that is now the job of the JSON structure file.

Location: `marketplace_builder/form_configurations/webapps/webapp_99.liquid`

Contents:

```yaml
---
name: webapp_99
resource: webapp_99
resource_owner: anyone
configuration:
  properties:
    webapp_name:
      name: webapp_name
      value: 'My CLI WebApp'
      property_options:
        virtual: true
    webapp_slug:
      name: webapp_slug
      value: 'my-cli-webapp'
      property_options:
        virtual: true
    webapp_detail:
      name: webapp_detail
      value: true
      property_options:
        virtual: true
    webapp_detail_template:
      name: webapp_detail_template
      value: 'templates/1'
      property_options:
        virtual: true
    webapp_detail_default_layout:
      name: webapp_detail_default_layout
      value: 'default'
      property_options:
        virtual: true
    webapp_sz:
      name: webapp_sz
      value: false
      property_options:
        virtual: true
    webapp_sz_updated:
      name: webapp_sz_updated
      value: false
      property_options:
        virtual: true
    webapp_sz_display_type:
      name: webapp_sz_display_type
      value: '404'
      property_options:
        virtual: true
    name:
      name: name
      type: string
    slug:
      name: slug
      type: string
    weighting:
      name: weighting
      type: integer
    release_date:
      name: release_date
      type: integer
    expiry_date:
      name: expiry_date
      type: integer
    enabled:
      name: enabled
      type: boolean
    category_array:
      name: category_array
      type: array
    meta_title:
      name: meta_title
      type: string
    meta_desc:
      name: meta_desc
      type: string
    og_title:
      name: og_title
      type: string
    og_desc:
      name: og_desc
      type: string
    og_image:
      name: og_image
      type: string
    og_type:
      name: og_type
      type: string
    twitter_type:
      name: twitter_type
      type: string
    full_slug:
      name: full_slug
      type: string
    secure_zone_array:
      name: secure_zone_array
      type: array
    location:
      name: location
      type: geojson
    address:
      name: address
      type: string
    webapp_field_99_1:
      name: "Custom Field"
      type: input_text
      live: true
      hidden: false
      order: 1
      editable: true
      required: false
      validation: {}
---

<div data-gb-custom-block data-tag="-"></div>layouts/webapps/webapp_99/form/{{_layout}}<div data-gb-custom-block data-tag="-"></div>

<div data-gb-custom-block data-tag="-"></div>
```

After both the above files are synced you will then need to refresh Siteglide Admin and your WebApp will appear under WebApps in the sites left hand menu

#### Layouts

If you need layouts for your WebApp, these will be saved to:

`marketplace_builder/views/partials/layouts/webapps/webapp_99/detail/default.liquid`

`marketplace_builder/views/partials/layouts/webapps/webapp_99/list/default.liquid`

Both files contain the following layout by default: `<p>{{this['name']}}</p>`
