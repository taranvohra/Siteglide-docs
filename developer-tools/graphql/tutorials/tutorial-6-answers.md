# Tutorial 6 - (Answers)

Last Time we challenged you to pull together everything you'd learned to create some Pagination Buttons powered by Graph. Answers here!

![](https://siteglide-52c14a1a8a9b.intercom-attachments-1.com/i/o/202146871/9e8f1b8fb1d3b5ccda64a8ec/Screen-20Recording-202020-04-20-20at-2004.32.00.25-20PM.gif)

## Challenge Objective

For this challenge, we'd asked you to set up your own simple Pagination controls. This combined several of the skills you've learned so far. As usual, don't worry if you need to check these answers before completing the challenge on your own.

On a new Page you create, the User should be able to see the first three Items in the Gallery WebApp.

Then, when they press the Page 2 button, the Page should refresh and they should see the second Page of Results.

## Step 1) Writing the Graph Query

Firstly, here's the query without variables.

```graphql
query gallery_by_page {
  records(per_page: 3, page: 1, filter: {table: {value: "webapp_1"}}) {
    page #optional
    results {
      properties
      id
    }
  }
}
```

Now let's add the variables:

```graphql
query gallery_by_page($page: Int) {
  records(per_page: 3, page: $page, filter: {table: {value: "webapp_1"}}) {
    results {
      page #optional
      properties
      id
    }
  }
}
```

Notes:

* The most difficult part here might have been working out the type. Here the query expects Page to be an integer. The documentation panel confirms this:
* From the documentation panel, you can also see "= 1" after the type. This is a default, which means if no variable is passed through, the variable will be given a default value of 1. Not all variables will have defaults.
* The type here does not have an exclamation mark ! so the query won't deliberately fail if no value is passed in.
* We set `per_page` to 3

## Step 2) Sync the Query to the Site using Siteglide-CLI

Refer back to [Tutorial 5](/developer-tools/graphql/tutorials/tutorial-5-using-liquid-to-run-graphql-queries-on-your-site.md) to refresh these steps.

## Step 3) Adding the HTML Controls

We gave you these in the tips. You'll have needed to add them on a Page of your choice.

```liquid
{% raw %}
<ul>
  <li><a href="{{context.headers.PATH_NAME}}?page=1">1</a></li>
  <li><a href="{{context.headers.PATH_NAME}}?page=2">2</a></li>
  <li><a href="{{context.headers.PATH_NAME}}?page=3">3</a></li>
</ul>
{% endraw %}
```

Pressing one of the buttons will redirect us to the same Page, but will be adding a `page` query parameter to the URL. This is the easiest way to pass variables to Liquid- because Liquid runs before the Page loads, and the URL is one of the only available sources of dynamic information at this point.

It's also possible to pass information to Liquid on another Page via an XHR request. This can lead to smoother UX, but is more challenging and will be covered in a future tutorial.

## Step 4) Reading the URL Parameters

Let's say we pressed the second button, our relative URL will now be:`/my-page-slug?page=2`

As we showed you in the tips, Liquid can read this parameter at the following dot-notation path. This will output the value on the Page: `{{context.params.page}}`

Or you can store this in a variable, which we'll need to do here:

```liquid
{% raw %}
{% assign current_page = context.params.page %}
{% endraw %}
```

By the way, the keys in `context.params` are dynamically generated for any query parameter in the URL, so you can pass through any variable you like with this method.

## Step 5) Feeding the Variables into the Query

a) First, let's set a default value, just in case a User arrives at the Page without setting the Parameter:

```liquid
{% raw %}
{% assign current_page = context.params.page | default: 1 %}
{% endraw %}
```

b) The query is expecting an integer, so let's apply an Integer filter that will change the type to an `Int` without changing the value: 

```liquid
{% raw %}
{% assign current_page = context.params.page | default: 1 | plus: 0 %}
{% endraw %}
```

c) Let's add the `graphql` tag with the variable parameter.

```liquid
{% raw %}
{% assign current_page = context.params.page | default: 1 | plus: 0 %}
{% graphql my_result = "gallery_by_page",
page: current_page
%}
{% endraw %}
```

## Step 6) Output the Results

We can output the results using the variable name we defined in the `graphql` tag.

```liquid
{% raw %}
{% assign current_page = context.params.page | default: 1 | plus: 0 %}
{% graphql my_result = "gallery_by_page",
page: current_page
%}
{{my_result}}
{% endraw %}
```

If pressing the HTML anchors changes the results by fetching different "pages" of JSON results, you've been successful. Congratulations.

If you're having difficulty with any of these steps still, please don't hesitate to ask for help on the Forum.

## Full Code

_Liquid_

```liquid
{% raw %}
{% graphql my_result = "gallery_by_page",
page: current_page
%}
<pre>{{my_result}}</pre>
<ul>
  <li><a href="{{context.headers.PATH_NAME}}?page=1">1</a></li>
  <li><a href="{{context.headers.PATH_NAME}}?page=2">2</a></li>
  <li><a href="{{context.headers.PATH_NAME}}?page=3">3</a></li>
</ul>
{% endraw %}
```

_GraphQL_

```graphql
query gallery_by_page($page: Int) {
  records(per_page: 2, page: $page, filter: {table: {value: "webapp_1"}}) {
    current_page #optional
    results {
      properties
      id
    }
  }
}
```

## Optional- Taking this further

The next steps give you ideas for how to take this further. They are not part of the initial challenge!

### Step 7) Output a Layout (Optional)

These JSON results don't look great. Remember, you can use Liquid to pass the results into a Layout- if you can find that Layout's relative path in Code Editor.

```liquid
{% raw %}
{% assign current_page = context.params.page | default: 1 | plus: 0 %}
{% graphql my_result = "gallery_by_page",
page: current_page
%}
{% assign result_array = my_result.records.results %}
{% for this in result_array %}
  {% include 'layouts/webapps/webapp_1/list/my_layout_name', this: this %}
{% endfor %}
{% endraw %}
```

However, you won't have access to the user-friendly names for fields in that Layout, because GraphQL will output the raw database IDs for fields.

You'll want to target fields in this Layout with syntax like:`{{this.properties.webapp_field_1_2}}`

You can view the database IDs for fields in the Admin using the toggle in the top-right of the screenshot, or you can look at the keys in the JSON results.

### Step 8) Use the Results of the Query to only show buttons you need. (Optional)

By returning `total_pages` from the query, we'll know exactly how many Pagination buttons to display:

```graphql
query gallery_by_page($page: Int) {
  records(per_page: 3, page: $page, filter: {table: {value: "webapp_1"}}) {
    current_page
    total_pages
    results {
      properties
      id
    }
  }
}
```

You can then use this to manipulate the HTML pagination controls:

```liquid
{% raw %}
<ul>
  {% for page in (1..my_result.records.total_pages) %}
    <li><a href="{{context.headers.PATH_NAME}}?page={{page}}">1</a></li>
  {% endfor %}
</ul>
{% endraw %}
```

## Next Time

Next time, we'll learn how to sort the results of your Query.

**Let's go!**
