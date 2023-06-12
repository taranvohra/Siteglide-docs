You can change the type and order of sorting. You can also sort by multiple properties at once.

# Introduction

&#x20;In this Article, we'll look at how you can instruct the query to return items in an order of your choice.&#x20;

Using sort along with pagination means you can make sure the first pagen of results shows you the items you're interested in.
Using sort along with variables allows you to let your end-User customise the sort order themselves. &#x20;

# Sorting by a Single Property

&#x20;In this example, we'll start with a query which fetches the Categories.

Code:

```graphql
query sorted_categories {
  models(per_page: 2000, filter: {model_schema_name: {contains: "category"}}) {
    results {
      model_schema_name
      id
      properties
    }
  }
}
```

## Step 1) First, we'll add in a sort parameter

Code:

```graphql
query sorted_categories {

  models(per_page: 2000, sort: {}) {

    results {

      model_schema_name

      id

      properties

    }

  }

}
```

Notes:

*   As a parameter, sort is contained within the round brackets after the query type

Explorer:

![](https://downloads.intercomcdn.com/i/o/213365154/e71b1872daa311c2f4b2376b/image.png)

## Step 2) Next, you can add a sort method.

&#x20;You can either use:

### 2) a) A field from the main options

Code:

```graphql
query sorted_categories {

  models(per_page: 2000, sort: {created_at: {}}) {

    results {

      model_schema_name

      id

      properties

    }

  }

}
```

Explorer:

![](https://downloads.intercomcdn.com/i/o/213366703/cd9dc582ba4bd8cbf2c0de3e/image.png)

&#x20;

### 2) b) a property from properties

Code:

```graphql
query sorted_categories {

  models(per_page: 2000, sort: {properties: {name: "weighting"}}) {

    results {

      model_schema_name

      id

      properties

    }

  }

}
```

Notes:

*   Remember, any field which is not a Platform default field will be a property. This means any field not listed in the other options, including several Siteglide fields such as "weighting". Default fields tend to be like created\_at automatically filled in when an item is created.

Explorer:

![](https://downloads.intercomcdn.com/i/o/213367555/4bfc9b8c5cdb438b0ae0a568/image.png)

&#x20;

## Step 3) Select a sort order

You can choose between the keywords DESC (descending) and ASC (ascending).

Code:

```graphql
query sorted_categories {

  models(per_page: 2000, sort: {properties: {name: "weighting", order: DESC}}) {

    results {

      model_schema_name

      id

      properties

    }

  }

}
```

Explorer:

![](https://downloads.intercomcdn.com/i/o/213369158/2aa128cce3b9bb8de24b141d/image.png)

&#x20;

# Sorting by Multiple Properties

Sometimes you may want to initially sort by one property, e.g. weighting, but then some items may have a blank weighting property. Those items where the sort field is blank will go to the end of the results list, but you can add additional sort conditions to sort these further.

Let's say we wish to firstly sort by "weighting", then sort those items without a weighting by the "release date".

Code:

```graphql
query sorted_categories {

  models(per_page: 2000, sort: {

    properties: [

      {name: "weighting", order: DESC}, 
      {name: "release_date", order: DESC}

    ]

  }) {

    results {

      model_schema_name

      id

      properties

    }

  }

}
```

Notes:&#x20;

*   Here we use an array with square brackets `[]` to add multiple sorting objects with curly braces `{}`

*   Unfortunately, arrays are not yet supported by the Explorer, so you'll need to add this code manually.&#x20;

*   You can use different sort orders for each condition

# Next Time

If you want to challenge yourself, you could choose to try making a query which uses variables to change the order and field by which results are sorted.

Next time, we'll look at how to implement keyword searches in your query. To do this, we'll look at a new type of query "customizations" instead of "models".
