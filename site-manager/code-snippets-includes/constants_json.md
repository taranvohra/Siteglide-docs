# 👀 constants\_json

## Introduction

The constants tag, automatically included at the top of all Siteglide pages and Page Templates gives access to several useful variables within that page.

However, some Liquid files, like automations (including email notifications), don't support a platformOS feature called exports which the constants include uses to give these variables scope in the page.

As a result, the constants include isn't fully supported in these settings.

Instead, we've provided a similar alternative constants\_json which you can use in automations reliably.

### Example

```liquid
{% raw %}
{% function constants = "constants_json" %}

<!-- company_information -->

{{constants.company_information}}

<!-- integrations -->

{{constants.integrations }}

<!-- currency_map -->

{{constants.currency_map}}
{% endraw %}
```

Not Currently Supported

As transactional emails are sent asynchronously, it's not straightforward to implement the current\_user and is\_logged\_in features of constants in the same way so they will not be currently supported.

We may in future add alternatives- by finding the details of the user who was logged in when the automation was queued.

Other Use Cases

You can use this function in Pages, however, be aware it could reduce performance if the page already contains the constants include - simply by duplicating the same functionality.

```
// Some code
```
