# Tutorial 6 - Variables

## Tutorial 6 - Variables

Adding variables to your query allows you to filter results based on User interaction - and re-use queries dynamically.

## Introduction

So far, we've set up queries which return the same set of results each time.

Variables allow you to make queries which:

* Can be re-used in different situations
* Can search, sort, filter and change page based on User Interaction
* Can show information which a particular User has permission to access

There are three main steps to setting up variables in a query:

* Define the variables
* Replace hard-coded values in the query with variables
* Pass in values for the variables

There is no set order in which to follow these steps, as you'll need to follow all three before the query works as expected.

## Our Example

In this Article, we'll use the following query as an example.

```graphql
query find_items_with_category { 
  records(  
   per_page: 2000,
    filter: {
    deleted_at: {exists: false}
      properties: [
        { name: "category_array", value_in: "98486" }
      ]
    }
  ) {
    results {
      id
      properties
    }
  }
}
```

As you might have guessed, this query aims to find WebApp or Module items with a particular category assigned to them.

As it stands, the query is not very useful or repeatable. We want to be able to pass in the category we're interested in as a variable. This would allow different Pages to use the same query to view different categories - or allow the User to choose which category they wish to view.

## Using Variables inside the Query

Normally in programming you would define the variables before you use them.

The benefit of adding the variable where you'll use it first is that the error message will tell you information about which type of data the variable will need to be.

In our example query, we'll remove the hardcoded category ID and replace it with the name of our new variable `$category`.

Code:

```graphql
query find_items_with_category { 
  records(  
   per_page: 2000,
    filter: {
      deleted_at: {exists: false}
      properties: [
        { name: "category_array", value_in: $category }
      ]
    }
  ) {
    results {
      id
      properties
    }
  }
}
```

Notes:

* All variables inside the query itself must be preceded with a dollar $ sign.
* This query will currently fail, because we still need to define the variable.

Explorer: Sorry, explorer does not currently support arrays or variables, so no demo is available this time.

## Defining Variables

Next, we'll define the variables we will use. These definitions will be entered as arguments on the top level of the query.

Each variable you define has two parts:

* A name e.g. $category
* A data type e.g. String

Here's what just the top level looks like with the newly added argument:

```graphql
query find_items_with_category($category: String) { 

}
```

Here's the whole query:

```graphql
query find_items_with_category($category: String) { 
  records(  
   per_page: 2000,
    filter: {
      deleted_at: {exists: false}
      properties: [
        { name: "category_array", value_in: $category }
      ]
    }
  ) {
    results {
      id
      properties
    }
  }
}
```

Notes:

* The variable name is again preceded with a dollar sign $.
* A colon : and an Title Case keyword are used to set the type. See below for more information on types.
* We've deliberately made a mistake with the type of the variable- we'll discuss this below.

Explorer: Sorry, explorer does not currently support arrays or variables, so no demo is available this time.

### Using the Correct Type

A variable's type is really important and an error will be thrown if you use the wrong one. For example, running our query now gives the following error:

```graphql
{
  "errors": [
    {
      "message": "List dimension mismatch on variable $category and argument value_in (String / [String!])",
```

We can use the error message to find the type we need- in this case it's `[String!]` not `String`. This indicates that an array of Strings is expected, which makes sense because "value\_in" is for filtering array fields. You can also check in the documentation panel:

We'll fix this in our query:

```graphql
query find_items_with_category($category: [String!]) { 
  records(  
   per_page: 2000,
    filter: {
      deleted_at: {exists: false}
      properties: [
        { name: "category_array", value_in: $category }
      ]
    }
  ) {
    results {
      id
      properties
    }
  }
}
```

What's important is the type of data that a particular GraphQL property expects as its value, not the type of data you were intending to pass in. In fact, you may have to modify the type of your variable with Liquid beforehand, so that it is acceptable to GraphQL.

### Mandatory Variable Types

An exclamation mark after a type e.g. `String!` means that this variable will be mandatory. The query will _not_ run without it. This is useful when that variable is used to control sensitive information- terminating the query if you can't be sure which data you need to return. However, it's important to make sure ordinary user behaviour can't cause this to happen, because the error message can be bad for UX.

### Array Variable Types

Square brackets around a value, indicate that it should be an array (which may have any length). E.g.

`[String]`

### Examples of using Liquid to modify data types

If you require any other conversions, please request them on Intercom and we'll try and include them in the List.

\*String to Int \*Apply an integer filter:

```liquid
{% raw %}
{% assign original_string = "123" %}
{% assign new_int = original_string | plus: 0 %}
{% endraw %}




```

_String to Float_

```liquid
{% raw %}
{% assign original_string = "123" %}
{% assign new_float = original_string | plus: 0.00 %}
{% endraw %}




```

_String to \[String]_

```liquid
{% raw %}
{% assign original_string = "123,456" %}
{% assign new_array = original_string | split: "," %}
{% endraw %}




```

_String to Boolean_

```liquid
{% raw %}
{% assign original_string = "true" %}
{% if original_string == "true" %}
  {% assign new_boolean == true %}
{% elsif original_string  == "false" %}
  {% assign new_boolean == false %}
{% endif %}
{% endraw %}




```

_Boolean to String_

```liquid
{% raw %}
{% assign original_boolean = true %}
{% assign new_string = original_boolean | downcase %}
{% endraw %}





```

_Int to String_

```liquid
{% raw %}
{% assign original_int = 123 %}
{% assign new_string = original_int | downcase %}
{% endraw %}
```

_Float to String_

```liquid
{% raw %}
{% assign original_float = 123 %}
{% assign new_string = original_float | downcase %}
{% endraw %}
```

_Literal JSON object to HASH object_ (Needed for advanced variables only- like passing an array of properties objects into a filter). You can also use the parse\_json tag to create any of the above types; if you can write the variable in a type that's supported by JSON, the tag will convert that to a variable in the hash format that can be passed into Graph as a variable value.

```liquid
{% raw %}
{% parse_json properties_object %}
  [
    { "name": "properties.webapp_field_1_1", exists: true },
    { "name": "properties.webapp_field_1_2", exists: true }
  ]
{% endparse_json %}
{% endraw %}




```

## Passing in Variables using the Sandbox (Testing)

You can test by entering values in JSON format in the panel in the bottom left. The panel may be hidden, in which case you'll need to click and drag it up.

Firstly, open a new JSON object:

Next, define the key of your property:

```graphql
{
  "category": 
}
```

And finally, define the value of your category. Make sure the data is in the type you defined earlier. Here are some examples:

* String - `` `"Hello"` ``
* Int - `3`
* Float - `3.2`
* Boolean - `true`
* \[String] (Array of Strings) - `["Hello", "Hi"]`

In our example, we will need an array of Strings:

```graphql
{
  "category": [ "98486" ]
}
```

Notes:

* This time, you won't need to use a dollar sign $. That's because this panel represents the input and is not part of the GraphQL query- it doesn't use GraphQL syntax, instead it uses JSON syntax.

Our query is now finished:

Explorer: Sorry, explorer does not currently support arrays or variables, so no demo is available this time.

## Passing in Variables using Liquid

Okay, so now you can use the GraphiQL Sandbox to test your queries with variables, but the really useful bit is to be able to use Liquid to pass variables in. This will unlock the ability to fetch data dynamically with GraphQL.

Step 1) Add parameters to the graphql tag for each variable you've defined in the Query. Here, we'll continue with our example and add `category`

```liquid
{% graphql my_results = "find_items_with_category",
 category: 
 %}

```

Notes:

* We will add the value of the category variable in the next step.
* You don't need to use a dollar sign $ before the name of your variable.
* You can add new lines to the inside of the tag to keep it tidy, or write the tag on one line, it's up to you.

Step 2) Next, add the value of the parameter.

You can either hardcode the value:

```liquid
{% graphql my_results = "find_items_with_category",
 category: "98486"
 %}


```

Or, you can use a Liquid variable which you defined earlier:

```liquid
<!-- Create an empty array -->
{% raw %}
{% assign current_category_array = "" | split: "," %}
<!-- Add Strings to the Array -->
{% assign current_category_array = current_category_array | add_to_array: "98486" | add_to_array: "98487" %}
{% endraw %}

<!-- Feed the Liquid Array into the query by its variable name. No quotes are needed around a variable name when you set it as a parameter- it's dynamic data. -->

{% graphql my_results = "find_items_with_category",
 category: current_category_array
 %}

```

Or, you can use data from Siteglide that's already stored in a Liquid variable. In this case, let's say we're in an item.liquid file for a Product. We already have access to the Categories that this Product is assigned to - luckily, the data is already a Liquid Array. Let's use that data to find other records in the same Category.

```liquid
{% graphql my_results = "find_items_with_category",
 category: this.category_array
 %}


```

## Challenge - Using Page as a Variable

![](https://siteglide-52c14a1a8a9b.intercom-attachments-1.com/i/o/202146518/becaf5c2241ec74d0f8c41de/Screen-20Recording-202020-04-20-20at-2004.32.00.25-20PM.gif)

### Challenge Objective

For this week's challenge, we'd like you to set up your own simple Pagination controls. This will combine everything you've learned so far. As usual, don't worry if you need to check the answers before completing it.

On a new Page you create, the User should be able to see the first two Items in the Gallery WebApp. Then, when they press the Page 2 button, the Page should refresh and they should see the second Page of Results. See the gif above for a demonstration.

In the Tips section, we'll give you the HTML and Liquid you need to get started, your challenge is to build the GraphQL query which will power the functionality.

### Tips

Here are some snippets of code you can use to help you:

\*User Interaction \*You can use anchors to allow the User to refresh the Page and change the Page Parameter in the URL.

```liquid
<ul>
  <li><a href="{{context.headers.PATH_NAME}}?page=1">1</a></li>
  <li><a href="{{context.headers.PATH_NAME}}?page=2">2</a></li>
  <li><a href="{{context.headers.PATH_NAME}}?page=3">3</a></li>
</ul>
```

\*Reading URL parameters \*You can use Liquid to read the Page parameter in the URL. You'll then need to work out how to feed this variable into your GraphQL query: \`

\`

By the way- we're using the filters `| default` and `| plus: 0` to make sure the page defaults to 1 if no parameter exists, and that the data is converted to an integer.

\*Remembering Pagination in GraphQL \* You may need to refer to [Tutorial 2](/developer-tools/graphql/tutorials/tutorial-2-pagination.md), to refresh your understanding of Pagination.

## Next Time

We'll look over the answers to our toughest challenge yet.

**Let's go!**
