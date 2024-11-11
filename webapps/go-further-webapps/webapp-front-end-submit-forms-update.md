---
title: WebApps - Front End Edit
slug: Z-iL-
createdAt: 2021-01-29T11:28:56.000Z
updatedAt: 2023-03-03T08:09:28.000Z
---
# WebApp - Front End Submit Forms - Update

## Introduction

If a logged-in visitor to your Site has submitted a WebApp Item, they can now edit it too.&#x20;

## The WebApp Creator

Most WebApps, including those created by the Admin and those created by visitors who are not logged in will not store the ID of a `creator`. 

However, any WebApps created Front-End by a logged in User will store their creator's ID in the `creator` field. 

## Filtering a WebApp List by creator

### Finding WebApp Items created by the current user

```liquid
{% raw %}
{% include 'webapp'
   id: '1'
   layout: 'default'
   type: 'list'
   creator_id: context.current_user.id 
%}
{% endraw %}
```

### Finding WebApp Items created by any specific user

In this example we create a variable by hard-coding a specific User ID.&#x20;

```liquid
{% raw %}
{% assign user_id = '8' %}
{% include 'webapp'
   id: '1'
   layout: 'default'
   type: 'list'
   creator_id: user_id  
%}
{% endraw %}
```

### Outputting information about the creator in the WebApp Layout

You can now access the following fields inside a WebApp Layout:

- `{{this.creator.id}}`
- `{{this.creator.name}}`
- `{{this.creator.first_name}}`
- `{{this.creator.last_name}}`
- `{{this.creator.created_at}}`

### Viewing the Edit Form and Permissions 

{% hint style="info" %}
## Important
Even if you include the Liquid Tag, the Form will only display for visitors who are logged in and are registered as that WebApp's creator.
{% endhint %}

Under default settings, only a WebApp owner can see and also submit the edit form. A WebApp gets an owner when a user is logged in and submits the original WebApp create form. Their User ID is stored in the user_id field against the webapp.

It is possible to modify the owner of a WebApp in the Siteglide Admin.

It is also possible to set the "Anyone can edit" setting to true in the Siteglide admin in the "View Table" area for that WebApp. 

Setting this to true means that default edit protections are removed for that WebApp on the front-end. You will then be responsible for writing your own Liquid code to wrap around the form if you wish to set custom Secure Zone permissions.

### Find other WebApp items with the same creator

You could of course combine both of these features- creating a link to the same page including the creator\_id as a query parameter and then filtering by that ID using `context.params` to fetch the ID from the URL.

# Syntax for the Edit Form

## Including the Form inside a WebApp Layout

Unlike the "Add" Form, the Front End WebApp Edit Form must be linked to the specific WebApp Item it will Edit. This means you can only output the Form inside a WebApp Detail or List Layout file. 

To include the Edit Form inside a WebApp Layout, add the Liquid tag:
```liquid
{% raw %}
{% include 'webapp_form_edit', layout: 'default' %}
{% endraw %}
```

Parameters: 

- `layout` - Optional - Choose the name of your Layout file

## Developing the Form Layout

The Edit Form will work if you use the same Layout as you used for your add Form. 

However, you may wish to use an alternative Layout so you can add some additional features.

### Dynamic Fields from the WebApp

As you're including the Edit Form inside a WebApp Item, you have access to the WebApp fields that are inherited from the WebApp Layout.

One example might be adding a Title to the Form which dynamically references the WebApp Item:
`<h3>Edit {{this.name}}</h3>`

Another example might be displaying the creator's name: `<h4>By {[this.creator.name}}</h4>`

### Pre-filling values 

In a Form Layout, we use the `form_builder` variable to dynamically add the correct `name` Attribute to inputs. You can use this to output the pre-filled value; instead of the name property, output the value property.

For this example WebApp field:
```liquid
{% raw %}
<input name="{{form_builder.fields.properties.webapp_field_1_1.name}}">
{% endraw %}
```

...you can use the name field and replace `.name` with `.value` to add a `value` attribute:

```liquid
{% raw %}
<input name="{{form_builder.fields.properties.webapp_field_1_1.name}}" value="{{form_builder.fields.properties.webapp_field_1_1.value}}">
{% endraw %}
```
