# Custom Field Sets & CRM Custom Fields

All Forms allow Users to edit their details in the CRM. This includes all standard fields like "name" and Custom Field Sets.

## Introduction

All Forms allow Users to edit their details in the CRM.

This includes:

* Name
* Any Custom Field Sets attached to the Form. Use these to store information that you want to keep up to date.
* [Learn more about editing email and password here](how-users-edit-their-email-and-password-front-end.md).

Standard Form Fields are stored against the Case only and are not stored against the CRM record.

This Article will:

* Show how to output Custom Field Set Data in the Form
* Show how to display any existing data in the Form- so the User understands that they are editing data.
* Explain the process Siteglide takes with User data when a Form is submitted

## How CRM editing works

The flowchart diagram below demonstrates an abbreviated summary of what happens when a Form is submitted on Siteglide. Where the diagram mentions Custom Field Sets, the newer CRM Custom Fields feature is applicable as well.

\-->

The most important points to draw from this are:

* All Forms will create a Case and all fields submitted will be shown in the case
* But only the following fields will update the CRM:
  * Custom Field Sets attached to the Form
  * CRM Custom Fields
  * The user's "name" field
  * The email field (on first submission only) - this is used as a unique identifier in the CRM.
  * The "edit email" and "edit password" fields [learn more about editing email and password here.](how-users-edit-their-email-and-password-front-end.md)
* When using Custom Field Sets and CRM custom fields to update the CRM, it doesn't matter whether or not the User already exists in the CRM, or whether or not the User is already logged in.

## Adding Custom Field Set Fields to a Form

See here for a more detailed explanation of [Adding Custom Field Set Fields to a Form](../../cms/forms/guides-forms/how-to-output-custom-field-set-fields-in-a-forms-custom-layout.md)

In summary, to add Custom Field Set fields to a Form, you'll need to:

1. Create a Custom Field Set (or choose an existing one)
2. Attach the Custom Field Set to a Form in Admin. You can mix & match different kinds of fields here.
3. Check that the Liquid for this field is included in the Form Layout
4. Add your Form to a Page with the chosen Layout

### Custom Field Set field syntax in the Form's Layout

If you use a default Form Layout, then attaching the Custom Field Set to the Form will automatically add the fields to the Layout. If using a Custom Layout, we recommend you copy and paste the code from the default Layout to your custom Layout before editing it.

Here is an example of a Custom Field Set field added to the Layout:

```liquid
<div class="row mt-4 input_text">
  <div class="col">
    <label for="form_field_13_3">Favourite Colour</label>
    <input class="form-control" 
           name="{{ form_builder.fields.properties.form_field_13_3.name }}" 
           data-cfs="3-3-input_text" 
           type="text">
  </div>
</div>

```

Note the `data-cfs` attribute which gives you a clue this is a Custom Field Set Field and will therefore submit to the CRM record.

## Adding CRM Custom Fields to the Form

CRM Custom Fields work in a similar way to Custom Field Sets, but instead of operating as a group of fields, they can be added to the form individually. One advantage they have over Custom Field Sets is that they use slightly less database records in your usage metrics.

See here for a more detailed explanation of creating CRM fields:

[https://docs.siteglide.com/en/crm/quickstart-crm](../quickstart-crm.md)

In summary:

1. In CRM, custom fields tab, create each custom field you need
2. Attach the CRM Fields to a Form in Admin. You can mix & match different kinds of fields here.
3. Check that the Liquid for these CRM fields is included in the Form Layout
4. Add your Form to a Page with the chosen Layout

### CRM Custom Field syntax in the Form Layout

As with Custom Field Sets, the syntax for adding CRM custom fields to your form is automatically added to the Form's default Layout. You may need to run a pull command if you are using Siteglide-CLI to get any new changes to your default Layout. If using a Custom Layout, we recommend you copy and paste the code from the default Layout to your custom Layout before editing it.

Here is an example of a CRM field added to the Layout:

```liquid
<label for="form_field_1_1">Shipping Address Line 1</label>
<input class="form-control sg-form-control required" name="{{ form_builder.fields.properties['form_field_1_1'].name }}" data-crm="user_field_1" type="text">


```

Note the `data-crm` attribute which gives you a clue this is a Custom Field Set Field and will therefore submit to the CRM record. The ID in the data-attribute refers to the CRM field's ID in the CRM; it is different from the ID in the name attribute, which refers to the field's ID in the case.

### Displaying current field values for logged in users

#### Prerequisites:

* The User must already be Signed Up to any [Secure Zone](../../modules/core-modules/secure-zones/quickstart-secure-zones.md)
* The User must be logged in

#### Why is pre-filling fields useful?

It's extremely useful to display the current values in the fields on Page load. This shows the User the data that is already stored and allows them to make a decision about whether the data needs to be changed.

#### An alternative - Using GraphQL to fetch CRM data

Before we show you the User Details method which uses a low-code approach, we should note that the GraphQL `users`query provides a more flexible approach to fetching user data, including fetching details of users who are not logged in. You can learn more about how to use GraphQL queries here: [https://docs.siteglide.com/en/developer-tools/graphql/tutorials](../../developer-tools/graphql/tutorials/)

#### Using User Details to fetch CRM data- steps

In Order to fetch the existing Custom Field Set data for the current User, they'll need to be logged in. This means they'll need to have already completed a Sign-Up Form to any Secure Zone and set up a password. You may find it helpful to build an onboarding flow with two separate.

To achieve this, you can combine two Siteglide Features by nesting a Siteglide Form inside a User Details Layout.

**Step 1) User Details Contain the existing CFS Data** To fetch the existing CFS and CRM data for the Current User, you'll need a [User Details](user-details.md) Layout.

```liquid
{% raw %}
{% include 'user_details', layout: 'user_details_edit_form_container' %}
{% endraw %}

```

Parameters:

* `layout` - Choose a Layout from the following folder in Code Editor: `layouts/modules/module_5/user_details/`

**Step 2) Place the Form inside User Details** The User Details Layout has direct access to Custom Field Set data, but normally the Form does not. In order to achieve this, we place the Form inside the `user_details` Layout. Due to Liquid inheritance, the Custom Field Set data will then be available inside the Form.

Output your Form by writing the code for the Form inside this `user_details` Layout instead of directly in the Page e.g.

```liquid
{% raw %}
{% include 'form', id: '10', layout: 'custom' %}
{% endraw %}

```

Remember to replace the example form ID with your own.

**Step 3) Use Liquid to prefill the HTML values** This will allow you to access the existing User data and their related Custom Field Sets within the Form.

In this example, we have a Custom Field Set "Checkout Address" with a "Profile Picture", a Favourite Colour and a Country field:

```liquid
{{this.custom_field_sets['Checkout Address']['Favourite Colour']}} 
<!-- Red-->
{{this.custom_field_sets['Checkout Address']['Country']}} 
<!-- UK -->
{{this.custom_field_sets['Checkout Address']['Profile Picture']}} 
<!-- documents/form_uploads/form_3/profile-1603989579828.png -->

```

See [https://docs.siteglide.com/en/crm/users/user-details#accessing-custom-crm-fields](user-details.md#accessing-custom-crm-fields) to see how to access data from CRM custom fields within the User Details Layout.

As the `value` attribute in HTML determines the pre-filled value of a field, we can use Liquid to add it. In most cases, there is an \<input> element which can be given a value, eg. in the "Favourite Colour" field:

```liquid
<input 
  class="form-control" 
  name="{{ form_builder.fields.properties.form_field_13_3.name }}" 
  data-cfs="3-3-input_text" 
  type="text" 
  value=""
>

```

Values can also be added to \<select> elements:

```liquid
<div class="row mt-4 select">
  <div class="col">
    <label for="form_field_13_1">Country</label>
    <select 
      class="" 
      name="{{ form_builder.fields.properties.form_field_13_1.name }}" 
      data-cfs="3-1-select" 
      value="{{this.custom_field_sets['Checkout Address']['Country']}}"
    >
      <option value="UK">UK</option>
      <option value="USA">USA</option>
      <option value="Canada">Canada</option>
      <option value="Australia">Australia</option>
      <option value="New Zealand">New Zealand</option>
    </select>
  </div>
</div>

```

File and Image fields are more complex, each has two elements- a `type="file"` and a `type="hidden"` field. If you wish the File upload to have validation, both the `value` attribute and `.required` class should be added to the `type="hidden"` input. This is because this is the field that actually has a `name` attribute and sends to the database.

```liquid
<label for="form_field_3_6">Profile Picture</label> 
<input 
  class="form-control required" 
  name="{{ form_builder.fields.properties.form_field_3_6.name }}" 
  data-cfs="1-6-image" 
  type="hidden"
  value="{{this.custom_field_sets['Checkout Address']['Profile Picture']}}"
>
<input class="form-control" id="form_field_3_6_file" type="file">

```

This adds the value to the field, but for the Profile Picture, I may also want to show a larger preview of the image outside the field. You can use the same Liquid to display the image, using the `asset_url` filter to complete the path:

```liquid
<div id="profile_pic" data-file-preview="form_field_10_1_file" style="background-image: url('{{this.custom_field_sets.cfs_3.properties.cfs_field_3_1 | asset_url}}');">

</div>
```

Attributes:

* `style="background-image: url('{{this.custom_field_sets.cfs_3.properties.cfs_field_3_1 | asset_url}}');"` - This Liquid would allow the existing image to be displayed on Page Load.
* `data-file-preview="form_field_10_1_file"` - This sets up the element to preview the next image a User uploads to this field. Read more here: [File Upload Previews](../../cms/forms/go-further-forms/file-upload-previews/).

## Multiple parts to the Form

You may wish to split your fields into multiple "User Profile" sections where the User can enter a set of fields, save and then move to another section.

To keep the Cases tidy for multiple Forms and be most efficient with Database Usage, you can optionally use:

* A single Admin Form
* A single Custom Field Set
* Multiple Form Layouts, each displaying alternative sub-sets of Fields. (Name and email can be pre-filled using HTML, to prevent asking logged in Users for this information multiple times in the flow.)

This will mean that Cases for each part of the Form will still be collected in the same location in Admin, but you can use the Form Layouts to control which fields are displayed in each view.

All Forms must include the `user_id` and `email` fields, but if you want to hide these from the sections which are not visible, you can give these `type="hidden"` so that they are not seen in the Sections which do not require them. You can auto-fill their values using the steps in the previous section.
