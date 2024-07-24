# 🔹 Detail Page Valid

### Example <a href="#example" id="example"></a>

```
{% raw %}
{%- function detail_page_valid = "modules/module_86/front_end/functions/v1/detail_page_valid", fc_data: fc_data, full_slug: this.full_slug -%}
{% endraw %}
```

### Purpose <a href="#purpose" id="purpose"></a>

This function aims to check two things:

1. Whether a WebApp has a Detail Layout enabled?
2. Whether a WebApp Layout has a \{{this.full\_slug\}} which fits an expected pattern.

In future, this function should also be able to provide these checks for Module Layouts too.

Currently, the function is experimental and works well as a straight-out-of-the-box solution for Layouts installed, but we do recommend you also carry out a manual check to make sure links to detial pages are working correctly.
