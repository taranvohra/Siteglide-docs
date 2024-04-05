---
title: Tutorial 3 - Filtering the Results
slug: huDo-
createdAt: Wed Feb 17 2021 12:11:06 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Dec 27 2023 14:18:16 GMT+0000 (Coordinated Universal Time)
---

You shall not pass! This time, we'll look at how you can use filters to only return results based on specified rules.

# Prerequisites

*   You have completed the Learning GraphQL tutorials 1 - 2. You can find the previous tutorial [here](https://developers.siteglide.com/tutorial-2-pagination)

*   [About GraphQL](https://developers.siteglide.com/about-graphql)- optional- Read more about GraphQL and when it might be best used.

# Introduction

`records`in the database have a `table`which tells us which WebApp or Module they belong to.

This time, we'll look at how you can use filters to only return results with a particular `table`, or with a `table `which matches a certain pattern. 

# Returning The Gallery WebApp

The Starter Site comes packaged with a ready-built WebApp with the id of `1` and the name `webapp_1`. 

## Step 1: Load the previous query

We'll return to our query from the previous tutorial, but this time, we'll rename it from `get_all_records`  to `get_webapp_1` to reflect the different purpose we intend for it. We'll also be wanting to look at `page 1` again.&#x20;

Code:

```graphql
query get_webapp_1 {
  records(
    page: 1
    per_page: 20
  ) {
    current_page
    total_pages
    results {
      table
      properties
    }
  }
}
```


Explorer:

![](https://downloads.intercomcdn.com/i/o/206703771/4fc28e56aa305cc7246b14b5/image.png)


Step 2: Add the filter argument
-------------------------------

Next, we'll add a filter argument:

Code:

```graphql
query get_webapp_1 {
  records(
    page: 1
    per_page: 20
    filter: {

    }
  ) {
    current_page
    total_pages
    results {
      table
      properties
    }
  }
}
```

Notes:

*   As an argument for the `records`query, this goes inside the round brackets after `records`.

*   Like the other arguments, `filter` is followed by a colon `:`

*   We have more settings to choose next (`filter` is an object) so we add curly braces `{ }` 

Explorer:

![](https://downloads.intercomcdn.com/i/o/206704320/bd8b3ad94a46a5ef7d75a6e1/image.png)



## Step 3: Filter by the table

&#x20;In this tutorial we'll choose the `table`to apply the filter to, because we're looking for items with the `table`of `webapp_1`.&#x20;

Code:

```graphql
query get_webapp_1 {
  records(
    page: 1
    per_page: 20
    filter: {
      table: {

      }
    }
  ) {
    current_page
    total_pages
    results {
      table
      properties
    }
  }
}
```

Notes:

*   We've chosen `table` as the only filter. In the next tutorial we'll explore using other fields, and filtering by more than one field at once.

*   This field also contains further options, so we use a colon `:` followed by curly braces `{ }` to contain the next set of options.

Explorer:

![](https://downloads.intercomcdn.com/i/o/206704959/c902a03c3f1130a8e7d42bb5/image.png)



## Step 4: Define the filtering rule

&#x20;We now have a choice about:

1.  How closely our value should match with the contents of a field before a match is returned. We'll use `value` (the exact value).

2.  The value we are matching against. We'll use `webapp_1` .

```graphql
query get_webapp_1 {
  records(
    page: 1
    per_page: 20
    filter: {
      table: {
        value: "webapp_1"
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

*   `value` is a key and is followed by a colon : 

*   Our value `"webapp_1"` must be a String, so we wrap it in double quotes.

Documentation panel: 

*   Selecting RecordsFilterInput gives you options for different filtering rules you can apply:

![](https://downloads.intercomcdn.com/i/o/185824786/90063b3476c0dc3f64e16b89/image.png)

*   After the colons `:` you can see the type of value expected for each of these keys. They are mostly strings `String` or arrays of strings `[String]`. This topic will be covered in more detail in later tutorials. Keep an eye out for the different data types expected by GraphQL in the meantime.

Explorer:
When implementing this using the Explorer, the wizard will help you get the type of value correct. In this case, it provides you with quotes so that you can enter the value as a String:

![](https://downloads.intercomcdn.com/i/o/206706642/0d3b707603b34f1728386700/image.png)

&#x20;

&#x20;

# Returning Items from the Blog Module

You can adjust the filter to return items from a specific Module item only. In this example, we'll specify `module_3` which is the Blog Module.

Code:

```graphql
query get_blog_module {
  records(
    page: 1
    per_page: 20
    filter: {
      table: {
        value: "module_3"
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


Explorer:

![](https://downloads.intercomcdn.com/i/o/206707131/e9fa3f76d39f4cd030187682/image.png)

This should return Blog Posts from the Blog Module. 

# Returning Form Submissions

You can adjust the filter to return Form Submissions from a specific Form only. In this example, we'll specify form\_1 which is the Newsletter Sign Up Form.

Code:

```graphql
query get_newsletter_signups {
  records(
    page: 1
    per_page: 20
    filter: {
      table: {
        value: "form_1"
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


Explorer:

![](https://downloads.intercomcdn.com/i/o/206707418/074e81dd0ed77fc4e300216f/image.png)



# Challenge!

## Introduction to GraphQL Challenges

In order to learn GraphQL, you'll need to start experimenting with what you've picked up from this tutorials. 

To help you do this, we'll now start to set you some challenges. These will ask you to tweak the examples we've given you so far and see if you can achieve the desired results. 

We'll always give you the answers to the challenge in the following Article, so don't worry if you get stuck. 

## Your Challenge is to Write a Query which returns Items from all WebApps but not Module items

To carry out this challenge, you will need to create a second WebApp and add a couple of items in the Admin.
By experimenting with the options in the documentation panel, see if you can filter the results so that:

*   your query returns all items with the `table`of `webapp_1` 

*   your query returns all items with the `table`of `webapp_2`

*   your query does not return items which start with `module_` 

*   your query does not return Form submissions which start with `form_`

We'll go over the answer to this challenge in the next Article.&#x20;

# Next Time

We'll look at a possible solution to our challenge.
After that, we'll continue to look at filtering queries in more detail, including:

*   filtering by different fields, or properties

*   filtering with different kinds of rules

*   using more than one filter at once

