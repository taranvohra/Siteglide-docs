# 🔹 Get Table Config

### Example <a href="#example" id="example"></a>

```liquid
{% raw %}
{% function table_config = "modules/module_86/front_end/functions/v1/get_table_config", model: _model, id: id, field_headings: field_headings %}
{% endraw %}
```

### Purpose <a href="#purpose" id="purpose"></a>

This function fetches the configuration file which Siteglide uses to store metadata about the WebApp or Module. By outputting the returned Object `{{table_config}}` you can explore the JSON tree and find out information about the WebApp dynamically.

SiteBuilder Layouts might for example use this to output the name of the WebApp in a Layout, or to loop over custom fields to output the field names as labels alongside the values.

The function carries out a GraphQL call behind the scenes, so for performance reasons, we recommend only including this function if you need it. It may be more appropriate, when you know the data should not change often, to hardcode these values in the Layout instead. Following this, you are also welcome to replace this function where you see it in an installed layout, with a more straightforward hardcoded solution.

However, if you have a situation where the WebApp configuration is likely to change often and you want the layout to automatically change often to reflect that, this function can be very useful.
