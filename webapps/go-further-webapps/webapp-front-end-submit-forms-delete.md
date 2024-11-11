---
title: WebApps - Delete owned WebApps from front-end
slug: LBWs-
createdAt: 2021-01-29T11:38:18.000Z
updatedAt: 2023-04-11T10:11:39.000Z
---
# Introduction

When your Users have created WebApp items front-end, you can now give them the option to delete the items they no longer need.

A User will only be able to delete a WebApp item they own. Generally a User will own a WebApp item they've already created, but it's now possible to change WebApp ownership in Admin. You can use Liquid to further control when the button is presented to Users.

This changes if you turn on "anyone can edit" for the WebApp in the Siteglide Admin. Then, you are responsible for adding your own custom Liquid logic to control access to the button.

You can use optionally use JavaScript to change the behaviour when the button is successful, or when it errors.

# Syntax

## Including the button

To include the delete button, add the following syntax inside a WebApp Layout of your choice
```
{% raw %}
{% include "webapp_delete", layout: "default" %}
{% endraw %}
```

Nesting this inside a WebApp Layout allows it to easily pick up the ID of the current WebApp item.

### Security

We recommend wrapping the Layout in the following Liquid to make sure the button is only visible to those Users who have the minimum permission needed to successfully delete the current item:

```liquid
{% raw %}
{% if context.current_user.id and context.current_user.id == this.creator.id %} 
    {%- include "webapp_delete", layout: "default" -%}
{% endif %}
{% endraw %}
```

Note that on the backend we will be running an additional check that the WebApp ID passed through is owned by the currently logged in User- so it won't be possible for malicious Users to delete items they don't own by passing through different IDs.

# Developing the Layout

Including the button in Liquid as above will require a small Layout- which allows you to customise the way the button looks and functions.

## File Structure

Layouts for this button are stored at the following path:
`layouts/webapp_components/webapp_delete/my_layout.liquid`

## Calling the Main JavaScript Function

To make the delete button functional, you need to run the `s_owned_webapp_delete()` function on an event (usually a click event).

You should pass the following arguments:

| Argument number | What is it?                                    | Example                 |
| --------------- | ---------------------------------------------- | ----------------------- |
| 1               | This WebApp ID                                 | `{{this.id}}`           |
| 2               | Token                                          | `{{token}}`             |
| 3               | Optional custom success callback function name | `webapp_delete_success` |
| 4               | Optional custom error callback function name   | `webapp_delete_fail`    |

## Customising the JavaScript

You can add custom JavaScript functions to customise the way the button behaves on success and failure. Examples are included on the default layout.

If you don't provide custom functions, the default behaviour will be to:

- On success, show a success message alert and reload the Page.
- On failure, show an error message alert.

Here's an example of custom functions defined and then passed into the 3rd and 4th arguments in the function:

```liquid
{% raw %}
<button
  class="btn btn-danger" 
  onclick="s_owned_webapp_delete('{{this.id}}', '{{token}}', webapp_delete_success, webapp_delete_fail)" 
  title="Delete {{this.name}}"
>
  x
</button>

{%- content_for 'siteglide_footer_scripts' -%}
  <script>
    function webapp_delete_success(id, name) {
      /*Add optional success callback function name as 2nd argument */
      alert('You have successfully deleted ' + name );
      /*Reload the Page to see the item removed - or remove from DOM */
      window.location.reload();
    };
    function webapp_delete_fail(error, status) {
      /*Add optional fail callback function name as 3rd argument */
      alert(status + ' ' + error);
    };
  </script>,,
{%- endcontent_for -%}
{% endraw %}
```

Note that the <a href="https://help.siteglide.com/article/224-siteglide-scripts" target="_blank">Siteglide Footer Scripts</a> feature is a helpful tool to make sure your function definitions are only included in the Page once, avoiding duplicates as multiple iterations of the WebApp Layout are included on the Page. Just be aware that inline comments are not supported by this feature!

Additionally, you could add in custom behaviour before the main delete function runs, for example to provide a confirmation message to Users to check they really want to delete the WebApp item:

```liquid
{% raw %}
<button class="btn btn-danger" 
  onclick="confirm_delete('{{this.id}}', '{{this.name}}', '{{token}}')" 
  title="Delete {{this.name}}"
>
  x
</button>

{%- content_for 'siteglide_footer_scripts' -%}
  <script>
    function confirm_delete(id, webappName, token) {
      var confirm = confirm('Are you sure you want to delete '+ webappName + '?');
      if (confirm == true) {
        s_owned_webapp_delete(id, token);
      }   
    }
  </script>,,
{%- endcontent_for -%}
{% endraw %}
```