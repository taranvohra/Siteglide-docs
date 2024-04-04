# Outputting Category Fields in any Location

This Article shows you how you can access Categories' fields on any Liquid Page -If you're beginning to develop with Categories, start here!

## Introduction

In this set of Articles, we'll show you the Liquid syntax needed to get the most out of [Categories](https://help.siteglide.com/article/123-categories-getting-started) on the Front End. This time we'll look at the Categories Object. This makes information about your Site's Categories available via Liquid. It can be accessed in any Liquid file on Siteglide.

We'll cover:

* Outputting the Categories data Object
* Accessing a specific Category via ID
* After accessing the Category, outputting its fields
* Looping over all Categories on the Site

## Outputting the Categories data Object

The following Liquid outputs a JSON object containing the details of all Categories:`{{context.exports.categories.data}}` This object is a "key map" with every Category stored in key-value pairs where the key is the ID of the Category and the value is an object containing all other available fields.

## Accessing a specific Category via ID

As the Categories data Object is a key map, you can access any specific category by accessing the object and then passing in the Category's ID in square brackets: `{{context.exports.categories.data['1234']}}`

## Accessing a Category's Fields

Once you've accessed the value of that Category via it's ID, you can access that Category's Fields using dot notation. For example, here we'll access its name: `{{context.exports.categories.data['1234']}}.name`

Other available fields are:

* `id` - the ID of the Category
* `name` - the name of the Category
* `parent` - the ID of the Parent Category if there is one
* `slug` - the end of the URL for the Category Detail Page which is unique to this Item
* `meta_title` - the meta-title of the Category
* `meta_desc` - the meta-description of the Category
* `og_title` - the open graph title of the Category
* `og_desc` - the open graph description of the Category
* `og_type` - the open graph type of the Category
* `twitter_type` - the twitter type of the Category
* `full_slug` - the full (relative) URL for the Category Detail Page

## Looping over all Categories on the Site

If you wish to display all the Categories on the Site, you can loop over them all. Inside the For Loop you can display any HTML or Category fields you like.

```liquid
{% raw %}
{% for category in context.exports.categories.data %}
  {{category[0]}} <!-- Category ID -->
  {{category[1]}} <!-- Current Category JSON Object -->
  {{category[1].name}} <!-- Accessing current Category's field e.g. name -->
{% endfor %}
{% endraw %}
```

If you want to skip any Categories, you can use Liquid if statements and the `continue` tag to do this:

```liquid

{% raw %}
{% for category in context.exports.categories.data %}
  {% if category[1].name == "name_of_category_I_want_to_skip" %}
    {% continue %}
  {% endif %}
  {{category[1].name}} <!-- Accessing current Category's field e.g. name -->
{% endfor %}
{% endraw %}
```
