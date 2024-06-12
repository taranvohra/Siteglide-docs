The Article will show you how to adapt your Liquid Syntax and Blog Layouts to allow the User to Search for Posts by Keyword

# 🔹 Introduction

You can also allow the User to search for Blog Posts by keyword. This requires a slightly different Liquid parameter from the other navigation methods, but you can use both parameters if you choose.

# Liquid Syntax

Although all other Blog Navigation options require you to set the `use_adv_search: 'true'` Liquid parameter, keyword search requires the `use_search: 'true'` parameter.&#x20;

```liquid
{% raw %}
{%- include 'module'
    id: '3'
    layout: 'design_system/1'
    per_page: 20
    use_search: 'true' 
-%}
{% endraw %}
```

If you wish to use both types of Navigation for your Blog, you can set both types of search parameter to 'true'.

```liquid
{% raw %}
{%- include 'module'
    id: '3'
    layout: 'design_system/1'
    per_page: 20
    use_search: 'true'
    use_adv_search: 'true' 
-%}
{% endraw %}
```

# HTML and JavaScript Syntax

This code can be included in one of your Blog Navigation Layouts. Keyword Search will be activated if you've set the Liquid parameter above and the JavaScript below sets the keyword parameter in the URL.

```liquid
{% raw %}
<div class="row no-gutters">
  <div class="col-12">
    <h2>Search Posts by Keyword</h2>
    <form title="Search posts by Date" id="blog-archive-search">
      <div class="form-group">
        <label for="blogSearch">Add Search Keyword</label>
        <input id="blogSearch" type="text">
      </div>
      <input value="Search" class="btn btn-primary" type="submit" data-slug="/module-12" 
      onclick="blogs_search()">
    </form>
  </div>
</div>
{% comment %}This example function will search for posts in the future with this keyword. You'll need to use the "use_search" and "use_adv_search" parameters in your Liquid tag.{% endcomment %}
<script>
  function blogs_search() {
    event.preventDefault();
    var keyword = document.querySelector("#blogSearch").value;
    var url_string = window.location.pathname+"?keyword="+keyword;
    location.assign(url_string);
  }
</script>
{% endraw %}
```

