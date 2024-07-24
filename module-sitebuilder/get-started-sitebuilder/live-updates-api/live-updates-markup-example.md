# 🔹 Live Updates Markup Example

### Pre-Requisites <a href="#prerequisites" id="prerequisites"></a>

* This guide assumes you have a basic familiarity with:
  * Building WebApp and Module Layouts on Siteglide using Liquid tags
  * HTML, including data-attributes

### Using a ready-made SiteBuilder Layout <a href="#using-a-readymade-sitebuilder-layout" id="using-a-readymade-sitebuilder-layout"></a>

{% hint style="info" %}
The quickest way to get started with the SiteBuilder Live Updates API is to install a SiteBuilder layout which already uses it. Look out for the teal 'Live-updates ready' tag on the layouts, install and modify at will.
{% endhint %}

Having said that, if you want to modify any other layout to start fetching live updates with the API, we'll show how to do that next.

### Basic Markup Example <a href="#basic-markup-example" id="basic-markup-example"></a>

The following markup example would work well in the `wrapper.liquid` file of a webapp or module layout. The `layout` and `_model` variables will then be inherited from the tag used to output the layout in the page.

```liquid
{% raw %}
{% comment %}Generate the public key as above and pass it to the main element of the HTML code as a data-attribite. Another data-attribute, data-sg-live-update-section, may optionally be used to supply a unique ID to the HTML section which will be referenced in the initialised Object.{% endcomment %}
{% if context.exports.sitebuilder.live_update_JS_loaded == blank %}
  <script async src="{{'modules/module_86/js/v1-2/sitegurus_live_update_javascript_api.js' | asset_url }}"></script>
  {% assign live_update_JS_loaded = true %}
  {% export live_update_JS_loaded, namespace: sitebuilder %}
{% endif %}
{% function public_key = "modules/module_86/front_end/functions/v1/live_update_params_encode", layout: layout, model: _model %}
<section data-sg-live-update-key="{{public_key}}" class="bg-white dark:bg-gray-900">
  <div data-sg-live-update-component="main_results">
    {% comment %} This HTML tag and its contents are marked with the data-attribute as a component which will live update. {% endcomment %}
    {%- include 'modules/siteglide_system/get/get_items', item_layout: 'item' -%}
  </div>
  <form data-sg-live-update-controls="sort_and_filters">
    {% comment %} 1) Hidden fields {% endcomment %}
    <input type="hidden" name="per_page" value="20">
    {% comment %} 2) Ordinary HTML Form Elements{% endcomment %}
    {% for category in context.exports.categories.items %}
      <label>
        <input type="checkbox" name="category" value="{{category[0]}}">
        <span>{{category[1].name}}</span>
      </label>
    {% endfor %}
    {% comment %} 3) Custom Toggle Buttons {% endcomment %}
    {% assign month_start = 1682895600 %}
    {% assign month_end = 1685574000 %}
    <button data-sg-live-update-control-params="/blog?range_gte={{month.start}}&range_lt={{month.end}}&range_type=month" data-sg-live-update-control-group="month">{{month.start | date: "%b" }}</button>
    {% comment %} 4) Sort buttons {% endcomment %}
    <div>
      Weighting
      <button data-sg-live-update-sort-order="unsorted" data-sg-live-update-sort-type="properties.weighting" type="button" class="ml-1">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" class="w-5 h-5">
          <path fill-rule="evenodd" d="M2.24 6.8a.75.75 0 001.06-.04l1.95-2.1v8.59a.75.75 0 001.5 0V4.66l1.95 2.1a.75.75 0 101.1-1.02l-3.25-3.5a.75.75 0 00-1.1 0L2.2 5.74a.75.75 0 00.04 1.06zm8 6.4a.75.75 0 00-.04 1.06l3.25 3.5a.75.75 0 001.1 0l3.25-3.5a.75.75 0 10-1.1-1.02l-1.95 2.1V6.75a.75.75 0 00-1.5 0v8.59l-1.95-2.1a.75.75 0 00-1.06-.04z" clip-rule="evenodd" />
        </svg>
      </button>
    </div>
  </form>
  {% comment %} Wrapping a component with aria-live alerts screen readers to changes in the number of results. {% endcomment %}
  <div aria-live="polite">
    <div data-sg-live-update-component="total_results">
      {% capture exports_key %}webapp_{{id}}{% endcapture %}
      {% assign per_page = per_page | default: context.params.per_page | default: 20 %}
      {% assign total_entries = context.exports[exports_key].data.result.total_entries %}
      {% assign total_pages = total_entries | plus: 0.0 | divided_by: per_page | ceil %}
      {% assign current_page = context.params.page | default: 1 %}
      <span class="text-sm font-normal text-gray-500 dark:text-gray-400">
        Showing Page
        <span class="font-semibold text-gray-900 dark:text-white">{{current_page}}</span>
        of
        <span class="font-semibold text-gray-900 dark:text-white">{{total_pages}}</span>
      </span>
    </div>
  </div>
  {% comment %} Our pre-built pagination solution when combined with a SiteBuilder pagination_layout which supports live-updates {% endcomment %}
  {% include "modules/module_86/front_end/includes/v1/pagination", live_updates: 'true', lock_per_page: 'false' %}
  {% comment %} A form example to allow users to change number of results per page {% endcomment %}
{% endraw %}
  <form class="flex flex-wrap space-x-2 space-y-2 items-center" data-sg-live-update-controls="per_page">
    <label for="rows" class="text-sm font-normal text-gray-500 dark:text-gray-400">
      Rows per page
    </label>
    <select name="per_page" id="rows" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-primary-500 focus:border-primary-500 block py-1.5 pl-3.5 pr-6 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-primary-500 dark:focus:border-primary-500">
      <option selected value="{{per_page}}">{{per_page}}</option>
      <option value="25">25</option>
      <option value="50">50</option>
      <option value="100">100</option>
    </select>
  </form>
</section>
```
