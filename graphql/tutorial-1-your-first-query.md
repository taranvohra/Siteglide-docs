
Hello WebApp! In Tutorial 1, we'll use Siteglide CLI to open the GraphQL sandbox. There, you'll write your first query and retrieve details about some webapp items.

# Prerequisites

*   Know how to create a Site, with Starter Site Enabled. Learn more here: <https://help.siteglide.com/en/article/portal-all-sites-creating-editing-sites-uwv7in/>.  We'll be using a Starter Site as the basis for these tutorials, so that you'll instantly have familiar website data available to fetch via GraphQL. **Update 2024 - the original Starter Site mentioned here is being phased out. You can now install a new site from a greater choice of Site Templates here: **<https://admin.siteglide.com/#/portal/community/marketplace>

*   [Siteglide-CLI ](https://developers.siteglide.com/introducing-siteglide-cli)- You'll need to understand how to open terminal on your machine and navigate to your Project's root folder. You'll need to have installed Siteglide-CLI and its dependency Node.js. You can't use GraphQL without Siteglide-CLI.

*   [About GraphQL](https://developers.siteglide.com/about-graphql)- optional- Read more about GraphQL and when it might be best used.

# Introduction

In this first of the GraphQL Tutorials, you'll need to either create a new Starter Site, or open up a Starter Site you've created previously.

We'll use Siteglide CLI to open the GraphQL sandbox. There, you'll write your first query- which will ask for all the data on the entire Starter Site!

# Running the GraphQL sandbox

The GraphQl sandbox is a place for testing Graph Queries. It has the additional benefits of giving you suggestions and documentation alongside your code.

When you open the sandbox- you'll be opening it with your chosen environment. This means you're picking a Siteglide Site to give the sandbox access to- it will be able to find database items from this Site.&#x20;

For these tutorials, we strongly suggest you use a Starter Site- because then you'll have exactly the same data and it will be ready to go.

## Choose an Environment (Site) to Connect to

Change directory into your project folder (create a folder first if you don't have one).

![Using CLI to create a Siteglide-CLI environment](https://downloads.intercomcdn.com/i/o/180527221/658e6017e583bc2048313a4a/image.png)

Then add your Site as an environment - the quickest way to do this is to copy the CLI command from your site in the Portal- or you can replace the --url and --email flags with your own. Add your Siteglide Admin password when prompted:

![Finding the CLI add command in Portal](../../assets/5EeZeVWyDatmSDbw3m_QE_image.png)

![Entering the add environment command in CLI](https://downloads.intercomcdn.com/i/o/180528133/86e344294e3ff1476b8b463d/image.png)

## Run the Sandbox

The command for running the sandbox is (replace the `staging`placeholder with the name you chose in the previous step):

`siteglide-cli gui staging `

Success should look like this: 

![](https://downloads.intercomcdn.com/i/o/180528856/ad832e1c427625dbd6224359/image.png)
 
Click, Ctrl+click (if your machine allows), or copy the "GraphQL Browser" link into a browser. This will open the sandbox. 

*Short Method:*
If you want to save time and skip the step of opening the link, add the flag -o to automatically open the link after you run the command:

`siteglide-cli gui my_env -o`

Your First Look at the GraphiQL Sandbox

![](https://downloads.intercomcdn.com/i/o/180529609/798287616944808153c596e5/image.png)

To start with a few important features are hidden. Click and drag up the `QUERY VARIABLES` panel from the bottom left and click the `< Docs` button in the top right. We'll come back to these later.

Click the "Toggle Explorer" button to open the Explorer wizard. This is a new tool which will make writing (non-deprecated) queries even easier. 

![](https://downloads.intercomcdn.com/i/o/206666077/558d3a0137150f0d820d1adf/image.png)

You've now set up your GraphiQL sandbox!&#x20;

![](https://downloads.intercomcdn.com/i/o/206666353/08fadb604e7db05b329b2cd1/image.png)

# What does each panel in the GraphiQL Sandbox do?


*The Central Panel*

![](https://downloads.intercomcdn.com/i/o/206677522/30673d53393dcc6953fca87a/image.png)

This is where you write your Query

*The Results Panel*
This is where the data will be displayed in JSON format after your query fetches it.

![](https://downloads.intercomcdn.com/i/o/206679435/ae277c726ef088060ea11dd6/image.png)

*Query Variables Panel*
This is where you'll be able to simulate dynamic variable inputs when testing variables in your Query.

![](https://downloads.intercomcdn.com/i/o/206678240/23bcd258b16236c49f884999/image.png)

We'll cover this in a later Article.

*Explorer Panel \*NEW\**
This displays the GraphQL schema in the form of a "wizard". Tick the options you want to include and they will automatically be added to your query. This is the most user-friendly way to write queries for beginners (and possibly for the experienced GraphQL developers as well!). Note the explorer user-interface can't handle arrays of query language very well e.g. when filtering by multiple properties, even though it's valid GraphQL; when you hit a limitation like this, it's time to leave the explorer behind and write the code manually.&#x20;

![](https://downloads.intercomcdn.com/i/o/206678384/19a4ae63a807d44821e24d15/image.png)

The other limitation is that it doesn't currently support older deprecated query and mutation types, if you have a need to use those.

*Documentation Explorer Panel*

This displays the available GraphQL schema as documentation. It works with nested levels, so each time you choose an option you can "click through" to the next level of options you can include.

![](https://downloads.intercomcdn.com/i/o/206678616/6d8d4808512c16632f1e3d17/image.png)

This is less user-friendly than the new "Explorer" panel above, but can still be useful:

*   especially if you want to use a deprecated query like "customisations" (The only reason for using deprecated queries is that some support features like keyword search that are not supported on the more modern queries yet)

*   If you want to search the schema for features and understand which types are allowed

# A note on naming conventions

platformOS sometimes changes the names of elements of their schema for the sake of better communication or as part of a functionality update. For example, `models` have been now renamed to `records`.

We are in the process of upgrading these docs to refer to `records `instead of `models` but in the meantime there may be some screenshots which continue to show the older terminology.

# Your First Query

For your first query, we'll fetch every `record`on the Site. A `record`is a catch-all term for WebApp and Module items that we'll use in these tutorials. The term `records` does not refer to `users`, as these contain more core fields like `email `which set them apart and therefore they use a different query type: `users`.

In these tutorials, we'll break the process of building a query into steps. For each step we'll show you:

*   The code you need

*   Notes explaining the syntax of the code example in detail

*   A screenshot from the Explorer Panel, showing the checkbox needed to quickly insert this code \*NEW\*

We'll sometimes also include a screenshot of the Documentation Explorer Panel to illustrate it's use, but this depends on whether it seems useful or not!

## Step 1) Name your query

Code:

```graphql
query getEverything {
  
}
```

Notes:

*   The word query tells Graph we want to GET data, as opposed to modifying data. 

*   `getEverything` is simply a name we have given the query. It is optional and has no functionality. 

*   Curly braces `{ }` have been added - these will contain an object containing the *next level* of instructions we will give the query. The next level from here is also known as `RootQuery` as it is the most fundamental level at which we choose which type of query we'll use.

Explorer:&#x20;
The "Explorer" wizard will add this for you if you type out a name here:

![](https://downloads.intercomcdn.com/i/o/206685851/f4715210070ca6c376035e98/image.png)

## Step 2) Choose a Query type

The documentation panel on the right shows you the full range of query types available. Click `RootQuery` to see the options on this level.

![](https://downloads.intercomcdn.com/i/o/180532971/1f893ad2f59ceeba82e0af09/image.png)

You can also see a list of non-deprecated query types in the Explorer panel:

![](https://downloads.intercomcdn.com/i/o/206687020/3f7ebee19c41be1a1c9cece6/image.png)

We'll be choosing `records`for our first query. This will get us a list of `records `in the database.&#x20;

Code:

```graphql
query getEverything {
  records{
    
  }
}
```

Notes:

*   The new code goes within the first level of curly braces we opened in the previous step. Notice how our instructions are "nested" inside each other- like a "Russian doll", just as both the explorer panels show options nested inside each other. 

*   We open another pair of curly braces inside `records`. We'll add further options here.

Explorer:
Quickly implement this level in the Explorer Panel by selecting the `records `query type. This will also open the next level of options in the explorer:

![](https://downloads.intercomcdn.com/i/o/206693175/2940a78487ccc5a202762525/image.png)

## Step 3) Ask for results

A GraphQL query doesn't give you results unless you ask for them. This helps it to stay as efficient as possible. We'll ask the query to pass back some key information about the records it finds, such as their table (this will help us identify which WebApp or Module the item belongs to) and then all of its properties (fields). 

Next, we'll ask the query to return `results` and `total_entries`.&#x20;

Code:&#x20;

```graphql
query getEverything {
  records {
    total_entries
    results {
      table
      properties
    }
  }
}
```

Notes:

*   `total entries` returns an integer, so we don't need to give it any more information.

*   `results` requires us to specify which fields we want to return with those results. We open a new pair of curly braces and choose fields from the docs. Siteglide doesn't use all of these fields, so some will return `null` . You can use `properties` to return all fields which have a value. `table `will return the name of the `table `the `record `belongs to (this was previously called `model_schema_name`).

Explorer:

![](https://downloads.intercomcdn.com/i/o/206688864/bef388f233371ecd64de1f20/image.png)

## Step 4) Add Arguments

You can press the "play" button to test your query:

![](https://downloads.intercomcdn.com/i/o/180538499/48ea0d31c60849777af1abb8/image.png)


 Ours is not quite ready, and the error message in the middle-right Results Panel will tell us why:

```graphql
{
  "errors": [
    {
      "message": "Field 'records' is missing required arguments: per_page",
```

Arguments are passed into a query to modify its behaviour. They always use round brackets `( )` syntax, just like JavaScript. Different types of queries will require some arguments, while allowing others as optional arguments.

This query requires that we specify how many records we would like to retrieve on each page of the results. This is to make sure the query isn't slowed down by retrieving too many records at once. We'll learn how to navigate multiple pages later, for now we'll ask for the first 20 records. 

Code:

```graphql
query get_all_records {
  records(
    per_page: 20
  ) {
    total_entries
    results {
      table
      properties
    }
  }
}
```

Notes:

*   `per_page` expects an integer, not a string, so we don't need quotes around `20` 

Explorer:
You can set a value for `per_page` in Explorer.

![](https://downloads.intercomcdn.com/i/o/206689789/d61d40ec36686623288e3f22/image.png)

Notice that the asterisk by the option in Explorer lets you know the property is mandatory.

In Explorer, there is a subtle colour scheme to help you differentiate between setting arguments and returning results:

*   Arguments are in purple

*   Results, and other returned properties are in dark blue

## Step 5: Press play to fetch all results

If successful, you should see an object named "data" containing a tree of your results. Well done, you've written your first query! You've returned all `records`, or, in other words: WebApp and Module items.

![](https://downloads.intercomcdn.com/i/o/206691423/9e94964deda4cac212327fb6/image.png)

You'll see there are actually more `total_entries` than the 20 results shown. That's because we're only viewing the first Page of the Results. We'll look at Pagination in the next Article. 

# CRM Users

If you want to get information on Siteglide CRM Users instead of WebApp or Module records, you can use the `users `query instead of the `records `query. The main difference is that `users `can return `first_name`, `last_name`, `email `etc. inside the `results `curly braces. See the explorer panel or the documentation panel to learn more.

# Next Time

In the next Article we'll look at how  GraphQL organises results into pages. We'll look at how to:

*   change page 

*   change the number of items per page

*   output useful pagination metadata

**Let's go!**
