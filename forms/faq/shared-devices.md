It's not too hard a situation to imagine...

You're logged in to a website, and you walk away from the PC. Someone comes along and starts using the same website. If they submit a form, then it shouldn't update your CRM record. It should show them that you're still logged in. They will then log out and create a new CRM record.

This problem was initially reported here -> [https://roadmap.siteglide.com/bugs/p/forms-overwriting-crm-records](https://roadmap.siteglide.com/core-platform/p/forms-overwriting-crm-records)

After much discussion here's measures we've taken to make this easier to implement for you.

### 1 - How to show that someone is logged in

Our default form layout for new or updated forms will set both 'email' and 'name' as readonly, pre-populated fields if there's a logged in user.

You can also add your own message on page like this:

```html
{%- if context.exports.is_logged_in.data == true -%}
    <p>Hi {{ session.current_user.name }}! <a href="/logout">(not you?)</a></p>
{%- endif -%}
```

### 2 - How to allow updating of existing user data - Essentially a 'user update' form

If you look at the email and name fields in your new default layout, you'll see this:

```html
 {% if context.exports.is_logged_in.data -%}
        readonly value="{{ session.current_user.name }}"
 {% endif %}
```

Either remove 'readonly' to allow editing, or remove the entire IF statement if you also don't want it pre-populated.
