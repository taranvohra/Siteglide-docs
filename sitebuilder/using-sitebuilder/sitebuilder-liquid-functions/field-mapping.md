# ℹ️ Field Mapping

### Example <a href="#example" id="example"></a>

```
{% raw %}
{%- function field_map = "modules/module_86/front_end/functions/v1/field_mapping", field_headings: field_headings, this: this -%}
{% endraw %}



```

### Purpose <a href="#purpose" id="purpose"></a>

This function is an important part of how WebApp Layouts can automatically adapt to handle different sources of data.

It takes in a headings object which stores field IDs as keys next to the names of available field slots as values. It then returns a new object using the values in `this` which stores the data values against those field slots so that the layout can output the data.

### Adjusting the Mapping <a href="#adjusting-the-mapping" id="adjusting-the-mapping"></a>

If you add a new field to the WebApp after creating the layout with SiteBuilder, you can safely access that value via the `this` object as you normally would in a layout.

However, if you wish, you can also modify the existing headings in the JSON object.

Starting with this Object...

```
{% raw %}
{% parse_json field_headings %}
{
"Title": "name"
}
{% endparse_json %}
{% endraw %}



```

You could change it so that existing `{{field_map['Title']}}` outputs would output values from a different field like so:

```
{% raw %}
{% parse_json field_headings %}
{
"Title": "webapp_field_1_1"
}
{% endparse_json %}
{% endraw %}



```

Or you can add a brand new slot to the WebApp `{{field_map['Extra Slot']}}` and populate it with a new field's data:

```
{% raw %}
{% parse_json field_headings %}
{
"Title": "name"
"Extra Slot": "webapp_field_1_2"
}
{% endparse_json %}
{% endraw %}
```

As the field\_headings are passed into the function, the function will return an object where the required data values are stored against the correct keys.
