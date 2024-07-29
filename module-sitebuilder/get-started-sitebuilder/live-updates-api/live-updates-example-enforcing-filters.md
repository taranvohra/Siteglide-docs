# 🔹 Live Updates Example - Enforcing Filters

### Introduction and Use Cases <a href="#introduction-and-use-cases" id="introduction-and-use-cases"></a>

This example is useful if you want to use [Siteglide filters](https://developers.siteglide.com/search-and-filtering) on a WebApp or Module, but don't want to give your end-user the option of altering the filters by modifying the URL.

In this example, we set the filter as if we have a WebApp 1 with a custom field which can be filtered. We imagine there is a variable `{{any_variable}}` which might come from a datasource in a parent layout, or be hardcoded. These variables of webapp, field and filter value you can change depending on your use-case.

### Example <a href="#example" id="example"></a>

#### Liquid in the wrapper.liquid file <a href="#liquid-in-the-wrapperliquid-file" id="liquid-in-the-wrapperliquid-file"></a>

```liquid
{% raw %}
{% comment %} Get public key as normal {% endcomment %}
{% function public_key = "modules/module_86/front_end/functions/v1/live_update_params_encode", layout: layout, model: _model, collection: 'false', creator_id: nil %}
{% comment %} Generate unique ID for the layout, unless one has already been generated and sent in the params. The main purpose of doing this here is to help the JavaScript reliably reference the instance of the Live Update object created for this layout.{% endcomment %}
{% if params.sitebuilder_uniq_component_id %}
  {% assign sitebuilder_uniq_component_id = params.sitebuilder_uniq_component_id %}
{% else %}
  {% capture sitebuilder_uniq_component_id %}sitegurus_component_{% increment sitegurus_gen_uniq_component_id %}{% endcapture %}
{% endif %}
{% comment %} Output Layout Wrapper code. {% endcomment %}
<section id="{{sitebuilder_uniq_component_id}}_table" data-sg-live-update-section="{{sitebuilder_uniq_component_id}}">
  {% comment %} Logic which will refuse to display any items until the correct filter is applied. {% endcomment %}
  {% if params.webapp_field_1_1 != any_variable %}
    {%- include 'modules/siteglide_system/get/get_items', item_layout: 'item' -%}
  {% endif %}
</section>
{% comment %} Re-render the layout using the filter param as soon as possible {% endcomment %}
<script>
  document.addEventListener('live_update_script_ready', ready);
  function ready() {
    {% comment %} Add to params the Siteglide filter relating to the WebApp custom field, and the unique ID custom parameter. {% endcomment %}
{% endraw %}

    window.sgLiveUpdateConfig['{{sitebuilder_uniq_component_id}}'].liveUpdate({webapp_field_1_1: '{{any_variable}}', sitebuilder_uniq_component_id: '{{sitebuilder_uniq_component_id}}'});
  }
</script>
```

Drawing your attention to the important bit: items are not displayed until the correct parameters are present in the URL. Users can't simply change the URL and access different content in this case!

```
{% raw %}
{% if params.webapp_field_1_1 != any_variable %}
  {%- include 'modules/siteglide_system/get/get_items', item_layout: 'item' -%}
{% endif %}
{% endraw %}
```

#### Notes <a href="#notes" id="notes"></a>

* In this example, it's useful to have a reliable ID for the layout, no-matter how many are outputted on the page. We generate a unique ID if the layout is rendered front-end, but on the live-update re-render, we use the already generated ID that was sent in the params.
