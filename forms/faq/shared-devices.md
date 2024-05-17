# Shared Devices

This problem was initially reported here -> [https://roadmap.siteglide.com/bugs/p/forms-overwriting-crm-records](https://roadmap.siteglide.com/core-platform/p/forms-overwriting-crm-records)

If users are sharing a device to access a site, they should log out and log back in when switching user to avoid the CRM record storing data on the wrong user.

However, it may not be obvious to the user that their family member, or colleague is already logged in.

### 1 - How to show that someone is logged in

Our default form layout for new or updated forms will set both 'email' and 'name' as readonly, pre-populated fields if there's a logged in user.

You can also add your own message on page like this:

```liquid
{% raw %}
{%- if context.exports.is_logged_in.data == true -%}
  <p>Hi {{ session.current_user.name }}! <a href="/logout">(not you?)</a></p>
{%- endif -%}
{% endraw %}

```

### 2 - How to allow updating of existing user data - Essentially a 'user update' form

If you look at the email and name fields in your new default layout, you'll see this:

```liquid
{% raw %}
{% if context.exports.is_logged_in.data -%}
    readonly value="{{ session.current_user.name }}"
{% endif %}
{% endraw %}
```

Either remove 'readonly' to allow editing, or remove the entire IF statement if you also don't want it pre-populated.
