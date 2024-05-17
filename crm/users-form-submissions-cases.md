# User's Form Submissions (Cases)

Allow Users to keep track of their communication history with your Client by outputting Form Cases.

## Prerequisites

* This Layout must be outputted inside a Page protected by a Secure Zone

You can use the following links to learn how to set up a Secure Page and the means to access it:

* [Create a Secure Zone](https://help.siteglide.com/article/138-secure-zones-getting-started#2-creating-and-editing-a-secure-zone)
* [Create a Secure Zone Sign Up Form](https://help.siteglide.com/article/138-secure-zones-getting-started#2-adding-a-sign-up-form)
* [Add a Secure Zone to a Page](https://help.siteglide.com/article/138-secure-zones-getting-started#3-securing-pages)

## Introduction

Allow Users to keep track of their communication history with your Client by outputting Form Cases.

### Syntax

`<div data-gb-custom-block data-tag="include" data-0='user_form_submissions' data-1='default' data-2='default'></div>`

Parameters:

* `layout`

## File Structure

You can find the `user_form_submissions` Layouts at the following path in Code Editor: `layouts/modules/module_5/user_form_submissions/`

Inside this folder, a single Liquid file can be created to act as your Layout. There is no "wrapper" and "item" file needed for this kind of Layout.

## Developing the Layout

### The Loop

You'll need to use a Liquid For Loop to loop over the records in this Layout.

One of the benefits of this is that you can rename the variable under which your fields are kept. If you like you can store the variables under the namespace "this".

```liquid
{% raw %}
{% for this in submissions %}
  <p>Form name: {{this.name}}</p>
{% endfor %}
{% endraw %}

```

Or, if you want to output the `form_submissions` layout inside a `user_details` Layout for example, you can store the variables under a different namespace e.g. `case` and continue to use `this` to refer to the `user_details` (Liquid variables are always inherited by Layouts included within them).

```liquid
{% raw %}
{% for case in submissions %}
  <p>User Name: {{this.name}}</p>
  <p>Form name: {{case.name}}</p>
{% endfor %}
{% endraw %}
```

### Available Fields (within the loop)

In the following examples, we'll use the namespace "case", but you can substitute this for the namespace you chose when creating your loop.

* `{{case.form_name}}` - The user-friendly name of the Form
* `{{case.name}}` - The model\_schema\_name of the Case- e.g. form\_3. This can tell you the Form's ID.
* `{{case.id}}`
* `{{case.created_at}}` - The date the Form was submitted. Use the "| date" filter with Ruby formatting to format.
* `{{case.properties.name}}`
* `{{case.properties.email}}`
* `{{case.properties.user_id}}`
* `{{case.properties.form_field_1_1}}` - Access any of your custom Form Fields with a variation of this output tag. The first number refers to the ID of the Form. The second number refers to the ID of the Field. You can check these IDs for your own custom fields in the Siteglide Admin.

To see the available data on Page load as JSON, output your namespace within the loop:

e.g. `<p>{{case}}</p>`
