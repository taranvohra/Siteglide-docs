# ℹ️ Getting Started with Event Filtering & Searching

The Events Module List View can be filtered by Category, Host, or by finding Events which are happening between given dates.

![](https://downloads.intercomcdn.com/i/o/203092694/4319734f3d1f785dfcf1cf0e/image.png)

## Introduction

The Events Module includes the following optional features for helping Users navigate the List View.

* Browse by Category
* Browse by Host (requires Authors Module)
* Browse by Month/Date - Finds Events which are happening during this month
* Search Events which are happening between two Dates

You may be familiar with many of these if you've used the [Blog Module Navigation](https://developers.siteglide.com/blog), however the main difference between them is how they handle dates; navigating the Blog Module by date would use the post's `Release Date`, whereas the Events Module will check to see if a given date falls between the `Event Start` and `Event End` dates.

## Using the Navigation Options to Filter the Map and Calendar Views

![](https://downloads.intercomcdn.com/i/o/203094035/263a4b74debb30ba8b902ed5/image.png)

You can use the Navigation Options on the Map and Calendar Layouts- these are List Layouts too!

However, certain features just won't have the same effect. For example, filtering the Calendar Layout by Date does not make sense- as the Calendar controls already give you an option to navigate by Date- using the Archive Navigation on the Calendar would cause certain Events to be "missing" from the Calendar, even if the User had navigated to a different month. On the other hand, it's perfectly possible that you might wish to filter the Calendar by Host or Category- to allow the User to focus on the type of Events which interest them most.

## Using two List Views on the Same Page- and only filtering one of them

As the Events Navigation options are powered by URL parameters, the parameters will filter all Events List Views on the Page the same way.

If you want to provide a Calendar and an Events List together on the Page for example, and you only wish one of them to be affected by the filters in the URL, you can do so by only using the `use_adv_search: 'true'` parameter on the List View you want to be filtered.

## User Feedback

Each Events Navigation Article will explain how you can use Liquid Logic to dynamically show the currently applied filter. Here, we'll show an example of some Logic that will check for any of the applied filters:

```liquid
{% raw %}
{% assign now = "now" | date: "%s" %}
{% if context.params.range_type == "past" %}
  <h2>Past Events</h2>
  <a href="{{context.headers.PATH_INFO}}?range_field=events&range_type=future&range_gt={{now}}">
    Future Events</a>
{% elsif context.params.range_type == "future" %}
  <h2>Future Events</h2>
  <a href="{{context.headers.PATH_INFO}}?range_field=events&range_type=past&range_lt={{now}}">
    Past Events</a>
{% elsif context.params.module_field_12_4 %}
  <h2>Events hosted by {{context.params.host_name | url_decode}}</h2>
{% elsif context.params.range_type == "month" %}
  <h2>Events in {{context.params.range_gt | date: "%b-%y"}}
    {{context.params.range_gte | date: "%b-%y"}}</h2>
{% elsif context.params.range_type == "between" %}
  <h2>Events between {{context.params.range_gt | date: "%d-%b-%y"}}
    {{context.params.range_gte | date: "%d-%b-%y"}} and 
    {{context.params.range_lt | date: "%d-%b-%y"}}
    {{context.params.range_lte | date: "%d-%b-%y"}}</h2>
{% elsif context.params.category %}
  <h2>Category: {{context.exports.categories.data[context.params.category].name}}</h2>
{% else %}
  <h2>All Events</h2>
  <a href="{{context.headers.PATH_INFO}}?range_field=events&range_type=past&range_lt={{now}}">
    Past Events</a>
{% endif %}
{% endraw %}
```

Of course, you can use this for inspiration and edit as you wish.

## Related Documents

* [Searching - Keyword](https://developers.siteglide.com/searching-keyword)
* [Searching - Advanced Filtering](https://developers.siteglide.com/searching-advanced-filtering)
