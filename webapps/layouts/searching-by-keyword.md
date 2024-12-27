How to use the `use_search` parameter in the WebApp include tag, along with a keyword parameter in the URL, to search for items.

## Prerequisites

- You have <a href="/webapps/quickstart-webapps.md" target="_blank">created a WebApp</a>
- You have [added a WebApp List View to a Page](/webapps/layouts/webapp-list-layout)

## Introduction

This is the easiest way to allow users to search for WebApp items on the Front End.

You can use a string of words to search all fields in the WebApp. Using OR logic, Siteglide will return all results where at least one keyword matches in one of the item's fields. The number of results will still be limited by pagination.

If you want to control which fields are searched, see <a href="https://docs.siteglide.com/en/webapps/go-further-webapps/searching-advanced-filtering" target="_blank">Searching - Advanced Filtering</a>.

### Steps

1. Add the `use_search` parameter to WebApp include tag 
2. Test by adding a URL query parameter
3. Build a form to allow Users to enter a search query

## Step 1 - Add the use\_search parameter to WebApp include tag

```liquid
{% raw %}
{%- include 'webapp'
  id: '1'
  layout: 'my_layout'
  per_page: '10'
  use_search: 'true' 
-%}
{% endraw %}
```

## Step 2 - Test by adding a URL query parameter

Since you have added the `use_search` parameter to the Liquid, Siteglide is now checking the URL for the keyword parameter.&#x20;

It will use this parameter's value to search all your WebApp's fields and return all items where at least one of keyword's words matches at least one word in the WebApp's fields.

With your site open in your browser, add the parameter to the URL to test this. Remember the example keyword is unlikely to be found in your unique WebApp, so choose something you know is there! You should see your WebApp's results adjust as only items which match are returned:

`https://my-website.staging.oregon.platform-os.com/webapp-list?keyword=my%20search%20terms`

## Step 3 - Build a form to allow Users to enter a search query

You can now build an input form to pass the user's chosen keywords as parameters to the URL.
