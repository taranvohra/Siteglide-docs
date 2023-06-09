You can now fully customise your Pagination controls, by building a Pagination Layout. Change Page with style.

# Introduction

Pagination is a catch-all term for the website User's ability to navigate through "pages" of results.&#x20;
It's available on all List Views including WebApps, Modules and Categories.&#x20;

## Custom Pagination Layouts are now available on most Features

You can now also change the HTML structure of the Pagination controls with custom Layouts on most Siteglide Features. Unfortunately, custom Pagination Layouts are not yet available on Site Search Results, as the results contain items from several features, making Pagination more complicated to implement.&#x20;

Furthermore, we provide you with Liquid variables detailing for example:

*   The number of available pages

*   The number of items per page

*   Whether a previous or next page exists

This can help you build more advanced designs which adapt dynamically depending on the data available. Examples of Pagination Layouts will soon become available on the Layout Library.

# Outputting Pagination - A Recap

## Default Pagination

When you output a List Layout it will fetch results based on the parameters you've given it. 

The parameter `per_page` will decide how many items will initially display in the List. By default, this value will be 20.

 If more results were fetched than the `per_page` value,  Pagination controls will be added to allow the User to change page and view the rest of the data.

## How to remove Pagination Controls

Set the parameter  `show_pagination: 'false'` to remove pagination controls.

## How to move Pagination Controls

Firstly remove the default Pagination controls, as above. 
Secondly, add the following Liquid where you'd like the controls to sit within your HTML structure: `{%- include 'modules/siteglide_system/get/get_pagination' -%}`

# Specifying a Pagination Layout

## Choose Your Layout File

Layouts for Pagination should be stored in Code Editor at the following path: `layouts/pagination/my_pagination_layout_name.liquid`

## Add a Pagination Layout to a WebApp or Module "include" tag

```html
{%- include 'webapp'
    id: '3'
    layout: 'default'
    per_page: '20'
    sort_type: 'properties.name'
    sort_order: 'asc'
    pagination_layout: 'my_pagination_layout_name'
-%}
```

## Add a Pagination Layout to a Pagination "include" tag

```html
{%- include 'modules/siteglide_system/get/get_pagination'
    pagination_layout: 'my_pagination_layout_name' 
-%}
```

# Developing a Pagination Layout

## Introduction to Pagination Layouts

Developing a Pagination Layout can start simple, but many designs will involve complex elements. 
We'd recommend checking out our Design System examples when they become available on Layout Library. You could alter these, or use them for inspiration and start from scratch. 

## How to Change Page

In order to make a Pagination control button functional, you need to refresh the current Page with a modified URL query parameter. 

For example, if I'm on the "About" Page of my site, the URL will be: `/about`, by default, this will show page 1.

If I want to send the User to Page 11, you'll need to add a page query parameter on the URL so that it looks like this: `/about?page=11`

You can do this with HTML, using the \<a> tag: `<a href="/about?page=11">11</a> `

Or, you can use JavaScript to achieve the same effect. 

This will change page for all Pagination controls on the Page, so currently it's best practice to only display one WebApp/ Module List  with Pagination on the Page.&#x20;

### Liquid Variables

Within Pagination Layouts, the following variables will be available to give you contextual information. 

*   `current_page`  -The current page (integer)  

*   `previous_page` - Designed to be used with a Prev button, its value is the previous page number (integer), or false (Boolean) if there is no previous page.

*   `prev_path` -  href for previous button

*   `next_page` - Designed to be used with a Next button, its value is the next page number (integer), or false (Boolean) if there is no next page.

*   `next_path` - href for next button

*   `first_path`: href for first button

*   `last_path`: href for last button

*   `total_pages`: The total number of pages (integer)

*   `page_search_params`: The preserved search terms in URL format- starts with & so can be added at the end of URL to new Page (`?page=x` will already be added at the end of a URL, so a prevailing & is appropriate). 

For example, you might have a button which will take Users to the next Page, but it might be helpful to know whether or not a next page exists (otherwise, the User will see an error when they navigate). Using these variables and a Liquid if statement, you can disable the button when the user is on page 1. In this example, we also use a variable from the above list to set the button's `href`.

```html
<li class="page-item {% if next_page == false %}disabled{% endif %}">
 <a class="page-link" href="{{next_path}}">Next</a>
</li>
```

### Looping

In order to give developers full flexibility, we've exposed the For Loop in Pagination Layouts. The reason for this is that you may not want to show all Pagination buttons at once, but instead only show a limited range of buttons.

If you're not familiar with Liquid For Loops, the following platformOS documentation might be helpful:

*   [Loops](https://documentation.platformos.com/api-reference/liquid/loops)

*   [Objects](https://documentation.platformos.com/api-reference/liquid/objects) - Many of these objects give helpful information within the context of a loop iteration.

