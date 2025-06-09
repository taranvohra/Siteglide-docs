# Tutorial 2 - Pagination

Turning the Page! In tutorial 2, we'll control how many items Graph returns on each Page of results and retrieve specific Pages.

## Prerequisites

* You have completed the [first Learning GraphQL tutorial](tutorial-1-your-first-query.md).
* [About GraphQL](../about-graphql.md)- optional- Read more about GraphQL and when it might be best used.

## Introduction

When GraphQL returns results, it will organise them into pages.

This allows it to be more efficient, as it only returns the data that is needed straight away. At the same time, the rest of the pages are organised ready for the next request.

You'll always need to think about Pagination when using GraphQL, even you only want to retrieve the first Page of results.

## Per Page

`per page` is an argument used to define the number of results that will be returned on each page.

It's now a mandatory argument on some types of query so we've already got the argument in our query from the last tutorial:

```graphql
query get_all_records {
  records(
    per_page: 20
  ) {
    total_entries
    results {
      model_schema_name
      properties
    }
  }
}
```

Experiment by changing the integer in the argument from `20` to another value, e.g. `1`. Observe the difference. It's recommended to keep the per\_page number as low as possible- for efficiency and performance.

Let's consider a few situations:

* You want to display 3 items - Set `per_page` to 3- only the three items you need will be retrieved.
* You want to display 20 items at a time, but allow the user to view the next 20 when they've finished reading - Set `per_page` to 20
* If you want the user to be able to change `per_page` dynamically, we'll cover this when we look at variables in a future tutorial.
* If you think you need to display more than 2000 items at a time (perhaps to provide data to a JavaScript plugin), consider using GET requests to a custom Liquid endpoint page to fetch each page of results asynchronously. You can learn more in [Tutorial 8 - Building a Liquid API GET Endpoint Page powered by GraphQL queries](tutorial-8-building-a-liquid-api-get-endpoint-page-powered-by-graphql-queries.md) but we recommend working through the other tutorials first.

## Returning Pagination Metadata

You can return pagination metadata alongside your query results:

* `current_page` - Returns the number of the current page.
* `per_page` - Returns the number of items on every page.
* `has_previous_page` - A boolean which is true if there is a page before the current page.
* `has_next_page` - A boolean which is true if there is a page after the current page.
* `total_pages` - Returns an integer representing the total number of pages in these results.

These optional properties can be requested alongside `total_entries` and your `results` object, like in the example below. Try them out. Code:

```graphql
query get_all_records {
  records(
    per_page: 20
  ) {
    current_page
    total_pages
    has_previous_page
    has_next_page
    per_page
    total_entries
    results {
      model_schema_name
      properties
    }
  }
}
```

Notes:

* Properties like `has_next_page` and `has_previous_page` are most useful for adding pagination buttons of your own.
* You can see that by default, we get the first page of results- so `page` returns `1`.

Explorer:

## Changing the Page

You can view other pages by setting the `page` argument to the page of results you'd like to see.

Code:

```graphql
query get_all_records {
  records(
    page: 2
    per_page: 20
  ) {
    current_page
    total_pages
    results {
      model_schema_name
      properties
    }
  }
}
```

Explorer:

## Next time

In the next Article, we'll look at how to filter results.

For example, we'll learn how to return items from only a specific WebApp.

**Let's go!**
