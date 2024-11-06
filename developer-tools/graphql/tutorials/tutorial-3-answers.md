
We look at a possible answer to Tutorial 3's challenge. This shows how to write a query which fetches all WebApp items, not Module items.

# Prerequisites

*   This Article shows the Answers to a Challenge. If you've not had a go at the challenge yet, we'd recommend you [head there first](https://developers.siteglide.com/tutorial-3-filtering-the-results).

*   [About GraphQL](https://developers.siteglide.com/about-graphql)- optional- Read more about GraphQL and when it might be best used.

# Challenge Answers

The trick here was to examine the `tables`and spot the common patterns in their values. 

The two types of `records`we wanted had these `tables `beginning with "webapp\_":

*   `webapp_1`

*   `webapp_2`

The types of `records `we don't want have `table `values without "webapp\_", for example:

*   `module_3` - (Blog Module)

*   `module_14` - (eCommerce Module)

*   `form_1` - Newsletter Sign Up Form Submissions

So, in order to filter for the `records`we do want and not the `records`we don't want, we need `records`which start with the string `webapp_`. 

Code:

```graphql
query get_all_webapps {
  records(
    page: 1
    per_page: 20
    filter: {
      table: {
        starts_with: "webapp_"
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

*   In this method, there is no need to write one filter to include `webapp` items and another to remove `module` and `form` items from the Results. This is because the given rule efficiently achieves both at once.

Explorer:

<!-- ![](https://downloads.intercomcdn.com/i/o/206709413/5f5a3592d2e2a3911903ec4f/image.png) -->

This is just one possible answer, you may have found a different method. 

Try and make sure you choose the best method for your use case. You should always be looking out for a more efficient way of doing things.

# Next Time

We'll continue to look at filtering queries in more detail, including:

*   filtering by different fields, or properties

*   filtering with different kinds of rules

*   using more than one filter at once

**Let's go!**
