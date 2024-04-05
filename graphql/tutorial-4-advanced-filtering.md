
Following on from the previous tutorial, we'll look at more advanced filtering options and show how you can filter with multiple rules.

# Prerequisites

*   You have completed the Learning GraphQL tutorials 1 - 3

*   [About GraphQL](https://developers.siteglide.com/about-graphql)- optional- Read more about GraphQL and when it might be best used.

# Introduction

In the last tutorial, we looked at how to filter your results so that only items from `webapp_1` were returned. We also challenged you to see if you could adjust the query so that it returned all WebApp items. 

This time, we'll look at:

*   filtering by different fields, or properties

*   filtering with different kinds of rules

*   using more than one filter at once

# Filtering by Properties

Some fields in `records`are defined in the GraphQL schema, like `table`, this often means they have their own filter option in the documentation. Siteglide fields, and your own custom fields, are very likely to be custom "properties" which are not directly defined by the schema.

If you're not sure, check the schema for the field you're looking for. If you can't find it, it's a property.&#x20;

For example, `release_date` is not a custom field in the Siteglide Admin, but it's not in the list of available fields to filter by in the schema- so we'll need to use properties.

![](https://downloads.intercomcdn.com/i/o/186027288/55e5c1b79332537d80ed35ba/image.png)

A brief note on `name` . You'll see the term `name` available in the schema- but this is a deprecated way of referring to the `table`e.g. `webapp_1`. To fetch the name of the item in the Siteglide Admin, you'll need `properties.name`.

In our next example query, we'll demonstrate this. Let's search for items with a `properties.name` that contains the string "music". 

Code:

```graphql
query get_items_with_musical_names {
  records(
    page: 1
    per_page: 20
    filter: {
      properties: {
        name: "name", contains: "music"
      }
    }
  ) {
    total_pages
    results {
      table
      properties
    }
  }
}
```

Notes:

*   See that properties uses a colon : and then curly braces `{ }` as we have usually used so far. Properties can instead be used to store an array of filter objects, but we'll look at this later.

*   Note that we have to specify inside the curly braces both the `name` of the property we want to filter by (which happens here to also be called `name`, but it could also have been something else like `release_date`) and the method we'll be matching the value by, in this case `contains: music`. 

Explorer:
Adding a single filter to properties can be done with the Explorer wizard. However, if you want to be able to filter by an array of different properties, Explorer has no support for this yet, but it is possible by writing in the query manually.&#x20;

![](https://downloads.intercomcdn.com/i/o/206719259/963aa78169eb77996bf16138/image.png)

# Filtering Data Types Other than Strings 

In the examples so far, we've only filtered by strings- or in other words, groups of letters or characters. Next we'll look at some other data types:

*   Booleans

*   Integers / Epoch Date stamps

*   Arrays

## Filtering by Booleans

A good example of a Boolean property in Siteglide is `enabled`. This is a property which is stored as either `true` or `false` . Let's find all the items which are currently enabled:

Code:

```graphql
query get_enabled_items {
  records(
    page: 1
    per_page: 20
    filter: {
      properties: {
        name: "enabled", value_boolean: true
      }
    }
  ) {
    total_pages
    results {
      table
      properties
    }
  }
}
```

Notes:

*   Again, we need to specify the name of the property we'll be filtering by, this time: `enabled`.

*   We'll use `value_boolean` as the most appropriate way to match an exact Boolean value. It's not the only method we could choose from the documentation, but it's more specialised to filtering Booleans, so is potentially faster.

Explorer:

![](https://downloads.intercomcdn.com/i/o/206726728/089ee0ed0941f44bbce81df1/image.png)

## Filtering by Integers and Epoch Timestamp Dates

When filtering by integers (which also includes Siteglide's `release_date` and `expiry_date` fields, as these are stored as Epoch Timestamps) you've got a choice whether to filter by values or a range of values.

### Filtering for properties which match an exact integer

Code:

```graphql
query get_heavily_weighted_items {
  records(
    page: 1
    per_page: 20
    filter: {
      properties: {
        name: "weighting", value_int: 1
      }
    }
  ) {
    total_pages
    results {
      table
      properties
    }
  }
}
```

Notes:

*   `value_int` works the same as `value_boolean` but is designed to handle the different type of data more efficiently.

*   Be aware that running this query yourself on a Starter Site may produce no results. This is the correct result, because Starter Site does not at the time of writing ship with any weightings set. If you add a weighting of `1` in the Admin, you'll see it appear in the results. 

Explorer:

![](https://downloads.intercomcdn.com/i/o/206727192/ef1365e490c66dc4547aed03/image.png)



### Filtering for integer properties which fall inside a range

&#x20;Most often, you'll want to use more complex comparisons for integers. We'll look at how to do this next- at the same time, we'll take a look at how Siteglide normally formats dates.

The dates are stored in Epoch Timestamp format, which is an integer storing the number of seconds which have elapsed since the Epoch. You can convert a date of your choice to this format here: <https://www.epochconverter.com/>

In this example, I'll use the time at the current time of writing: `1582108820`. Let's query for all items which have already been released. In other words, the value stored in `release_date` should be less than, or equal to, the current timestamp.  When you're thinking about dates, you can think of "less than" as meaning "before" and "greater than" as meaning "after". So here we're asking for "items with a release\_date before now".

Code:

```graphql
query items_already_released {
  records(
    page: 1
    per_page: 20
    filter: {
      properties: {
        name: "release_date", range: {lte: "1582108820"}
      }
    }
  ) {
    total_pages
    results {
      table
      properties
    }
  }
}
```

Notes: 

*   The range filter requires you create a new object `{ }` containing some logical comparison operators. You can choose between the operators in the documentation panel- see below.

Documentation Panel: 

*   Available operators can be seen under `RangeFilter`. They are short for `Greater Than` , `Greater Than or Equal` , `Less Than` and `Less Than or Equal`.

![](https://downloads.intercomcdn.com/i/o/186051482/cfe3b246861b0fd38042dd11/image.png)

Explorer:

![](https://downloads.intercomcdn.com/i/o/206727637/d7f7d52145a417d5ecca1bb8/image.png)

## Filtering by Arrays

An array is a list of data. One good example in Siteglide is `category_array`, which stores a list of unique IDs that refer to categories. We can now write a query to find items in a particular category.&#x20;

Code:

```graphql
query mens_clothing {
  records(
    page: 1
    per_page: 2000
    filter: {
      properties: {
        name: "category_array", value_in: ["158198"]
      }
    }
  ) {
    total_pages
    results {
      table
      properties
    }
  }
}
```

Notes: 

*   `value_in` is special to fields which have an array data type. 

*   It takes an array of strings `["string_1", "string_2"]` as its value. Here we are just using one category ID as an example. You could experiment with combinations of category\_ids. 

Explorer:
Only *partial support* is currently available in Explorer for this. It's not so good at handling arrays. So you can select the property in Explorer, but you'll need to add the value manually into your query.

So firstly, implement with the wizard:

![](https://downloads.intercomcdn.com/i/o/206729672/26e3eab0e3daf66d9b63c44f/image.png)

Secondly, change the value manually in the code from:

`value_in: "158198"`...to: `value_in: ["158198"]`

# Filtering by Multiple Fields

For all the filters you've learned in this Article and the previous Article, you can apply more than one at once.

```graphql
query released_mens_clothing_products {
  records(
    page: 1
    per_page: 2000
    filter: { 
      table: {value: "module_14/product"}
      properties: [
        { name: "category_array", value_in: ["158198"] },
        { name: "release_date", range: {lte: "1582108820"} }
      ]
    }
  ) {
    total_pages
    results {
      table
      properties
    }
  }
}
```

Notes:

*   In this example, `table`and properties are both chosen as filter options. 

*   `properties` takes an array (denoted by square brackets `[ ]` ) of objects (denoted by curly braces `{ }`

*   Each pair of curly braces `{ }`  inside `properties` should contain the `name` of the property and an independent filtering method e.g. `range` or `value` which will be used.

*   Using a combination of filters in this way generally follows AND logic. Items must pass all of the filtering tests you choose before they are returned.

Explorer:
Unfortunately, arrays are not currently supported in Explorer, so you'll have to enter this section of the query manually for now.

# Filtering by whether a Property Exists - or doesn't exist!

You can also find items where a property does, or doesn't exist. 

In this example, we're looking for WebApps where a `meta_title` was not added.&#x20;

Code:

```graphql
query webapps_missing_meta_descriptions {
  records(
    page: 1
    per_page: 2000
    filter: { 
      table: {starts_with: "webapp"}
      properties: [
        {
          name: "meta_title", exists: false
        }
      ]
    }
  ) {
    total_pages
    results {
      table
      properties
    }
  }
}
```

Notes:

*   exists accepts a Boolean, so you can use `false` or `true`. This shouldn't be wrapped in quotes, because Booleans don't require them.

Explorer:

![](https://downloads.intercomcdn.com/i/o/206731347/d274318e212e7e35fa949042/image.png)

# \*New\* Filtering with OR logic

&#x20;What if you are looking to filter `records `so you can find `records `which fit either one rule or another- but don't need to match both rules?

Here's an example from the pOS team of how you can use the "or" option when filtering. In this example we get `records `where either a `webapp_field_1_1 `exists OR a field `parent `exists.

```graphql
query {

  records(per_page: 2000, filter: {

    or: [

      { 

        properties: [

          { name: "webapp_field_1_1", exists: true } 
      	]

      },

      {

        properties: [

          {name: "parent", exists: true}

        ]

      } 
    ] 
  }) { 
    results {

      id

      table

      properties

    }

  }

}

```

Notes:&#x20;

*   Inside `filter` we add an or property and an array with square brackets `[]`

*   This array takes one or more objects with curly braces `{}` each Object is compared with OR logic. Within the object, you can use the same properties you might normally use inside `filter`.

You can add multiple filter properties inside each object, but these will be compared with AND logic. So, to filter records by those which have both ( `webapp_field_1_1 `AND `webapp_field_1_2`) OR "parent", you would do the following:

```graphql
query { 
  records(per_page: 2000, filter: { 
    or: [ 
      {  
        properties: [ 
          { name: "webapp_field_1_1", exists: true },
          { name: "webapp_field_1_2", exists: true }  
      	] 
      }, 
      { 
        properties: [ 
          {name: "parent", exists: true} 
        ] 
      } 
    ] 
  }) { 
    results { 
      id 
      table
      properties 
    } 
  } 
} 
```

# Challenge!

See if you can write one query which uses multiple filters. Try and return `records`which meet these criteria:

*   They are an item from a `record`with a `table`starting with `module_` .

*   They are `enabled`

*   They have already been released

*   They have not yet expired

*   They have a weighting between 1 and 3

*   They have a meta\_title

*   They fall into the `posters` category

Hint: This search is so specific, that by default on Starter Site it will return no results. Try creating an eCommerce Product which meets these criteria before you start- that way, you'll know when you've succeeded.

It's unusual to run this many filters at once. Most of the time in a real use case, you'd have less to write than this! However, putting together everything you've done so far will be good practice.

We'll look at the answer to this Challenge in the next Article.

# Next Time

We'll look at a possible solution to our latest challenge question.

After that, we'll look at how to run a query on a real Siteglide Site for the first time- and look at what you can do with the results.
