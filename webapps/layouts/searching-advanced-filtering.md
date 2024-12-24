# 📋 Searching - Advanced Filtering

How to use the `use_adv_search` parameter in the WebApp include tag, along with a URL parameters, to search for within specific fields of an item.

### Prerequisites

* You have [created a WebApp](https://help.siteglide.com/article/126-webapps-getting-started#2-creating-your-webapp)
* You have [added a WebApp List View to a Page](/webapps/layouts/webapp-list-layout.md)

### Introduction

Advanced search allows you to use AND or OR logic to filter WebApp items by specific fields.

If you are looking to search for WebApp items which match any of your search terms in any of their fields using OR logic, see [Searching - Keyword](/webapps/go-further-webapps/searching-by-keyword.md).

#### Steps

1. Identify the IDs of the Custom Fields that you want to filter by
2. Add the `use_adv_search` parameter to WebApp include tag
3. Setting the match type for String fields
4. Setting the match type for Array fields
5. Test by adding a URL query parameter
6. Build a form to allow Users to enter a search query

### Step 1 - Identify the IDs of the Custom Fields that you want to filter by

In the database, each field has an ID that is different from their user-friendly name. In order to use the advanced search, you will need to know the ID of the field.

You can learn more about why we use Custom Field IDs and how to find the one you need for a WebApp or Module here: [Custom Field IDs](developer-tools/configuration/custom_fields.md)

Once you've checked that Article and found the ID of the Custom Field you need, you can move on to Step 2.

### Step 2 - Add the use\_adv\_search parameter to WebApp include tag

```html
{%- include 'webapp'
    id: '1'
    layout: 'my_layout'
    per_page: '10'
    use_adv_search: 'true' 
-%}
```

### Step 3 - Setting the match type for String fields

Let's work with a field ID of `webapp_field_1_1`. You have 2 options for setting the match type when searching:

* AND (default) - The search will return exact matches for the search term it receives
* OR - The search will return results where there is a match on any of the search terms it receives. These terms are comma separated.
  * For example, if we have `webapp_field_1_1=content 1,content 2&webapp_field_1_1_match_type=OR` then we will be looking for items where `webapp_field_1_1` is either equal to 'content 1' OR 'content 2'.

You can find what type your fields are [here](/developer-tools/configuration/field-types.md).

### Step 4 - Setting the match type for Array fields

Let's work with a field ID of `webapp_field_1_2`. You have 2 options for setting the match type when searching:

* AND (default) - The search will return items that contain all search terms. These terms are comma separated.
  * For example, if we have `webapp_field_1_2=option1,option2&webapp_field_1_2_match_type=AND` then we will be looking for items where `webapp_field_1_2` contains both 'option1' AND 'option2'.
* OR - The search will return results where there is a match on any of the search values it receives. These terms are comma separated.
  * For example, if we have `webapp_field_1_2=option1,option2&webapp_field_1_2_match_type=OR` then we will be looking for items where `webapp_field_1_2` contains either 'option1' OR 'option2'.

You can find what type your fields are [here](/developer-tools/configuration/field-types.md).

### Step 5 - Test by adding a URL query parameter

Now `use_adv_search` has been added, Siteglide is watching the query parameters for any parameters with a key including "field\_". It will use these to carry out the search when the page is loaded, so it can display the WebApp items which match.

To see how the filter works, start by manually adding parameters to the URL in your browser. Remember the example Custom Field ID and keyword is unlikely to be found in your unique WebApp, so choose something you know is there! You should see your WebApp's results adjust as only items which match are returned.

**Example 1**

`https://my-website.staging.oregon.platform-os.com/webapp-list?webapp_field_1_1=my%20search%20terms`

**Example 2**

`https://my-website.staging.oregon.platform-os.com/webapp-list?webapp_field_1_2=option1,option2&webapp_field_1_2_match_type=OR`

### Step 6 - Build a form to allow Users to enter a search query

You can now build an input form to pass the user's chosen keywords as parameters to the URL.
