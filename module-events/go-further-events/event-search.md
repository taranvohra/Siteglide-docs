# ℹ️ Search

The Article will show you how to adapt your Liquid Syntax and Events Layouts to allow the User to Search for Events by Keyword

## Introduction

You can also allow the User to search for Events by keyword. This requires a slightly different Liquid parameter from the other navigation methods, but you can use both parameters if you choose.

## Liquid Syntax

Although all other Events Navigation options require you to set the `use_adv_search: 'true'` Liquid parameter, keyword search requires the `use_search` parameter.

```liquid
{% raw %}
{%- include 'module'
    id: '12'
    layout: 'design_system/1'
    per_page: 20
    show_pagination: 'false'
    use_search: 'true' 
-%}

{% endraw %}
```

If you wish to use both types of Navigation for your Events, you can set both types of search parameter to 'true'.

```liquid
{% raw %}
{%- include 'module'
    id: '12'
    layout: 'design_system/1'
    per_page: 20
    show_pagination: 'false'
    use_search: 'true'
    use_adv_search: 'true' 
-%}

{% endraw %}
```

## HTML and JavaScript Syntax

This code can be included in one of your Events Navigation Layouts. Keyword Search will be activated if you've set the Liquid parameter above and the JavaScript below sets the keyword parameter in the URL.

```liquid
{% raw %}
<div class="row no-gutters">
  <div class="col-12">
    <h2>Search Events by Keyword</h2>
    <form title="Search events by Keyword" id="events-archive-search">
      <div class="form-group">
        <label for="eventsSearch">Add Search Keyword</label>
        <input id="eventsSearch" type="text">
      </div>
      <input
        value="Search" 
        class="btn btn-primary" 
        type="submit" 
        data-slug="/module-12" 
        onclick="events_search()"
      />
    </form>
  </div>
</div>

{% raw %}
{% comment %}
This example function will search for events in the future with this keyword. 
You'll need to use the "use_search" and "use_adv_search" parameters in your Liquid tag.
{% endcomment %}
{% endraw %}
<script>
  function events_search() {
    event.preventDefault();
    var keyword = document.querySelector("#eventsSearch").value;
    var url_string = window.location.pathname+"?keyword="+keyword;
    location.assign(url_string);
  }
</script>
{% endraw %}
```

## Searching and Filtering at the Same Time

The following example also filters for future Events at the same time as it searches for keywords. You need to have set both `use_search` and `use_adv_search` parameters in the Liquid (see Syntax section above). You can adjust the JavaScript to remove this, or switch it to fetch Events in the Past.

```javascript
<script>
  function events_search() {
    event.preventDefault();
    var keyword = document.querySelector("#eventsSearch").value;
    var url_string = window.location.pathname+"?keyword="+keyword+"&range_lt={{now}}
    &range_type=past&range_field=events";
    location.assign(url_string);
  }
</script>
```
