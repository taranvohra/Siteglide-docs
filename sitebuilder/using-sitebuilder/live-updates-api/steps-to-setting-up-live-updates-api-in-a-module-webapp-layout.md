# 📋 Steps to Setting Up Live Updates API in a Module/WebApp Layout

{% hint style="info" %}
The quickest way to get started with the SiteBuilder Live Updates API is to install a SiteBuilder layout which already uses it. Look out for the teal 'Live-updates ready' tag on the layouts, install and modify at will.
{% endhint %}

## 1) Installing the Module and including the JavaScript <a href="#id-1-installing-the-module-and-including-the-javascript" id="id-1-installing-the-module-and-including-the-javascript"></a>

Firstly, make sure the SiteBuilder Module is installed on your site. Then, include the JavaScript via CDN in the Page. We recommend you use the Liquid in the example below; it helps to ensure that the JavaScript is only loaded once, even if used by multiple layouts, maintaining good performance.

```liquid
{% raw %}
{% if context.exports.sitebuilder.live_update_JS_loaded == blank %}
  <script async src="{{'modules/module_86/js/v1-2/sitegurus_live_update_javascript_api.js' | asset_url }}"></script>
  {% assign live_update_JS_loaded = true %}
  {% export live_update_JS_loaded, namespace: sitebuilder %}
{% endif %}
{% endraw %}



```

## 2) Defining a Layout which will live-update and automatically generating a public API key <a href="#id-2-defining-a-layout-which-will-liveupdate-and-automatically-generating-a-public-api-key" id="id-2-defining-a-layout-which-will-liveupdate-and-automatically-generating-a-public-api-key"></a>

Secondly, choose which section of code you'd like the API to be ready to live-update.

* This must be some Liquid code which can be rendered using a single Liquid \`

\` tag. E.g. \`\` or \`\`. \* The code must not rely on inheriting any variables from higher up in the Page because those variables will not be available on the API endpoint Page. If you need to pass in more variables, this must be done via URL Params and read via \`\{{context.params\}}\`.

At the top of this layout, in the wrapper file if it has one, you need to include the following Liquid. This generates a public\_key you need to use the API. See "Thinking about Security" for why we use this. If you're using a WebApp or Module tag and layout from Siteglide, these variables will be available automatically.

```liquid
{% raw %}
{% function public_key = "modules/module_86/front_end/functions/v1/live_update_params_encode", layout: layout, model: _model, collection: 'false', creator_id: nil %}
{% endraw %}



```

However, if you're using a Liquid tag which has a value other than `module` or `webapp`, you will need to manually feed in the model\_type parameter as well. For example, if you're using the tag: \`

\`, then your public key function should look like this:

```liquid
{% raw %}
{% function public_key = "modules/module_86/front_end/functions/v1/live_update_params_encode", layout: layout, model: _model, model_type: 'ecommerce/cart', collection: 'false' %}
{% endraw %}


```

You can also use the Live Updates API with a `content_section` or `code_snippet`. Note that these include types don't intrinsically react to changes in the URL e.g. setting a parameter like `page` would not be natively supported. This can however be a benefit if you intend to write custom code including GraphQl; you will have to write that server-side code yourself, but you can take advantage of the Live Updates JS and event-listeners to quickly implement filter functionality on the client-side.

To use Live Updates with a `content_section` or `code_snippet`, you need to add a `model_type` as above, selecting the one you intend to use. Then you also need to add an `include_id` to the ID of the snippet/ section:

```liquid
{% raw %}
{% function public_key = "modules/module_86/front_end/functions/v1/live_update_params_encode", model_type: 'code_snippet', include_id: '1' %}
{% endraw %}


```

See the `collection` and `creator_id` URL parameters for more details about setting `collection` to 'true' when generating the public key.

### 3) Initialising the JavaScript <a href="#id-3-initialising-the-javascript" id="id-3-initialising-the-javascript"></a>

Before you can use the API on a layout, you must let the JavaScript know that a particular layout needs to be prepared to connect to the Live Updates API. To do this we need to add a data-attribute containing the public key from earlier to a layout's main element. (See the API reference for an alternative method using the JavaScript new keyword.)

```liquid
{% raw %}
<section data-sg-live-update-key="{{public_key}}" class="bg-white dark:bg-gray-900">
  <!-- rest of layout markup goes here -->
</section>
{% endraw %}
```

The layout will now initialise once the JS has loaded. You can check it has initialised and access the instance by typing `window.sgLiveUpdateConfig` into your JavaScript console.

### 4) Setting up a form for user interaction <a href="#id-4-setting-up-a-form-for-user-interaction" id="id-4-setting-up-a-form-for-user-interaction"></a>

At this point in our guide, your code should look something like this:

```liquid
{% raw %}
{% if context.exports.sitebuilder.live_update_JS_loaded == blank %}
  <script async src="{{'modules/module_86/js/v1-2/sitegurus_live_update_javascript_api.js' | asset_url }}"></script>
  {% assign live_update_JS_loaded = true %}
  {% export live_update_JS_loaded, namespace: sitebuilder %}
{% endif %}
{% function public_key = "modules/module_86/front_end/functions/v1/live_update_params_encode", layout: layout, model: _model, collection: 'false', creator_id: nil %}
{% endraw %}


<section data-sg-live-update-key="{{public_key}}" class="bg-white dark:bg-gray-900">
  <!-- rest of layout markup goes here -->
</section>
```

Next, a common feature of a layout with live updates is to add a form which the user can interact with to prompt some kind of change in what they are being displayed. For example, they may wish to sort, filter, change page or even edit the data they are seeing.

To add a form, we need another data-attribute. You can add as many forms as you need (if for example different controls need to be in different places in the layout).

```liquid
{% raw %}
<section data-sg-live-update-key="{{public_key}}" class="bg-white dark:bg-gray-900">
  <form data-sg-live-update-controls="search">

  </form>
  <form data-sg-live-update-controls="filters">

  </form>
  <!-- rest of layout markup goes here -->
</section>
{% endraw %}
```

The simplest way to add controls to your form is to use standard HTML form elements. The element's name should correspond to the URL parameter you wish the user to be able to change, while the value of the element obviously will set the parameter's value. Check the full example at the beginning along with the API Reference to see other kinds of supported controls and buttons:

* [Toggle Buttons](https://www.sitegurus.io/documentation/sitebuilder/live\_updates/API\_reference#live-updates-toggle-buttons)
* [Sort Buttons](https://www.sitegurus.io/documentation/sitebuilder/live\_updates/API\_reference#live-updates-sort-buttons)

Note ordinary HTML elements don't need any additional data-attributes. The API will watch for changes within the form area.

```liquid
{% raw %}
<section data-sg-live-update-key="{{public_key}}" class="bg-white dark:bg-gray-900">
  <form data-sg-live-update-controls="search">
    <input name="keyword" placeholder="Search">
  </form>
  <form data-sg-live-update-controls="filters">
{% for category in context.exports.categories.items %}
      <label>
        <input type="checkbox" name="category" value="{{category[0]}}">
        <span>{{category[1].name}}</span>
      </label>
    {% endfor %}
  </form>
</section>
{% endraw %}
```

## 5) Defining Components <a href="#id-5-defining-components" id="id-5-defining-components"></a>

As you make changes to the elments in the form, the Live Updates API will update the entire layout with a new Liquid re-render and replace it in the DOM.

Replacing the entire layout in the DOM may not be ideal however, as users interactions with the form will be interupred by the change.

The API allows you to specify one or more "components" which should update when the data changes. Once you setup a component, the HTML in between components will no longer change.

Let's add the important Siteglide tag \`

\`, which fetches our results, inside a new area marked as a component:

```liquid
{% raw %}
<section data-sg-live-update-key="{{public_key}}" class="bg-white dark:bg-gray-900">
  <form data-sg-live-update-controls="search">
    <input name="keyword" placeholder="Search">
  </form>
  <form data-sg-live-update-controls="filters">
    {% for category in context.exports.categories.items %}
      <label>
        <input type="checkbox" name="category" value="{{category[0]}}">
        <span>{{category[1].name}}</span>
      </label>
    {% endfor %}
  </form>
  <div data-sg-live-update-component="results">
    {%- include 'modules/siteglide_system/get/get_items', item_layout: 'item' -%}
  </div>
</section>
{% endraw %}
```

Now the results will update when we the user types in the search box, but their entries so far will not be lost as the form is not inside the component.

It's required to give the component a unique value in its data-attribute so the API can match up the component in the DOM with the component in the re-rendered document.

That's the basics of the Live Update API.

Learn more:

* Check out the [API Reference Guide](https://www.sitegurus.io/documentation/sitebuilder/live\_updates/API\_reference) each time you want to look something up.
* How to add sort buttons
* How to add custom toggle buttons
* How to set up pagination
* How to use a method to change advanced settings
