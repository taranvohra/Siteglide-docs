# User Secure Zones

Outputting a User's Secure Zones can help them to keep track of services they're signed up to.

## Prerequisites

* This Layout must be outputted inside a Page protected by a Secure Zone

You can use the following links to learn how to set up a Secure Page and the means to access it:

* [Create a Secure Zone](https://help.siteglide.com/article/138-secure-zones-getting-started#2-creating-and-editing-a-secure-zone)
* [Create a Secure Zone Sign Up Form](https://help.siteglide.com/article/138-secure-zones-getting-started#2-adding-a-sign-up-form)
* [Add a Secure Zone to a Page](https://help.siteglide.com/article/138-secure-zones-getting-started#3-securing-pages)

## Introduction

Outputting a User's Secure Zones can help them to keep track of services they're signed up to.

## Syntax

```liquid
{% raw %}
{% include 'user_secure_zones', layout: 'default' %}
{% endraw %}
```

Parameters:

* `layout`

## File Structure

You can find the `user_secure_zones` Layouts at the following path in Code Editor: `layouts/modules/module_5/user_secure_zones/`

Inside this folder, a single Liquid file can be created to act as your Layout. There is no "wrapper" and "item" file needed for this kind of Layout.

## Developing the Layout

### The Loop

You'll need to use a Liquid For Loop to loop over the records in this Layout.

One of the benefits of this is that you can rename the variable under which your fields are kept. If you like you can store the variables under the namespace "this".

```liquid
{% raw %}
{% for this in secure_zones %}
  <p>Form name: {{this.name}}</p>
{% endfor %}
{% endraw %}


```

Or, if you want to output the `form_submissions` layout inside a `user_details` Layout for example, you can store the variables under a different namespace e.g. case and continue to use `this` to refer to the `user_details` (Liquid variables are always inherited by Layouts included within them).

```liquid
{% raw %}
{% for secure_zone in secure_zones %}
  <p>User Name: {{this.name}}</p>
  <p>Form name: {{secure_zone.name}}</p>
{% endfor %}
{% endraw %}
```

### Available Fields (within the loop)

In the following examples, we'll use the namespace "secure\_zone", but you can substitute this for the namespace you chose when creating your loop.

* `{{secure_zone.name}}` - The User friendly name for this Secure Zone.
* `{{secure_zone.id}}` - The ID of this Secure Zone
