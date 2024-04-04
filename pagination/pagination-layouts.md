---
description: >-
  You can now fully customise your Pagination controls, by building a Pagination
  Layout. Change Page with style.
---

# Custom Pagination Layouts

## Introduction

Pagination is a catch-all term for the website User's ability to navigate through "pages" of results. It's available on all List Views including WebApps, Modules and Categories.

### Custom Pagination Layouts are now available on most Features

You can now also change the HTML structure of the Pagination controls with custom Layouts on most Siteglide Features. Unfortunately, custom Pagination Layouts are not yet available on Site Search Results, as the results contain items from several features, making Pagination more complicated to implement.

Furthermore, we provide you with Liquid variables detailing for example:

* The number of available pages
* The number of items per page
* Whether a previous or next page exists

This can help you build more advanced designs which adapt dynamically depending on the data available. Examples of Pagination Layouts will soon become available on the Layout Library.

## Developing a Pagination Layout

### Introduction to Pagination Layouts

Developing a Pagination Layout can start simple, but many designs will involve complex elements.  We'd recommend checking out our Design System examples when they become available on Layout Library. You could alter these, or use them for inspiration and start from scratch.&#x20;

### How to Change Page

In order to make a Pagination control button functional, you need to refresh the current Page with a modified URL query parameter.&#x20;

For example, if I'm on the "About" Page of my site, the URL will be: `/about`, by default, this will show page 1.

If I want to send the User to Page 11, you'll need to add a page query parameter on the URL so that it looks like this: `/about?page=11`

You can do this with HTML, using the \<a> tag: `<a href="/about?page=11">11</a>`&#x20;

Or, you can use JavaScript to achieve the same effect.&#x20;

This will change page for all Pagination controls on the Page, so currently it's best practice to only display one WebApp/ Module List  with Pagination on the Page.

#### Liquid Variables

Within Pagination Layouts, the following variables will be available to give you contextual information.&#x20;

* `current_page`  -The current page (integer) &#x20;
* `previous_page` - Designed to be used with a Prev button, its value is the previous page number (integer), or false (Boolean) if there is no previous page.
* `prev_path` -  href for previous button
* `next_page` - Designed to be used with a Next button, its value is the next page number (integer), or false (Boolean) if there is no next page.
* `next_path` - href for next button
* `first_path`: href for first button
* `last_path`: href for last button
* `total_pages`: The total number of pages (integer)
* `page_search_params`: The preserved search terms in URL format- starts with & so can be added at the end of URL to new Page (`?page=x` will already be added at the end of a URL, so a prevailing & is appropriate).&#x20;

For example, you might have a button which will take Users to the next Page, but it might be helpful to know whether or not a next page exists (otherwise, the User will see an error when they navigate). Using these variables and a Liquid if statement, you can disable the button when the user is on page 1. In this example, we also use a variable from the above list to set the button's `href`.

```liquid
<li class="page-item <div data-gb-custom-block data-tag="if" data-0='false' data-1='false' data-2='false'>disabled</div>">
 <a class="page-link" href="{{next_path}}">Next</a>
</li>
```

#### Looping

In order to give developers full flexibility, we've exposed the For Loop in Pagination Layouts. The reason for this is that you may not want to show all Pagination buttons at once, but instead only show a limited range of buttons.

If you're not familiar with Liquid For Loops, the following platformOS documentation might be helpful:

* [Loops](https://documentation.platformos.com/api-reference/liquid/loops)
* [Objects](https://documentation.platformos.com/api-reference/liquid/objects) - Many of these objects give helpful information within the context of a loop iteration.
