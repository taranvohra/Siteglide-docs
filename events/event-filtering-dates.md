
This option allows you to provide the User with links to months when Events are happening - or let them Search between any two dates.

![](https://downloads.intercomcdn.com/i/o/203114561/8fa65fd9be84c2ac669c0020/image.png)

# Prerequisites

*   You've installed the Events Module

*   You've updated your System Files to at least version 2.4.4.0

# Introduction

This article will show:

*   How to add a parameter to the main Events Module "include" Liquid Tag to enable advanced filtering by `Event Start` and `Event End` dates.

*   How to include the Archive Navigation Feature

*   An explanation of the three main sub-Layouts available in in the Default Layout: (1) Search Between Two Dates (2) Browse By Months (3) Browse by Months under Year Header.

*   How to give User Feedback about Search Results

# Add "use\_adv\_search" parameter to include for Event List View

The "use\_adv\_search" parameter is needed to allow filtering from the URL to apply to your Event Items, this can be added to the include for Event List like so:

```html
{%- include 'module'
    id: '12'
    layout: 'default'
    per_page: '20'
    show_pagination: 'true'
    sort_type: 'created_at'
    sort_order: 'desc'
    use_adv_search: 'true' 
-%}
```

# Past Events and Future Events

![](https://downloads.intercomcdn.com/i/o/203096167/dac797858dbe8ef904390967/image.png)

By default, the List View will show all Events that are enabled, released and not yet expired.&#x20;

If you just want to filter the List so it either shows Events that have already happened in the Past- or those Events which will happen in the Future, it may not be necessary to include the entire Archive Feature. 

## Filter by Past Events

![](https://downloads.intercomcdn.com/i/o/203096602/7b027cbd23e44d9032958ec0/image.png)

```html
{% assign now = "now" | date: "%s" %}
<a href="{{context.headers.PATH_INFO}}?range_field=events&range_type=future&range_gt={{now}}">Future Events</a>
```

## Filter by Future Events

![](https://downloads.intercomcdn.com/i/o/203096442/877bf46b3b86c72c84d360df/image.png)

```html
{% assign now = "now" | date: "%s" %}
<a href="{{context.headers.PATH_INFO}}?range_field=events&range_type=past&range_lt={{now}}">Past Events</a>
```

## Using Liquid Logic to "Toggle" between Past and Future Events

```html
{% assign now = "now" | date: "%s" %}
{% if context.params.range_type == "past" %}
  <h2>Past Events</h2>
  <a href="{{context.headers.PATH_INFO}}?range_field=events&range_type=future&range_gt={{now}}">Future Events</a>
{% elsif context.params.range_type == "future" %}
  <h2>Future Events</h2>
  <a href="{{context.headers.PATH_INFO}}?range_field=events&range_type=past&range_lt={{now}}">Past Events</a>
{% else %}
  <h2>All Events</h2>
  <a href="{{context.headers.PATH_INFO}}?range_field=events&range_type=past&range_lt={{now}}">Past Events</a>
{% endif %}
```

# Including the Archive Navigation Feature

Firstly, you will need to provide the following Liquid to include your Archive layout:

```html
{%- include 'modules/siteglide_events/get/get_events_archive'
    archive_layout: "design_system/1/archive"
    archive_layout_type: "sidebar_years_and_date_search" 
-%}
```

## Parameters

*   `archive_layout`-The layout parameter refers to the main layout folder followed by a path to the folder storing any archive layouts you are using. In the example, an `/archive` folder is used.

*   `archive_layout_type`- The type parameter refers to the name of the Archive Layout file. 

In the `default/archive/` folder we have 3 different optional types of Archive Layout you can choose by entering their names in the `type` parameter. We will show the liquid tag for including each.

***Include: Browse By Months***

```html
{%- include 'modules/siteglide_events/get/get_events_archive'
    archive_layout: "design_system/1/archive"
    archive_layout_type: "sidebar" 
-%}
```

***Include: Browse By Months Under Years Header***

```html
{%- include 'modules/siteglide_events/get/get_events_archive'
    archive_layout: "design_system/1/archive"
    archive_layout_type: "sidebar_years"
-%}
```

***Include: Search Events Between Two Dates***

```html
{%- include 'modules/siteglide_events/get/get_events_archive'
    archive_layout: "design_system/1/archive"
    archive_layout_type: "sidebar_years_and_date_search" 
-%}
```

# Events Archive Layouts

The following examples will take you through the different options:

## Browse by Month

![](https://downloads.intercomcdn.com/i/o/203097728/66141d6f7f41130389f473fc/image.png)

```html
<h2>Archive</h2>
<ul>
  {% for month in events_archive_months %}
    <li>
      <a href="{{context.headers.PATH_INFO}}?range_gt={{month.start}}&range_lte={{month.end}}&range_type=month&range_field=events">
        {{month.start | date: "%b-%y" }}
      </a>
    </li>
  {% endfor %}
</ul>
```

In this example, we use the `events_archive_months` object and loop over the array. For each iteration, a URL link is outputted which has three range parameters:

*   `` `range_gte` `` = An epoch format date for midnight on the beginning of the first day of the selected month

*   `range_lt` = The date above + 1 month. We don't use `lte` because the date is the first valid date in the next month- we want every date up until then.

*   `range_field` =events - This parameter is important as it makes sure that the `Event Start` and `Event End` fields are used instead of `Release Date` for the filtering.

## Browse by Months, organised into Years

![](https://downloads.intercomcdn.com/i/o/203098785/9d029c33b1e04b3305d93909/image.png)

This Layout does not just organise the Months available under the relevant Year Headers, it also will skip any Years without an Event.

```html
<h2>Archive by Years</h2>
<ul>
  {% for year in events_archive_years %}
    <li>{{year.start | date: "%Y"}}</li>
    <ul>
      {% assign months_by_year = events_archive_months | group_by: "year"  %}
      {% for month in months_by_year[year.start] %}
        <li>
          <a href="{{context.headers.PATH_INFO}}?range_gte={{month.start}}&range_lt={{month.end}}&range_type=month&range_field=events">
            {{month.start | date: "%b" }}
          </a>
        </li>
      {% endfor %}
    </ul>
  {% endfor %}
</ul>
```

&#x20;This example uses the same links as the previous one. However, it also organises the links into the years in which they belong by first looping over the years in the events\_archive\_years and then using the group\_by liquid filter and another loop to output the month links grouped under the current iteration's year. Learn more about this Liquid at the pOS docs:

*   [group\_by filter](https://documentation.platformos.com/api-reference/liquid/platformos-filters#group_by)

*   [for loop](https://documentation.platformos.com/api-reference/liquid/loops)

## Search Events between two dates

![](https://downloads.intercomcdn.com/i/o/203099049/74ee8f39c26894cc9782e4a2/image.png)

In the Default Layout, this Option also includes the Previous "Browse by Months Organised into Years" Option for convenience- though the code can be simply removed if you prefer. We have removed it in this article's example.

 It also adds a Form for directly manipulating the URL parameters to find the exact dates the User is interested in.

```html
<div class="row no-gutters">
  <div class="col-12">
    <h2>Archive by Years</h2>
    <ul>
      {% assign events_archive_years = events_archive_years | sort: "start" %}
      {% for year in events_archive_years %}
        <li>{{year.start | date: "%Y"}}</li>
        <ul>
          {% assign months_by_year = events_archive_months | sort: "start" | group_by: "year"  %}
          {% for month in months_by_year[year.start] %}
            <li>
              <a href="{{context.headers.PATH_INFO}}?range_gte={{month.start}}&range_lt={{month.end}}&range_type=month&range_field=events">
                {{month.start | date: "%b" }}
              </a>
            </li>
          {% endfor %}
        </ul>
      {% endfor %}
    </ul>
  </div>
</div>
{% assign now = "now" | date: "%s" %}
<div class="row no-gutters">
  <div class="col-12">
    <h2><a href="{{context.headers.PATH_INFO}}?range_field=events&range_lt={{now}}">All Past Events</a></h2>
  </div>
</div>
<div class="row no-gutters">
  <div class="col-12">
    <h2><a href="{{context.headers.PATH_INFO}}?range_field=events&range_gte={{now}}">All Future Events</a></h2>
  </div>
</div>
<div class="row no-gutters">
  <div class="col-12">
    <h2>Search by Date</h2>
    <form title="Search events by Date" id="events-archive-search">
      <div class="form-group">
        <label for="range_gt">Start Date</label>
        <input data-sg-events="start-date" id="range_gt" name="range_gt" type="date">
      </div>
      <div class="form-group">
        <label for="range_gt">End Date</label>
        <input data-sg-events="end-date" id="range_lte" name="range_lte" type="date">
      </div>
      <input value="Search" class="btn btn-primary" type="submit" data-slug="/module-12" 
      onclick="s_events_date_search(s_events_date_search_error)">
    </form>
  </div>
</div>
{% comment %}
Add your custom error message here- it can be renamed by changing its name in the argument for the s_events_date_search function and in the definition below.
{% endcomment %}
<script>
  function s_events_date_search_error() {
    alert("Please enter valid dates before searching.");
  }
</script>
```

In this example a form is used to take user input. The Siteglide function automatically adds the dates to the URL parameters in the correct format. You can rewrite the error function to customise the way the form handles invalid dates entered.

***A note about Date Entry Inputs on different Browsers
***Different Browsers may display the Date Input fields very differently. 3rd party Javascript Plugins are available for making sure these display with your desired Design. 

# Custom Layouts

This is a relatively complex feature, so some understanding of Liquid will be necessary to understand how to create a Custom Layout. The best way to start would be to copy one of the Default layouts and edit it to provide the changes you need.

Any Layouts included with the above Liquid will get access to the `events_archive_years `and `events_archive_months`arrays, which contain detailed data about the years and months respectively which contain valid Events. This can be used to generate dynamic buttons to the User so they can browse.

***events\_archive\_years***

```html
{% for year in events_archive_years %}
  {{year.start}} <!-- Outputs Epoch time at start of Year -->
  {{year.end}} <!-- Outputs Epoch time at end of Year -->
{% endfor %}
```

***events\_archive\_months***

```html
{% for year in events_archive_years %}
  {{year.start}} <!-- Outputs Epoch time at start of Year -->
  {{year.end}} <!-- Outputs Epoch time at end of Year -->
{% endfor %}
```

In order to filter the Events List by date, you need to refresh the Page URL with parameters in the [Unix Epoch time](https://www.unixtimestamp.com/index.php) format. 

The following URL Parameters will cause Results in the List to Filter:

*   `range_gt` - greater than 

*   `range_gte` - greater than or equal to 

*   `range_lt` - less than

*   `range_lte` - less than or equal to

For the above to work, remember to set the `use_adv_search: true` parameter (see start of article)! 

The pOS documentation website has some useful tips on how to use liquid to convert date formats and manipulate dates and times. See the following useful filters, and browse the docs for more:

*   [localize](https://documentation.platformos.com/api-reference/liquid/platformos-filters#localize-aliases-l)

*   [date](https://documentation.platformos.com/api-reference/liquid/platformos-filters#localize-aliases-l)

*   [add\_to\_time](https://documentation.platformos.com/api-reference/liquid/platformos-filters#add_to_time)

# Feedback for the User - Displaying the currently applied filter

![](https://downloads.intercomcdn.com/i/o/203114980/bde87f47b0da6f9f530dca49/image.png)

In the examples, you may notice another URL parameter is used: `range_type`. The `s_events_date_search` Siteglide function for filtering Events by user-inputted dates adds the parameter `range_type="between"`. This would allow the following liquid on the List Layout to identify that this search is between two dates:

```html

{% if context.params.range_type == "between" %}

  Events between {{context.params.range_gt | date: "%d-%b-%y"}}
  {{context.params.range_gte | date: "%d-%b-%y"}} 
  and 
  {{context.params.range_lt | date: "%d-%b-%y"}}
  {{context.params.range_lte | date: "%d-%b-%y"}}

{% endif %}
```

Whereas, you could use another `range_type` to indicate that different feedback should be given to the User. e.g. the parameter `month` in this example changes the sentence structure from "Events between" to "Events in" to communicate the different kind of filtering that is now taking place.

```html
{% if context.params.range_type == "month" %}

  Events in {{context.params.range_gt | date: "%b-%y"}}
  {{context.params.range_gte | date: "%b-%y"}}

{% endif %}
```

Note- in both of these examples- the `gte` and `gt`  dates are both outputted- this is because only one is expected to be available. The Layout is designed to accept either
