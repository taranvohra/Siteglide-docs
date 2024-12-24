---
title: Tutorial
slug: qP49-
createdAt: 2021-02-17T16:16:50.000Z
updatedAt: 2023-03-03T08:09:58.000Z
---

# Accessing Data in Liquid Variables - Tutorial 1 - Using Dot Notation

This Liquid is useful when you are accessing a WebApp 'collection', creating a Categories layout, using a custom GraphQL query and more.

## Prerequisites

* Choose your favourite third party tool for parsing and formatting JSON. Everyone has a different favourite tool, but you can see a third party comparison here to help you get started and find one: [https://geekflare.com/json-online-tools/](https://geekflare.com/json-online-tools/) We'll look at this again below in "Using a Third Party Tool to Visualise Objects"

## Introduction

Understanding dot notation is a really useful skill for Developers who are trying to get the most out of Siteglide and the platformOS technology it runs on. This Getting Started Article will cover:

* What is dot notation?
* How to find a property of an Object
* How to chain dot-notation
* The Data Tree
* Visualising the Data Tree

You will come across the following terms which might be new:

* Object
* Array
* Key-value Pairs
* properties
* Curly Bracket

This Article is intended to be the starting point for a Series of Articles involving dot notation.

* [Advanced Dot Notation- Arrays and Key Maps](/developer-tools/liquid/accessing-data-by-looping-or-iterating-arrays-or-objects.md)
* [Using WebApp Collections- Tutorial](/developer-tools/liquid/using-collections-with-webapps-and-modules.md)

## What is dot notation?

Normally when you're accessing data on Siteglide, you simply want to access a single value. For example, on a Starter Site (using the WebApp installed by default, Gallery), you might need to output a Title on your Layout: `{{this.Title}}`

In this example, this outputs a String: `The Latest Music`

You could use this syntax from memory, or by referring to the Docs, but you're actually already using dot notation. The syntax above takes a variable `this` which returns an object. `.Title` is dot notation which specifies that the Developer wants to access the `Title` which is a property of `this`.

Note: Sometimes you may see something like this: `{{this['Title']}}` This is the exactly same thing, except this alternative syntax also allows you to add spaces in field names. We'll cover this in more detail in the next Article.

### Key Value Pairs

Another important piece of terminology is the concept of a Key-Value Pair.

A key is a place where data is stored; a value is the data itself.

In the previous example, `this` and `Title` are both keys. The _key_ `Title`has the _value_ `The Latest Music`.

### Chaining

You can chain dot notation. The following example will output the first name of the User currently signed in to a Secure Zone: `{{context.current_user.first_name}}`

This accesses the `context` object, then accesses its `current_user` property and finally accesses the `id` property of `current_user`. `current_user` can be considered an Object, because it has properties of its own, however, `id` has no properties and is stored as a String.

## The Data "Tree"

You can think of objects in pOS and Siteglide as a Tree. The Object you start on like `context` or `this` is like the trunk of the tree. Each time you use a dot to access a property, you are going one level down the tree, until you reach the branch of data you needed.

Just outputting `this` on its own would show you the real JSON Object behind the first example in this Article and all of its properties: `{{this}}`

This outputs an object of data, which to start with is a little hard to read. That's because whitespace is removed for efficiency reasons. Adding the whitespace back in with a third party tool will allow us to read it more easily (see the next section).

```json
{
  "id":"98656",
  "properties": {
    "name":"The Latest Music",
    "slug":"the-latest-music"
  }
}
```

## Visualising the Object "Tree"

To make sense of the JSON that the Liquid outputs, you'll need a tool for automatically formatting the JSON data and adding whitespace. Some tools even help you visualise the data in other more advanced ways.

We don't have a favourite JSON parsing tool, but you can see a third-party comparison here: [https://geekflare.com/json-online-tools/](https://geekflare.com/json-online-tools/) Many Code Editing environments like VSCode also have a useful extension for prettifying JSON data.

{% hint style="danger" %}
#### Important Note

We'd recommend when parsing JSON using third party tools that you do not use sensitive Client data. It's best to use test data and publically accessible data when testing and developing dot-notation. We cannot verify that any third party tool will handle your data safely.
{% endhint %}

#### Visualising the Data

Here is an example of a tree-view. It's the JSON data with extra whitespace and newlines added for readability (colours too).

<!-- ![](https://downloads.intercomcdn.com/i/o/170900129/70897663e71f69098f379221/image.png) -->

From this view you can make the same observations we made when using the \<pre> tag, but it is easier because each level of the tree is indented and all keys are coloured light blue:

* The first and last character is a curly bracket- this represents the this object we are accessing.
* The key id has no properties, it has a value of `98656` which is stored as a String. this.id will be enough to access it.
* The key properties has properties which are accessible by dot notation. You can tell because the properties key is followed by more curly brackets indicating that it is an object. All the properties inside this set of curly brackets are properties of properties. `` `{{this.properties.name}}` `` will access the name property of properties.

Here is a chart view from the same tool. It shows more clearly how some objects are nested within others. You can use this to help you chain dot-notation to get the values you need.

<!-- ![](https://downloads.intercomcdn.com/i/o/170899985/1ff54ab397ab0f29e7404df0/image.png) -->

## A Special Case - Arrays

You may notice that `category_array` looks slightly different in the examples above. This is because its value is an array. You can notice an array in your data when square brackets are used around a list of values separated by commas e.g `"category_array":["98479", "111111"]`

We will cover arrays in the next Article: Advanced Dot Notation: Arrays and Key Maps
