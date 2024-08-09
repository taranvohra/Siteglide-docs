---
title: Using the current_user object with Secure Zones
slug: '-niR-'
createdAt: 2021-02-17T12:51:44.000Z
updatedAt: 2023-03-03T08:09:58.000Z
---

# ℹ️ Using the context.current\_user object

This article for developers helps you get more out of Secure Zones, as you can output basic information about the Current User dynamically.

## Prerequisites

* You have installed the Secure Zones Module
* You have added a User Sign Up Form
* A User has logged in

## The current\_user Object

When a User signs up or logs into your site, we store basic information about that user. You can use this to make the page respond uniquely to that user.

Outputting the following liquid on the page shows the full range of fields available:`{{context.current_user | json}}` You can traverse through the fields in the object and output them with dot notation. E.g. `{{context.current_user.first_name}}` This will output the current user's first name, so you can say hello.

You could also use an if statement to run logic using this. E.g. If I want to say hello to all users with a siteglide email address:

```liquid
{% raw %}
{% if context.current_user.email contains "@siteglide.com" %}
  <p>Hello Siteglider!</p>
{% endif %}
{% endraw %}
```
