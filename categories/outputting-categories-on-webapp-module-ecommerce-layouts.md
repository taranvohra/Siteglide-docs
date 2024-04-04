# Outputting Categories on WebApp / Module / eCommerce Layouts

This Article shows how you can use the category\_array field to access the IDs of the Categories assigned to a WebApp or Module Item

## Introduction

In this set of Articles, we'll show you the Liquid syntax needed to get the most out of [Categories](https://help.siteglide.com/article/123-categories-getting-started) on the Front End.

The following features are available in WebApp and Module Layouts only, as they require access to a particular Item's `category_array` field. In Module Layouts, they'll only be available in the `item.liquid` file.

* Using the category\_array field to access the IDs of Categories that have been assigned to the current Item
* Displaying all Categories that belong to the current Item
* Displaying the first, last or nth Category which belongs to the current Item
* Check if an Item has an Nth Category assigned to it

## Accessing the Category Array Field

Each WebApp or Module Item has a Category Array field stored inside the `this` object. For WebApps, you can access this in the Layout file. For Modules, you can access this in the `item.liquid` file in the Layout folder: `{{this.category_array}}`

This will output the IDs of Categories which are assigned to the current Item in an array e.g. if the Item is assigned to Categories with ID 1 and 2 it will look like this:

```json
[
  "1",
  "2"
]
```

## Displaying all Categories that belong to the current Item

To loop over all these Category IDs you can use a Liquid For Loop:

```liquid
{% raw %}
{% for category in this.category_array %}
  {{category}} <!-- outputs the ID of the Category -->
{% endfor %}
{% endraw %}
```

Once you have the Category ID, you can use the Categories data object to access any other Category fields, e.g. the name:

```liquid
{% raw %}
{% for category in this.category_array %}
  {{context.exports.categories.data[category]}} <!-- outputs this Category JSON Object -->
  {{context.exports.categories.data[category].name}} <!-- outputs this Category name -->
{% endfor %}
{% endraw %}
```

## Displaying the first, last or nth Category which belongs to the current Item

Instead of using a Loop, you can access a specific index of the `category_array` field and use it to fetch a particular Category ID.

### First in Category Array

You can use the following to only output the name of the first category assigned to the Item:`{{context.exports.categories.data[this.category_array.first].name}}`

### Last in Category Array

You can use the following to only output the name of the last category assigned to the Item:`{{context.exports.categories.data[this.category_array.last].name}}`

### Nth in Category Array

You can use the following to only output the name of a specifc category assigned to the Item, by its zeroed-index, where 0 is the first and 1 is the second:

```liquid
<!-- Fetch second Category name -->
{% raw %}
{% assign categoryID == this.category_array[1] %}
{% endraw %}
{{context.exports.categories.data[categoryID].name}}
```

## Check if an Item has an Nth Category assigned to it

If you want to make sure the category item in the array you are calling exists first, then you should do the following: First category in the array:

```liquid

{% raw %}
{% if this.category_array[0] != blank %}
    {{context.exports.categories.data[this.category_array[0]].name}}
{% endif %}
{% endraw %}

```

Second category in the array (and so on):

```liquid

{% raw %}
{% if this.category_array[1] != blank %}
    {{context.exports.categories.data[this.category_array[1]].name}}
{% endif %}
{% endraw %}
```
