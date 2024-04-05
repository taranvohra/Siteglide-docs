---
description: >-
  Discover liquid tags that you can use to output and capture data globally
  available on Pages.
---

# Accessing Page Data

Discover liquid tags that you can use to output and capture data globally available on Pages.

## Page Content

You can customise content on pages by navigating to your page within CMS / Pages and then scrolling to the Code Editor section at the bottom of the page.

From here you can use the Toolbox to add in custom content sections. Change the order of sections by copying the liquid tags and then pasting them in the desired order.

## Liquid Variables

For the full documentation on the platformOS `context` variable, see here: [https://documentation.platformos.com/developer-guide/variables/context-variable#displaying-the-context-object](https://documentation.platformos.com/developer-guide/variables/context-variable#displaying-the-context-object)\
\
Here are a few useful highlights:

### URL Parameters

* `{{context.location.pathname}}` - outputs the full url path such as "/first-part/second-part"
* `{{context.params.slug}}` - outputs the first part of your url path such as "/first-part"
* `{{context.params.slug2}}`  - outputs the second part of your url path such as "/second-part"
* `{{context.params.myparam}}`  - outputs the value of ?myparam=true

### Page Data

* `{{context | json}}` - outputs the full array of page data
* `{{context.page.metadata}}`  - outputs the metadata of the page, though meta fields are usually automatically outputted for you.
* `{{context.page.metadata.name}}` - outputs the Name field of the page

## Example Page Header:

In this example, we check to see if the page name exists or not, as WebApp pages output their name differently. If there is a page name, it will display it, if not it will output the WebApp name instead.

```liquid
{% raw %}

{% raw %}
{% if context.page.metadata.name != undefined %}
    {{context.page.metadata.name}}
{% else %}
    {{context.exports.webapp_1.data.result.items[0].name}}
{% endif %}
{% endraw %}

{% endraw %}
```

## Example of URL based breadcrumbs:

This takes the URL path of the page, splits it based on / and titleizes the items.

```liquid
{% raw %}
{% assign slugSplit = context.location.pathname | remove_first: '/' | split: '/' %}
<ul>
    <li>
        <p>Home</p>
        <i class="fal fa-chevron-right"></i>
    </li>
    {% for item in slugSplit %}
        {% if forloop.last == true %}
            <li>
                <p>{{item | titleize}}</p>
            </li>
        {% else %}
            <li>
                <p>{{item | titleize}}</p>
                <i class="fal fa-chevron-right"></i>
            </li>
        {% endif %}
    {% endfor %}
{% endraw %}
</ul>

{% endraw %}
```
