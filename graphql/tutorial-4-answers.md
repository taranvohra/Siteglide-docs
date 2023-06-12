In our Tutorial 4 challenge, we asked you to write a query which returned items matching multiple filter rules. Here's a possible solution.

# Prerequisites

*   This Article shows the Answers to a Challenge. If you've not had a go at the challenge yet, we'd recommend you [head there first.](https://developers.siteglide.com/tutorial-4-advanced-filtering)

*   [About GraphQL](https://developers.siteglide.com/about-graphql)- optional- Read more about GraphQL and when it might be best used.

# Introduction

Last time, we asked you to write a single query which utilised a combination of filters to find `models` which meet these criteria:

*   They are Module Items

*   They are `enabled`

*   They have already been released

*   They have not yet expired

*   They have a `` `weighting` `` between 1 and 3

*   They have a `meta_title `

*   They fall into the posters Category


This challenge required you to modify and combine the queries we'd already looked at. If you were able to match at least some of the criteria, good work.

# Challenge Answers

To find the category\_id for the `posters` Category. One way to do it would have been to go to the Siteglide Admin:&#x20;

![](https://downloads.intercomcdn.com/i/o/186111084/6f18c1efb54bd90ef6715a24/image.png)


After that, it was a case of combining what you'd learned so far to add multiple filters to a query:

```graphql
query webapps_missing_meta_descriptions {
  models(
    page: 1
    per_page: 2000
    filter: { 
      model_schema_name: {starts_with: "module_"}
      properties: [
        { name: "meta_title", exists: true }
        { name: "enabled", value_boolean: true}
        { name: "release_date", range: { lte: "1582108820" }}
        { name: "expiry_date", range: { gt: "1582108820" }}
        { name: "weighting", range: { gte: "1", lte: "3" } }
        { name: "meta_title", exists: true }
        { name: "category_array", value_in: ["158197"] }
        
      ]
    }
  ) {
    total_pages
    results {
      model_schema_name
      properties
    }
  }
}
```

Notes:

*   For the `range` of `weighting` we've added a `gte` and `lte` setting, in order to demonstrate the possibility. This is not really necessary as there won't be values less than 0, but it's not a bad idea to rule these out, should data be entered incorrectly. 

*   The `category_array`  ID may be different from one site to another. Check your site's `category_id` in the Admin. 

Explorer:
Unfortunately, as mentioned last time, Explorer does not yet support arrays, so it's not possible to show an Explorer demo for this challenge.&#x20;

# Next Time

It's time for the real thing! We'll look at how you can save your GraphQL query in a File and use Liquid to run it on a website Page.

**Let's go!**
