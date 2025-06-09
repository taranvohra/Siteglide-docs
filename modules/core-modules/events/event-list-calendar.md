# ℹ️ Calendar List View

## Prerequisites

* You've Installed the Events Module
* You've added Events in the Admin

## Introduction

The Calendar Layout is a List Layout which demonstrates how you can use the FullCalendar API to visualise Events from the Siteglide database. You can read more about the [open-source license](https://fullcalendar.io/license)

## Outputting the Calendar Layout on a Page

The Events Module Calendar Layout is an example of a List Layout. Like all List Layouts, you can output it in any Liquid File, including Pages, Templates and Layouts. However, it also requires JavaScript to function properly, so it will not be supported inside an Email e.g. Autoresponder or Workflow.

To output the Calendar, output the List Layout as normal, and choose a Calendar Layout in the layout parameter.

```liquid
{% raw %}
{%- include 'module', id: '12', layout: 'design_system/1/calendar', per_page: '5000', show_pagination: 'false' -%}
{% endraw %}
```

There are a few parameters which work particularly well on the Calendar Layout, because we will want to disable Pagination and show all enabled and released Events at once:

* per\_page: 5000 - Makes sure the first Page shows all Events that are enabled and released
* show\_pagination: 'false' - Hides Pagination Controls

You can use filtering Parameters as normal to filter Events and only show some on the Calendar.

* category\_ids - Add a comma-seperated string of Category IDs to display
* item\_ids - Add a comma-seperated string of Item IDs to display

There's no need to use the sorting parameters on the Calendar, as they will make no difference to the output- Events will always show in chronological order!

## Filtering the Calendar with Events Navigation Options

You can use some Events Navigation Options to further filter the Events which appear on the Calendar.

## How to Style

You can inspect on the Calendar in dev-tools to see which classes are used by the elements. You can then write CSS rules to style it.

You can also find pre-built themes at the FullCalendar Site: https://fullcalendar.io/docs/theming

### How to Style Categories

We've set up the calendar to apply classes to Events which represent any Siteglide Categories they are assigned to.

This means that you can use these classes when writing your CSS, if you want to style Events of different Categories with different colors for example. This will of course be simpler if you only assign each Event to a single Category, but by setting up the classes in this way, we aim to make this flexible for you to style the way you want.

## Customising the Calendar Layout- Advanced - Using the FullCalendar Docs

The Siteglide Events Module is powered by the FullCalendar plugin. We provide you with an example Layout, but you can use their docs to fully customise your calendar view: [fullcalendar](https://fullcalendar.io/)
