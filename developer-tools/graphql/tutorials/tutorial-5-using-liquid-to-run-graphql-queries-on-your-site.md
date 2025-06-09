# Tutorial 5 - Using Liquid to run GraphQL queries on your Site

You've now used the GraphQL playground to write queries which fetch data. Now you're probably itching to see how you can add one to a Site!

## Prerequisites

* You've completed the "Learning GraphQL" tutorials 1 - 4.
* In order to use GraphQL results on your Page, you'll need to be familiar with Dot Notation Liquid syntax. You can get started with learning to use [Dot Notation here](../../liquid/accessing-data-from-liquid-objects.md). You may find that you want to refer back and forth between articles on Dot Notation and GraphQL as you continue with your learning.
* You'll need to be familiar with Siteglide-CLI. In this tutorial we'll be using Siteglide-CLI to add a GraphQL folder and sync our new queries up to the Site.
* [About GraphQL](../about-graphql.md)- optional- Read more about GraphQL and when it might be best used.

## Introduction

Last time, we looked at how to use `filter` to refine your queries so that they only return results matching particular criteria.

So far we've been working in GraphiQL, the interative playground. This time, we'll run a GraphQL query on your Starter Site. We'll also take a quick look at how to handle the results- but you can learn more about this by following our Documentation on [Dot Notation](../../liquid/accessing-data-from-liquid-objects.md) and [Collections](../../liquid/using-collections-with-webapps-and-modules.md).

## Saving your GraphQL File

The best way to run your GraphQL query on a Site is to save the query inside a GraphQL file. This keeps it tidy and allows you to easily re-use the same query elsewhere on the Site should you need to.

### Step 1) Find or Create a Project Folder on your Device

If you're following this tutorial with the same Site each time, you'll already have a project folder. After all, we have been using the `.siteglide-config` file in your Project Folder to interact with the GraphiQL interactive playground.

In this example, my project folder

### Step 2) Use Siteglide-CLI to pull down the Site's main File Structure

We need to add a GraphQL query inside a specific folder in order to refer to it with Liquid. Before we do that- we need to see your Site's File Structure so we know where to add the folder.

In terminal, you'll need to change directory to the Project Folder.

If you've not already, run a pull command in terminal to pull down the current file structure: `siteglide-cli pull my_environment_name`

If you want to refresh your memory on using the Siteglide-CLI, you can learn more\*\* here\*\*.

### Step 3) Load the Project Folder in a Text Editor/ Code Editor

I'll be using Microsoft Visual Studio Code in this example. Other Editors are available.

All the folders and files that can be synced with your Site are in the `marketplace_builder` folder.

### Step 4) Add a new folder called `graph_queries`

Open up the `marketplace_builder` folder. If you've not already got a folder inside this called `graph_queries` , create one now.

### Step 5) Create a new file in that folder to store your GraphQL Query inside

Create a new file to store your query inside. It's best to give the file the exact same name as your query. This will make it easier to find later.

The file should have the extension `.graphql`.

### Step 6) Use Siteglide CLI to sync or deploy that file to your Site

So that file now exists on your device, but not yet on your Site. You'll need to either `sync` or `deploy` the file to your Site.

The choice of command is up to you. `sync` will watch for changes in the `marketplace_builder` folder, so you'll need to make a change in the file after running the command before your file is uploaded. The `sync` command will continue to watch and sync files until you cancel it. `deploy` will simply `deploy` all your local files to the Site as a one off command.

Here, I'll use sync:

This query file _will not be visible_ in Code Editor, but the files will be on the server and Liquid will be able to access them. The reason for not displaying them here is to hide the most complex code from areas where Clients and non-developers can access it. This might change in the future.

If you wanted to check if the file has synced correctly, you can turn off `sync`, delete the file and run a `pull` command. In our experience, there's no need to run this check, as sync will tell you if a file is synced and "done" accurately.

## Adding the GraphQL Liquid Tag

We'll use the `graphql` Liquid tag provided by platformOS. You may see other developers familiar with platformOS using tags like `query_graph` or `execute_query`, but `graphql` is the most up-to-date:

```liquid

<div data-gb-custom-block data-tag="-"></div>

<div data-gb-custom-block data-tag="-" data-my_results='get_items_with_musical_names'></div>

<div data-gb-custom-block data-tag="-"></div>
```

Notes:

* The tag itself is `graphql`
* The first parameter you give should be a new variable name. This will create a Liquid variable containing your results- you can choose your own name.
* After the equals = sign, you should write the file name of your GraphQL file, without its file extension or any folders. For example, my filename is `"get_items_with_musical_names.graphql"` so I remove the extension: `"get_items_with_musical_names"` .

## Accessing the Results

You can output all of your results on the Page, using Liquid output syntax `{{ }}` to output the variable we defined earlier.

```liquid
{% raw %}
{% graphql my_results = "get_items_with_musical_names" %}
{% endraw %}
{{my_results}}

```

Notes:

* The Liquid output must be on any line below the `graphql` tag.
* You can output this in any Liquid File; this includes Pages, Page Templates, Headers, Footers, Layouts, Code Snippets and Workflow/ Auto-Responders.

The results will output in Hash format. You can use dot notation to access specific results within the Object.

## Looping over the Results

This example uses dot notation.

It is possible to use your Query to rename the keys in your Results- doing this would require different dot notation. We'll look at this later.

For now, we'll be using the query below, which does not rename any keys. I've set `per_page` to 2, in order to make the example data Object shorter and easier to read.

Code:

```graphql
query get_items_with_musical_names {
  records(
    page: 1
    per_page: 2
    filter: {
      table: { starts_with:  "webapp_"  }
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

### Step 1) Output the Results as shown above

### Step 2) Find the key which holds the main array of results

My Page returns the following results- don't worry- there's no need to read them in this form:

Running these results through a 3rd-party JSON parser gives me the data in a format which is much easier to read. We don't recommend any particular JSON parser, but if you're using a text editor there will normally be an extension available which does this.

The structure of the results here matches the results we see in the GraphQL playground. We're looking for the key which returns an _array_ of results- this is indicated by the square bracket `[ ]`:

The dot notation to reach the results is:

```liquid
{% raw %}
{% graphql my_results = "get_items_with_musical_names" %}
{% endraw %}
{{my_results.records.results}}

```

Alternatively, you can always run your query in the GraphiQL Playground and work out the dot notation needed from the results shown in the middle-right panel. You'll just need to ignore the very top key in the results `data`: and use the variable from your `graphql` tag instead e.g. `my_results` :

### Step 3) Implement a Liquid For Loop to loop over the results

```liquid
{% raw %}
{% graphql my_results = "get_items_with_musical_names" %}
{% for this in my_results.records.results %}
{% endfor %}
{% endraw %}

```

We loop over every item in the Results array. We create a variable called `this` with a scope which allows it to be accessed only inside each loop iteration. `this` contains all the data for that result.

### Step 4) Output properties inside each Item's iteration

In this example, we'll output:

* the `table`
* An example property `name`
* An example property `webapp_field_1_2` . This is the second custom Field defined in the WebApp's structure on Starter Site.

We can now also bring in other Front End languages. I'll add some common HTML tags.

```liquid
{% raw %}
{% graphql my_results = "get_items_with_musical_names" %}
{% for this in my_results.records.results %}
  <h1>{{this.table}}</h1>
  <h2>{{this.properties.name}}</h2>
  <p>{{this.properties.webapp_field_1_2}}</p>
{% endfor %}
{% endraw %}
```

This gets me the following Results on the Page:

## Outputting Layouts

You can use a Liquid `include` tag to output a Layout to display your results. The trick is to make sure that the data fits the same format as the layout is expecting.

You can learn more about this topic [here](../../liquid/using-collections-with-webapps-and-modules.md), as it works in the same way as displaying Collection Results in a Layout.

## Congratulations

You've reached the end of the first collection of our Learning GraphQL tutorials.

By now, you should be able to:

* Set up a development environment to test GraphQL queries
* Run GraphQL queries on a Siteglide Site
* Understand and use GraphQL Pagination
* Use GraphQL filters

New Tutorials will be added soon!

## Next Time

There's no official challenge for this tutorial, because you probably want to experiment with adding queries to your Site.

In the next Tutorial, we'll look at using variables in your Queries to make them more dynamic. We'll look at how you can use variables:

* In the GraphiQL playground
* Using Liquid in a Page

**Let's go!**
