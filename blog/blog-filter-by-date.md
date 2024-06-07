# Blog Filter by Date

Browse by Month and/or Search Blog Posts Between Two Dates

## Introduction

This article will show:

* How to add a parameter to the main Blog Module "include" Liquid Tag to enable advanced filtering by "Release Date".
* How to include the Archive Navigation Feature
* An explanation of the three main sub-Layouts available in in the Default Layout: (1) Search Between Two Dates (2) Browse By Months (3) Browse by Months under Year Header.
* How to give User Feedback about Search Results

![](https://downloads.intercomcdn.com/i/o/167280567/d043e46b31966ad5bad10e5b/image.png)

## Adding the Advanced Search Parameter

The "Archive" Blog Navigation features all depend on the Advanced Search feature. In order to enable this dependency, you will need to add a parameter on the Page where you initially included a Blog Module: `use_adv_search: 'true'` Note- the word `true` must be in single quotes.

In the Starter Site example below, the Module is initially included on the Blog Page, so we will do it here. We also switch to the `default` layout as this contains the updated examples.

![](https://downloads.intercomcdn.com/i/o/167283252/7fa2434977ef1ed0458d412e/image.png)

### To Include the Archive Navigation Feature

Firstly, you will need to provide the following Liquid to include your Archive layout:

<pre class="language-liquid"><code class="lang-liquid"><strong>{%- include 'modules/siteglide_blog/get/get_blog_archive'
</strong>    archive_layout: "default/archive"
    archive_layout_type: "sidebar_years_and_date_search" 
-%}

</code></pre>

In the default layout, this Liquid would be placed inside the `sidebar/wrapper.liquid` file, but this is optional.

### Parameters

* `archive_layout`- The layout parameter refers to the main layout folder followed by a path to the folder storing any archive layouts you are using. In the example, an `/archive` folder is used.
* `archive_layout_type`  - The type parameter refers to the name of the Archive Layout file.&#x20;

In the `default/archive/` folder we have 3 different optional `types` of Archive Layout you can choose by entering their names in the type parameter. We will show the liquid tag for including each.

_**Include: Browse By Months**_

```liquid
{%- include 'modules/siteglide_blog/get/get_blog_archive'
    archive_layout: "default/archive"
    archive_layout_type: "sidebar" 
-%}

```

_**Include: Browse By Months Under Years Header**_

```liquid
{%- include 'modules/siteglide_blog/get/get_blog_archive'
    archive_layout: "default/archive"
    archive_layout_type: "sidebar_years" 
-%}

```

_**Include: Search Blog Between Two Dates**_

```liquid
{%- include 'modules/siteglide_blog/get/get_blog_archive'
    archive_layout: "default/archive"
    archive_layout_type: "sidebar_years_and_date_search" 
-%}

```

## Blog Archive Layouts

The following examples will take you through the different options:

### Browse by Month

![](https://downloads.intercomcdn.com/i/o/167292503/6661f116c2357242b71011b2/image.png)

```liquid
<h2>Archive</h2>
<ul>
  {% raw %}
{% for month in blog_archive_months %}
    <li><a href="{{context.location.pathname}}?range_gt={{month.start}}&range_lte={{month.end}}&range_type=month">
      {{month.start | date: "%b-%y" }}</a></li>
  {% endfor %}
{% endraw %}
</ul>

```

In this example, we use the `blog_archive_months` object and loop over the array. For each iteration, a link is outputted which has two range parameters:

* `range_gte=` An epoch format date for midnight on the beginning of the first day of the selected month
* `range_lt=` The date above + 1 month. We don't use `` `lte` `` because the date is the first valid date in the next month- we want every date up until then.

### Browse by Months, organised into Years

This Layout does not just organise the Months available under the relevant Year Headers, it also will skip any Years without a Blog Post.

![](https://downloads.intercomcdn.com/i/o/167292829/53d955e9099672368596ff35/image.png)

```liquid
<h2>Archive by Years</h2>
<ul>
  {% raw %}
{% for year in blog_archive_years %}
    <li>{{year.start | date: "%Y"}}</li>
    <ul>
      {% assign months_by_year = blog_archive_months | group_by: "year" %}
      {% for month in months_by_year[year.start] %}
        <li><a href="{{context.location.pathname}}?range_gte={{month.start}}&range_lt={{month.end}}&range_type=month">
          {{month.start | date: "%b" }}</a></li>
      {% endfor %}
    </ul>
  {% endfor %}
{% endraw %}
</ul>

```

This example uses the same links as the previous one. However, it also organises the links into the years in which they belong by first looping over the years in the `blog_archive_years` and then using the `group_by` liquid filter and another loop to output the month links grouped under the current iteration's year. Learn more about this Liquid at the pOS docs:

* [group\_by filter](https://documentation.platformos.com/api-reference/liquid/platformos-filters#group\_by)
* [for loop](https://documentation.platformos.com/api-reference/liquid/loops)

### Search Blog Posts between two dates

In the Default Layout, this Option also includes the Previous "Browse by Months Organised into Years" Option for convenience- though the code can be simply removed if you prefer. We have removed it in this article's example.

&#x20;It also adds a Form for directly manipulating the URL parameters to find the exact dates the User is interested in.

![](https://downloads.intercomcdn.com/i/o/167292152/0e2fa3b1d153bdda479dacb0/image.png)

```liquid
<h2>Search by Date</h2>
<form title="Search Blog by Date" id="blog-archive-search">
  <div class="form-group">
    <label for="range_gt">Start Date</label>
    <input data-sg-blog="start-date" id="range_gt" name="range_gt" type="date">
  </div>
  <div class="form-group">
    <label for="range_gt">End Date</label>
    <input data-sg-blog="end-date" id="range_lte" name="range_lte" type="date">
  </div>
  <div class="form-group">
    <input value="Search" class="btn btn-primary" type="submit" onclick="s_blog_date_search(s_blog_date_search_error)">
  </div>
</form>
{% raw %}
{% comment %}
Add your custom error message here - it can be renamed by changing its name in the argument for the s_blog_date_search function and in the definition below.
{% endcomment %}
{% endraw %}
<script>
  function s_blog_date_search_error() {
    alert("Please enter valid dates before searching.");
  }
</script>

```

In this example a form is used to take user input. The Siteglide function automatically adds the dates to the URL parameters in the correct format. You can rewrite the error function to customise the way the form handles invalid dates entered.

_**A note about Date Entry Inputs on different Browsers**_ Different Browsers may display the Date Input fields very differently. 3rd party Javascript Plugins are available for making sure these display with your desired Design.&#x20;

### Custom Layouts

This is a relatively complex feature, so some understanding of Liquid will be necessary to understand how to create a Custom Layout. The best way to start would be to copy one of the Default layouts and edit it to provide the changes you need.

Any Layouts included with the above Liquid will get access to the `blog_archive_years`and `blog_archive_months`arrays, which contain detailed data about the years and months respectively which contain valid Blog Posts. This can be used to generate dynamic buttons to the User so they can browse.

_**blog\_archive\_years**_

```liquid
{% raw %}
{% for year in blog_archive_years %}
  {{year.start}} <!-- Outputs Epoch time at start of Year -->
  {{year.end}} <!-- Outputs Epoch time at end of Year -->
{% endfor %}
{% endraw %}

```

_**blog\_archive\_months**_

```liquid
{% raw %}
{% for month in blog_archive_months %}
  {{month.start}} <!-- Outputs Epoch time at start of Month -->
  {{month.end}} <!-- Outputs Epoch time at end of Month -->
  {{month.year}} <!-- Outputs Epoch time for the beginning of the Year in which this month falls. -->
{% endfor %}
{% endraw %}

```

In order to filter the Blog list by date, you need to refresh the Page URL with parameters in the [Unix Epoch time](https://www.unixtimestamp.com/index.php) format.&#x20;

The following URL Parameters will cause Results in the List to Filter and more than one can be added:

* `range_gt` - greater than - this will filter for Blog posts after the given date.
* `range_gte` - greater than or equal to - this will filter for Blog posts on and after the given date.
* `range_lt` - less than - this will filter for Blog posts before the given date.
* `range_lte` - less than or equal to - this will filter for Blog posts on and before the given date.

&#x20;For the above to work, remember to set the `use_adv_search: true` parameter (see start of article)!

The pOS documentation website has some useful tips on how to use liquid to convert date formats and manipulate dates and times. See the following useful filters, and browse the docs for more:

* [localize](https://documentation.platformos.com/api-reference/liquid/platformos-filters#localize-aliases-l)
* [date](https://documentation.platformos.com/api-reference/liquid/platformos-filters#localize-aliases-l)
* [add\_to\_time](https://documentation.platformos.com/api-reference/liquid/platformos-filters#add\_to\_time)

### Feedback for the User

![](https://downloads.intercomcdn.com/i/o/167295402/abe1734641ef2604993dbc7b/image.png)

In the examples, you may notice another URL parameter is used: `range_type`. The `s_blog_date_search` Siteglide function for filtering blog posts by user-inputted dates adds the parameter `range_type="between"`. This would allow the following liquid on the List Layout to identify that this search is between two dates:

```liquid
{% raw %}
{% if context.params.range_type == "between" %}
  Posts between {{context.params.range_gt | date: "%d-%b-%y"}}
  {{context.params.range_gte | date: "%d-%b-%y"}} 
  and 
  {{context.params.range_lt | date: "%d-%b-%y"}}
  {{context.params.range_lte | date: "%d-%b-%y"}}
{% endif %}
{% endraw %}

```

Whereas, you could use another `range_type` to indicate that different feedback should be given to the User. e.g. the parameter `month` in this example changes the sentence structure from "posts between" to "posts from" to communicate the different kind of filtering that is now taking place.

```liquid
{% raw %}
{% if context.params.range_type == "month" %}
  Posts from {{context.params.range_gt | date: "%b-%y"}}
  {{context.params.range_gte | date: "%b-%y"}}
{% endif %}
{% endraw %}
```

Note - in both of these examples- the `gte` and `gt`  dates are both outputted- this is because only one is expected to be available. The Layout is designed to accept either.
