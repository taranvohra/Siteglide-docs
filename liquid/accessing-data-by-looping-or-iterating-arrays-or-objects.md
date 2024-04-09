---
title: Advanced- Arrays and Key Maps- Tutorial
slug: 98it-
createdAt: 2021-02-17T12:59:21.000Z
updatedAt: 2023-03-03T08:09:58.000Z
---

How to use Liquid For Loops and Indexing to handle arrays. Also, how to use a key to access key maps, using categories as an example.

# Prerequisites:

This Article is the second in a series on using Dot Notation in Siteglide. We strongly recommend reading the Article below first:

*   [Getting Started with Dot Notation](https://developers.siteglide.com/tutorial)

# Introduction

If you're using dot notation, you'll probably come across arrays and maps. The syntax for dealing with them is slightly different, but this actually makes them more powerful when you're building complex Layouts. 

The examples below focus mainly on Categories because they are a good example of arrays and maps.

# Arrays

An array is a group or list of data. A key might have a single value, or an array of values.&#x20;

In Siteglide for example, each WebApp item for example has a field called `category_array` which stores a list of the IDs of every Category assigned to that item. The more categories an item belongs to, the longer the array. E.g. `{ "category_array":["98479", "111111"] }`

If you try to use standard dot notation as we practised in the previous Article, you will be able to output the array as it is using the key `category_array` and the liquid `{{this.category_array}}`:&#x20;

`["98479", "111111"]`

However, there aren't many places where this would actually be helpful.&#x20;
It would probably be more useful to do one of the following:

*   Access one of the Array items by its Index

*   Loop over the array Items

*   Find the length of the array (how many items are there?)

# Accessing an Array by its Index

Arrays have an index, which means they are numbered. In Siteglide (and in JavaScript) Arrays are zero-indexed, meaning the first item has the index of `0` while the second item has the index of `1`. 

We can access the first value in the `category_array` by its index using the following Liquid:
`{{this.category_array[0]}}`outputs `98479`

Note that straight after the key, we give the index number of the value we want in square brackets. If the array contained objects, you could go a step further and access one of their properties with a dot after the square brackets.&#x20;

# Looping the Array to Access all Values in it

We can access all values in the Array using a Liquid For Loop:

```liquid
{% raw %}
{% for item in this.category_array %}

  {{item}}<br><br>

{% endfor %}
{% endraw %}
```

This outputs:

```liquid
{% raw %}
98479

111111
{% endraw %}
```

# Finding the Length of an Array

You can find the length of an array using a Liquid filter: `{{this.category_array | size}}`
outputs: `2`

# Maps 

As well as arrays, you might come across a map of data. Here is an example which can be tried on any Siteglide Starter Site using the Liquid: `{{context.exports.categories}}`

It outputs something like this (but I've shortened it here!):

```liquid
{% raw %}
{"items":
  {
    "98490":
{"id":"98490"
  "external_id":"category_57703"
  "name":"Women"
  "parent":"98487"
  "slug":"women"
  "image":null
  "description":null
  "meta_title":"Women"
  "meta_desc":null
  "og_title":null
  "og_desc":null
  "og_type":null
  "twitter_type":null
  "full_slug":"/our-products/merch/clothes/women"},
    "98489":{"id":"98489"
             "external_id":"category_57701"
             "name":"Men"
             "parent":"98487"
             "slug":"men"
             "image":null
             "description":null
             "meta_title":"Men"
             "meta_desc":null
             "og_title":null
             "og_desc":null
             "og_type":null
             "twitter_type":null
             "full_slug":"/our-products/merch/clothes/men"}
  }
}
{% endraw %}
```

A map is used to store data when you know the ID of an item and want to fetch it using it's ID as a key. In Siteglide we use them for performance reasons. You can tell this is a map, because the key `items` contains several comma-separated objects instead of a single value. Each of these has a key representing an ID, instead of the name of a property. 

Let's say you have the ID of a category, but you want to display the Category's name:
`{{context.exports.categories.items["98490"].name}}`

This outputs: `Women`

This sounds odd, but it's the name of the eCommerce Category we wanted! You can achieve the same if you have the ID stored as a variable:

```liquid
{% raw %}
{% assign my_example_category_id = 98490 %}

{{context.exports.categories.items[my_example_category_id].name}}
{% endraw %}
```

## Looping over a Map

You can loop over all keys in a key map using a Liquid FOR loop. Inside the loop, each key-value pair is treated as an array with the key being the first item in the array and the value being the second and last value in the array.&#x20;

In this example, we'll loop over all Categories in `context.exports.categories.data` and see what data is available to output:

```liquid
{% raw %}
{% for item in context.exports.categories.data %}
  {{item[0]}} <!-- Outputs the key, which in this case is the ID of the category -->
  {{item[1]}} <!-- Outputs the value, which in this case is an object containing this category's fields. You can see all available fields by outputting it. -->
  {{item[1].name}} <!-- Outputs the name of the Category in this iteration of the loop. -->
{% endfor %}
{% endraw %}
```

# Using what you've learned so far

Here's a challenge you can try.

Can you create a WebApp with Categories and in your Layout output a list of the Category names that belong to the item?

Step 1) Create a WebApp and assign more than one Category to each of the Items.&#x20;
Step 2) In the Layout, access the this object.
Step 3) Use your Understanding of arrays to loop through every category belonging to the item.&#x20;
Step 4) Use your understanding of maps to find the name of each category in the Loop and output it. 

# Next Article

Next, we'll look at how you can use dot-notation to work with WebApp collections: Using WebApp Collections
