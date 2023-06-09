# Introduction

Site Search is an include you can add to your Pages to enable users to search Pages, WebApp items, and Module items for terms they're looking for. By default, this will now search slugs, metadata and Page content.

Site Search now has more configuration options to make searching your site more powerful.  This document will cover the new toolbox options for setting up a Site Search.

There are two parts of Site Search which you'll need to include in a Site:

*   Search Input

*   Search Results

Both are available in [Toolbox](https://help.siteglide.com/article/100-pages-getting-started) and it is up to you whether you put them on the same Page or different Pages.

# Including the Search Input

```html
{% include 'site_search_input'
   search_placeholder: 'Search'
   result_page_url: 'search-results'
-%}
```

## Parameters

*   `search_placeholder` - default is search - Placeholder value that displays in the input field.

*   `result_page_url` - This lets you define the relative URL of the Page where the Search Results are included. This can be the current Page URL. (default: 'search-results')

*   `search_input_class`- class on input field

*   `input_id` - id on input field (default: 'site\_search\_field')

*   `button_id` - id of the button you want to control submission (default: 'site\_search\_submit')&#x20;

## Using Multiple Site Search Forms on the Same Page

If you're using a button to submit your Input Form and there are multiple Input Forms within the same Page there are a couple of attributes you'll need to ensure are added.

You'll need to add the `button_id` parameter to the include for Search Input and this must be unique for each Search Form:

```html
{% include 'site_search_input'
   search_placeholder: 'Search'
   result_page_url: 'search-results'
   button_id: 'id_1' 
-%}
```

Then add an ID to the button that submits your input, please match this to the ID within the `button_id` parameter, for example:`<button class="btn site_search_submit" id="id_1">Submit</button>`

# Including the Search Results

```html
{% include 'site_search_results'
   layout: 'default'
   per_page: '20' 
-%}
```

## Parameters

*   `per_page` - default is 20 - defines the number of items outputted on the page

*   `layout` - default is default - defines the layout file used to display the results

*   `{{_all_results | size}}` can be used in the wrapper layout, and this will return the number of total results.&#x20;

# More Parameters - Search by Type

When selecting "Site Search Results" from the toolbox, you have the option of selecting which type of content will be contained within the results.  Here you can mix and match whether you would like to display results from Pages, WebApp Detail Pages or Module Detail Pages.  For example if you only want to search for Pages on the website then you could have the results exclude any data from WebApps and Modules.

To get results from WebApps or Modules, you must turn on Detail Pages in their configuration in Admin.

![](https://downloads.intercomcdn.com/i/o/163878328/498f53d9d4af441aac212718/Screen+Shot+2019-11-18+at+10.14.51.png)

# WebApps

If you select WebApps as a Type, you then get a further configuration option to select which WebApps to search.  The WebApps dropdown will display all of the available WebApps, this allows you to either select one or multiple WebApps to show results from.  If you leave this field empty them the search will show results all WebApps on your Site.

# More Parameters - Allow WebApp Items Without Detail Pages

Sometimes you may want to show results from WebApps without detail Pages- perhaps the relevant information is shown in a table instead? 

You can add the parameter:  `allow_list_items: 'true'` and WebApp items without Detail Pages will also show in the results.

We strongly recommend that if you use this parameter, you also update your Site Search Results Layout so that it hides links to the Detail Page if one does not exist. You can use the following Liquid if statement to achieve this:

```html
{% if this.detail_view == 'true' %}
   <a href="{{this.full_slug}}">Details</a>
{% endif %}
```

# Custom Results Layouts

By default, results will appear in a list. You can change the way they display with a custom Layout.

## Layout Files

Site Search Module layouts are stored in the following folder structure, which you can view via Code Editor: `layouts/modules/site_search/`

Within this module folder you will find the following layout folders:

*   `results/` - the results layout folder
    *   `design_system/` - default design system layouts folder 
        *   `item.liquid` - items displayed within the results wrapper  

        *   `wrapper.liquid` - wrapper of the list displayed using the results

To create a custom layout, right click on the results folder and write a folder, followed by the two required files (item & wrapper).&#x20;

For example, type: `custom_layout_1/wrapper.liquid` to create a folder called "custom\_layout\_1" that contains a file called "wrapper". Right click on your "custom\_layout\_1" folder to create the final item.liquid file.

## Handling Liquid Output

**Pages, WebApp Items and Module Items may all output different Liquid.** This is because they are different sorts of database Objects.

If your search covers more than one type, you may wish to only use output fields which are available to all those types, or you could use if statements to show one field or the other depending on which is available. 

For example, if you have a Search Results Layout and you want to display the SEO Meta Title for Pages and WebApps, you can use logic to show whichever one is actually available:

```html
{% if this.metadata.title %}
  <p>{{this.metadata.title}}</p>
{% elsif this.properties.meta_title %}
  <p>{{this.properties.meta_title}}</p>
{% endif %}
```

You can also use the default filter:  
`<p>{{this.metadata.title | default: this.properties.meta_title }}</p>`

## Page Results - Liquid Reference

The following output is available for Pages.

*   `{{this.id}}`  - ID of the Page

*   `{{this.name}}` - Page Name from Admin

*   `{{this.slug}}`  - Unique section of relative URL marked by forward slashes

*   `{{this.redirect_to}}` - Siteglide-CLI only 

*   `{{this.full_slug}}`   - URL

*   `{{this.content}}`  - Page content- this will include Liquid in its un-rendered state- rendering Liquid from Search Results is blocked to securely avoid injection attacks. This field is most likely to be used only in a filtered form, or as part of a Logical operation

*   `{{this.metadata.id}}`  

*   `{{this.metadata.name}} ` 

*   `{{this.metadata.enabled}}`

*   `{{this.metadata.file_type}}` - In most cases- this will show as Page

*   `{{this.metadata.last_edit}}` 

*   `{{this.metadata.meta_desc}}`

*   `{{this.metadata.meta_title}}`

## WebApp Results - Liquid Reference

This will depend on the WebApp. [Use Liquid Dot Notation](https://developers.siteglide.com/tutorial) to see the results for your WebApps. Here is an example of a typical WebApp.

*   `{{this.id}}` - ID of the WebApp Item

*   `{{this.name}}` - Name of WebApp Item

*   `{{this.model}}` - Shows that this is a WebApp Item and the ID of the WebApp

*   `{{this.full_slug}}` - URL for WebApp Detail Page

*   `{{this.properties.name}}`

*   `{{this.properties.slug}}` - The WebApp Item's Unique URL Slug- without the preceding URL slug which precedes all detail Pages for this WebApp. 

*   `{{this.properties.enabled}}`

*   `{{this.properties.release_date}}`

*   `{{this.properties.expiry_date}}`

*   `{{this.properties.og_type}}`

*   `{{this.properties.og_title}}`

*   `{{this.properties.meta_desc}}`

*   `{{this.properties.meta_title}}`

*   `{{this.properties.weighting}}`

*   `{{this.properties.twitter_type}}`

*   `{{this.properties.category_array}}`- Array of IDs for categories assigned to this Item

*   `{{this.properties.webapp_field_1_1}}` - Custom Fields where the first number is the ID of the WebApp and the Second number the ID of the Field. The IDs are integers given to WebApps and Fields in the order they are created- you can work this out by looking at the list of Fields in the WebApp's Admin View.

## Module Results - Liquid Reference

This will depend on the Module. [Use Liquid Dot Notation](https://developers.siteglide.com/tutorial) to see the results for your Modules. Here is an example of a typical Module.

*   `{{this.id}}` -ID of the Module Item

*   `{{this.name}}` - Name of Module Item

*   `{{this.full_slug}}` - URL for Module Detail Page

*   `{{this.model}}` - Shows that this is a Module Item and the ID of the Module

*   `{{this.properties.name}}`

*   `{{this.properties.slug}}` - The Module Item's Unique URL Slug- without the preceding URL slug which precedes all detail Pages for this Module. 

*   `{{this.properties.enabled}}`

*   `{{this.properties.release_date}}`

*   `{{this.properties.expiry_date}}`

*   `{{this.properties.og_type}}`

*   `{{this.properties.og_title}}`

*   `{{this.properties.meta_desc}}`

*   `{{this.properties.meta_title}}`

*   `{{this.properties.weighting}}`

*   `{{this.properties.category_array}}`- Array of IDs for categories assigned to this Item

*   `{{this.properties.twitter_type}}` - SEO Twitter Type

*   `{{this.properties.module_field_1_1}}` - Custom Fields where the first number is the ID of the Module and the Second number the ID of the Field. The Module IDs are fixed for all Sites, for example, the Blog Module always has the ID of 3.

# Outputting the Search Keyword

You can output the value of any URL parameter using platformOS's `context.params` object, including the search term in the "keyword" parameter: `<p>Search results for: {{context.params.keyword}}</p>`

platformOS [automatically sanitize](https://documentation.platformos.com/api-reference/liquid/sanitization) tag output to escape any malicious input using the  Cross Site Scripting technique.&#x20;

# Related Documents

*   [Searching - Keyword](https://developers.siteglide.com/searching-keyword)

*   [Searching - Advanced Filtering](https://developers.siteglide.com/searching-advanced-filtering)

