# 👀 Live Updates Reference

### HTML data-attribute markup <a href="#html-dataattribute-markup" id="html-dataattribute-markup"></a>

HTML data-attributes are a convenient way to configure the Live Update API JavaScript. We recommend using these in most use-cases. Unlike some JavaScript Libraries, it is possible to use data-attributes along with JavaScript methods without any known conflicts.

<table data-full-width="true"><thead><tr><th>Attribute</th><th>Role</th><th>Required</th><th>Example</th></tr></thead><tbody><tr><td><code>data-sg-live-update-section</code></td><td>Allows you to pass a uniq reference to the Object which will allow you to access it later in the <code>window.sgLiveUpdateConfig</code> object (when ready - see Events).</td><td>Optional</td><td><code>&#x3C;section data-sg-live-update-section="uniq">&#x3C;/section></code></td></tr><tr><td><code>data-sg-live-update-key</code></td><td>Passes the public_key to the API. You need to build the public key first using the function tag above. No other data-attributes will function without this one.</td><td>Required</td><td><code>&#x3C;section data-sg-live-update-key="{{public_key}}">&#x3C;/section></code></td></tr><tr><td><code>data-sg-live-update-component</code></td><td>Marks this element as a live-updateable element. If at least one of these are set, the default behaviour changes from live-updating the whole layout, to only live-updating the passed components. The data-attribute in the current and live-updated DOM code must match for this to work.</td><td>Optional</td><td><code>&#x3C;div data-sg-live-update-component="willChange1">&#x3C;/div></code></td></tr><tr><td><code>data-sg-live-update-controls</code></td><td>This marks this part of the HTML as an interactive area which should have default event listeners added.</td><td>Optional</td><td><code>&#x3C;form data-sg-live-update-controls="willChange1">&#x3C;input type="text" name="foo" value="bar"></code></td></tr><tr><td><code>data-sg-live-update-control-group</code></td><td>When adding a custom toggle button, this attribute's value should be the name of a group of buttons. Using the special "page" group means the button is reset to Page 1 when other changes in state occur.</td><td>Optional</td><td><code>&#x3C;div data-sg-live-update-control-params="?range_gte={{month.start}}&#x26;range_lt={{month.end}}&#x26;range_type=month" data-sg-live-update-control-group="month">&#x3C;/div></code></td></tr><tr><td><code>data-sg-live-update-listeners-attached</code></td><td>This is added automatically when using data-attributes to indicate that event listeners have already been added to the component. It can be used to tell the API not to add any more automatic event listeners to this element. In normal use, you do not need to set it.</td><td>optional</td><td></td></tr><tr><td><code>data-sg-live-update-modify-history-enabled="true"</code></td><td>Turns on modifyHistory behaviour, updating the URL parameters without refreshing the page when live-update form elements are modified by the user.</td><td>optional</td><td><code>&#x3C;section data-sg-live-update-section="uniq" data-sg-live-update-modify-history-enabled="true">&#x3C;/section></code></td></tr><tr><td><code>data-sg-live-update-modify-history-include-hidden-fields="true"</code></td><td>When modifyHistory behaviour is turned on, if false, hidden live-update fields will not be included in URL history updates.</td><td>optional</td><td><code>&#x3C;section data-sg-live-update-section="uniq" data-sg-live-update-modify-history-enabled="true" data-sg-live-update-modify-history-include-hidden-fields="false">&#x3C;/section></code></td></tr><tr><td><code>data-sg-live-update-default-param</code></td><td>This attribute should be given to an HTML form element within a <code>data-sg-live-update-controls</code> element. As usual, the element must also have a name to define which parameter it will set. This element will now set a defaultParams property instead of directly setting a parameter. This is useful because you can use the new default elements to set a default then use ordinary elements to override that default when the user makes a change. In the example here, the default parameter will be "1" until the checkbox is checked, when the parameter will be set to "2". If the checkbox is unchecked, the parameter will return to "1" instead of being removed.</td><td>optional</td><td><pre class="language-html"><code class="lang-html">&#x3C;form sg-live-update-controls="defaults">
  &#x3C;input type="hidden" data-sg-live-update-default-param name="category" value="1">
  &#x3C;input type="checkbox" name="category" value="2">
&#x3C;/form>
</code></pre></td></tr></tbody></table>

### GET URL Parameters <a href="#get-url-parameters" id="get-url-parameters"></a>

The Live Updates API, at its core, sends requests to the server to fetch a new version of the HTML content. Therefore, this section shows you which parameters can be sent in this request to modify how the Liquid will be rendered in the next response.

Before reading this section, it will help to be familiar with the Siteglide documentation relating to the kind of Liquid tag you are intending to live-update- here are a few useful links, but you may need to browse further to find the feature you're working with:

* [WebApp List Layouts Parameters](/webapps/layouts/webapp-list-layout.md)
* [Parameters for Filtering](/webapps/layouts/searching-advanced-filtering.md)
* [Parameters for Search](/webapps/layouts/searching-by-keyword.md)
* [Blog Archive](/modules/core-modules/blog-and-authors/blog-filter-by-date.md)

On the endpoint page we provide, the Liquid tag being live-updated is output.

In order to make the process of dynamically modifying the output simpler, we are basing the parameters for modifying it 99% on existing Siteglide functionality. We will update this module after new Siteglide functionality is released. We do have a few custom parameters with an `sg` prefix which can be used to modify module behaviour.

\*\*While in Siteglide some parameters must be set via Liquid e.g. `item_ids`:

```liquid
{% raw %}
{% include 'webapp', id: '1', layout: 'default', item_ids: '1,2' %}
{% endraw %}




```

...and others via URL e.g. `page`:

```liquid
<!-- URL: /webapp_1?page=2 -->
{% raw %}
{% include 'webapp', id: '1', layout: 'default' %}
{% endraw %}

```

...when using the Live Updates API, you can set any parameter via our URL parameters alone, giving you direct and consistent control.

<table data-full-width="true"><thead><tr><th>parameter</th><th>notes</th></tr></thead><tbody><tr><td><code>item_ids</code></td><td>If using data-attributes, we'll automatically send these in comma-seperated format.</td></tr><tr><td><code>category_ids</code></td><td>If using data-attributes, we'll automatically send these in comma-seperated format.</td></tr><tr><td><code>show_all_sub_items</code></td><td></td></tr><tr><td><code>per_page</code></td><td></td></tr><tr><td><code>show_pagination</code></td><td></td></tr><tr><td><code>ignore_pagination</code></td><td></td></tr><tr><td><code>sort_type</code></td><td></td></tr><tr><td><code>sort_order</code></td><td></td></tr><tr><td><code>type</code></td><td></td></tr><tr><td><code>pagination_layout</code></td><td></td></tr><tr><td><code>datasource</code></td><td></td></tr><tr><td><code>datasource_fields_by_name</code></td><td></td></tr><tr><td><code>datasource_fields_by_id</code></td><td></td></tr><tr><td><code>collection</code></td><td>This parameter will only work if <code>collection: 'true'</code> is also set on the public_key generating Liquid function tag; this is to prevent malicious users from being allowed to access raw data by default, without the layer of the server defining what they should and should not access. Note however that if you do allow this, the data will be viewable in the browser, so it must not be sensitive. If set to 'true' instead of returning HTML, we'll return the raw data from the collection. The data will be available in the details of the <code>live_update_end</code> custom event on the initiated element and in the parameters of the <code>onAfterLiveUpdate</code> callback function. The DOM will not be directly modified.</td></tr><tr><td><code>creator_id</code></td><td>If your users have permission to access webapp/ module items they did not personally create on the Front End, you can use this parameter dynamically as normal to filter. However, if you are using this parameter to prevent users from accessing items which do not belong to them and do not wish them to be able to change this in client-side code, you can make this a sensitive parameter by adding the same parameter to the <code>live_update_params_encode</code> function. If set against the function, the parameter can't be overridden.</td></tr><tr><td><code>page</code></td><td></td></tr><tr><td><code>use_default_properties</code></td><td></td></tr><tr><td><code>range_field</code></td><td>Coming soon in 4.8.2</td></tr><tr><td><code>range_lt</code></td><td></td></tr><tr><td><code>range_lte</code></td><td></td></tr><tr><td><code>range_gt</code></td><td></td></tr><tr><td><code>range_gte</code></td><td></td></tr><tr><td><code>use_location_search</code></td><td>Unlike <code>use_search</code> and <code>use_adv_search</code>, this is not set to <code>'true'</code> by default and must be set by the developer.</td></tr><tr><td><code>longlat</code></td><td></td></tr><tr><td><code>distance</code></td><td></td></tr><tr><td><code>marketplace</code></td><td>Required if this is a layout for a module downloaded from the Siteglide marketplace.</td></tr><tr><td><code>cache</code></td><td>Using this as a default parameter could significantly boost performance, but test carefully as the feature is presently in beta.</td></tr></tbody></table>

If you need to use a URL parameter which is missing from the table above:

* If Siteglide recognises it as a URL parameter which can modify results, you should be able to use it safely.
* If Siteglide requires the parameter to be added as a Liquid parameter to the main tag, please ask Sitegurus and we'll add support for it, if possible.

_Live Updates Custom Parameters_

The following parameters modify the behaviour of the API endpoint page:

<table data-full-width="true"><thead><tr><th>parameter</th><th>notes</th></tr></thead><tbody><tr><td><code>sg_skip_siteglide_constants</code></td><td>Some layouts don't require the Siteglide constants tag to be rendered. You can optionally use this to skip it and improve server response time. Especiually useful if the site has a lot of categories but your layout doesn't use them.</td></tr></tbody></table>

### Interactive Form Areas and Controls <a href="#interactive-form-areas-and-controls" id="interactive-form-areas-and-controls"></a>

In the last section, we detailed the URL Parameters which the API uses to request data. This next section will detail how you can set these paramters and allow the user to interact with the HTML to change these parameters.

#### Form Areas <a href="#form-areas" id="form-areas"></a>

By interactive form areas, we mean any area of the layout which contains filters, sorting controls, pagination controls or buttons designed to change the state of the layout, causing it to live-update in some way. It will most likely have a `<form>` tag in the DOM for semantic reasons, but this is not strictly necessary.

The `data-sg-live-update-controls` attribute marks an element as an interactive form area and the JavaScript will search the area for Form elements and custom buttons to which it can attach event listeners.

#### Using HTML Form Elements <a href="#using-html-form-elements" id="using-html-form-elements"></a>

Any HTML Form elements with a name attribute (including hidden inputs) inside this element will automatically have event listeners added to them watching for "keyup" or "change" events which will trigger a live-update with new parameters based on the name and values all HTML form elements inside.

For example, the following markup can be used to add the parameters `&per_page=20` to the request URL, changing that parameter in the endpoint Liquid tag and live-updating the content with the parameter applied. The name attribute provides the parameter key and the value property provides the value:

```liquid
<form sg-live-update-controls="results_per_page">
  <select name="per_page">
    <option value="10">10</option>
    <option value="20">20</option>
    <option value="50">50</option>
  </select>
</form>

```

Using the data-attributes and our automatic event listeners allows the user to modify multiple parameters at the same time. If you have filters for both category and colour, when the category filter changes, it will trigger a live-update of the content, but both the current values of the category and the colour inputs will be included in the request. Once the color filter is changed, it will in turn also include the category filter's current value in the request.

Keyup events, targeting fields in which the user will type, will be [debounced](https://css-tricks.com/debouncing-throttling-explained-examples/) so that keyup events don't cause disorientating changes too often. After the user pauses in typing, the live-update will take the latest values and trigger the live-update. Other events are set to update immediately.

#### Using Hidden HTML Form Elements <a href="#using-hidden-html-form-elements" id="using-hidden-html-form-elements"></a>

HTML Form Elements with the `type="hidden"` attribute will behave the same as other HTML Form Elements for the purposes of controlling the GET Parameters the API will use in its requests.

One common use-case for these is to use as "default" settings that will be needed in every request, despite any choices made by the user.

#### Live Updates Toggle Buttons <a href="#live-updates-toggle-buttons" id="live-updates-toggle-buttons"></a>

_Markup_

```liquid
<button data-sg-live-update-control-params="/blog?range_gte={{month.start}}&range_lt={{month.end}}&range_type=month" data-sg-live-update-control-group="month">{{month.start | date: "%b" }}</button>

```

_What Problems do our custom toggle buttons solve?_

Often in Siteglide, modules will have a single button which triggers JavaScript which will need to change multiple parameters in the URL at once, for example the archive buttons on the Blog and Events Lists needs to change both the `range_lt` and `range_gte` parameters.

* An ordinary form control in HTML can have only one name, so is not suitable changing multiple parameters at once without some other supporting JavaScript.
* Radio buttons cannot be unchecked easily by the user. It is useful to be able to clear filters.

To provide a consistent, convenient solution to both these problems, we're including custom toggle buttons in our documented markup:

Markup rules:

* They must use the `<button>` semantic element.
* They must have a `data-sg-live-update-control-params` data-attribute. This stores an absolute or relative URL, or just the search parameters of a URL starting with a `?`. When the button is pressed, the query parameters from the passed URL will be added to the request, along with parameters sourced from other form controls.
* Optionally they can have a `data-sg-live-update-control-group` data-attribute. This allows them to act as radio buttons within that group, with only one pressed at a time, however, with the important difference that it is possible to uncheck all of them. If you do not provide this attribute, the buttons will be considered to be in a group with all ungrouped buttons.

When a custom toggle button is pressed, we'll automatically add the data-attribute `aria-pressed="true"` to make the toggle button match accessibility guidelines. When unpressed, we will set `aria-pressed` to false. For sighted users, we strongly recommend adding CSS to make buttons with `aria-pressed="true"` look visually as if they are toggled, for example by changing colour. e.g. in CSS:

```css
[aria-pressed=true] {
  outline-style: solid;
  outline-width: 1px;
  outline-color: #22d3ee;
}
```

At the time of writing, the newest version of Tailwind supports the variant `aria-pressed:`.

If using Flowbite, you can place a toggle component inside your button and modify it to use `group-aria-pressed:`; it can then show the toggled state of the parent button very clearly, using CSS only.

```liquid
<button type="button" class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800 group" aria-pressed="true">
  <span class="mr-2">{{month.start | date: "%B" }}</span>
  <div class="relative inline-flex items-center cursor-pointer">
    <div class="w-11 h-6 bg-gray-200 group-focus:outline-none group-focus:ring-4 group-focus:ring-blue-300 dark:group-focus:ring-blue-800 rounded-full dark:bg-gray-700 group-aria-pressed:after:translate-x-full group-aria-pressed:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all dark:border-gray-600 group-aria-pressed:bg-blue-600"></div>
  </div>
</button>

```

The special group `data-sg-live-update-control-group="page"` behaves uniquely, as the page will always reset to "1" when another change is made to the parameters elsewhere. For example, if you are currently on page 2, but a filter change means there is now only one result, staying on page 2 would mean the result was hidden- the special group behaviour avoids this problem. If there is no available page 1 button, all page buttons will be unpressed.

#### Live Updates Sort Buttons <a href="#live-updates-sort-buttons" id="live-updates-sort-buttons"></a>

Controls to handle the sorting of module or webapp data require a slightly different approach. Such buttons commonly have three different states- unpressed, sort ascending and sort descending.

We've therefore provided specific markup for a sort button.

```liquid
<div>
  Weighting
  <button data-sg-live-update-sort-order="unsorted" data-sg-live-update-sort-type="properties.weighting" type="button" class="ml-1">
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" class="w-5 h-5">
      <path fill-rule="evenodd" d="M2.24 6.8a.75.75 0 001.06-.04l1.95-2.1v8.59a.75.75 0 001.5 0V4.66l1.95 2.1a.75.75 0 101.1-1.02l-3.25-3.5a.75.75 0 00-1.1 0L2.2 5.74a.75.75 0 00.04 1.06zm8 6.4a.75.75 0 00-.04 1.06l3.25 3.5a.75.75 0 001.1 0l3.25-3.5a.75.75 0 10-1.1-1.02l-1.95 2.1V6.75a.75.75 0 00-1.5 0v8.59l-1.95-2.1a.75.75 0 00-1.06-.04z" clip-rule="evenodd" />
    </svg>
  </button>
</div>

```

Markup rules:

* They must use the `<button>` semantic element.
* It is strongly recommended that the button be a child of the semantic `<th>` element.
* Requires the `data-sg-live-update-sort-type` attribute to be set to the name of the field you wish to sort by. As you would on a Siteglide Liquid parameter of the same name, you need to prepend with `properties.` for any Siteglide field. platformOS core fields like id, external\_id, created\_at, updated\_at and deleted\_at do not require the properties prefix.

4. Requires the `data-sg-live-update-sort-order="unsorted"` attribute to be set. There are three available states: `'unsorted'`, `'asc'` and `'desc'`. You should set most sort controls to 'unsorted', but may set one to be sorted 'asc' or 'desc' by default. If you do sort a column 'asc' or 'desc' by default, you should add the correct [aria-sort](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-sort) attribute to the `<th>` ancestor element. For subsequent button interactions, our JavaScript will apply this `aria-sort` attribute for you.
5. In order to show changes of state in the buttons to sighted users, the buttons will change their innerHTML dynamically according to the sortHTML property of the initiated `SitegurusLiveUpdate` object. By default, the module will use a series of icons (with the default unsorted icon being used as a default state in the example below). There is no need to use icons; any HTML is valid. We'll explain how to change these defaults below the main example.

When a sort button changes state to either 'asc' or 'desc', all other sort buttons will be set to 'unsorted'. The main reason for this behaviour is that sorting by multiple parameters at once is not supported by Siteglide, although it is possible via graphQL.

_Changing default HTML for each button state_

See the [Methods section](#methods) for `.setSortHTML();` and the instructions for using methods with data-attributes.

#### Live-Updating the Interactive Form Areas <a href="#liveupdating-the-interactive-form-areas" id="liveupdating-the-interactive-form-areas"></a>

Sometimes it is very convenient to make components which control live-updating, live-update themselves. A pagination `<nav>` is an excellent example, because the server can live-update this with the correct number of page buttons based on the new content.

It is not such a good idea to do this with some other form elements, like `<input>` tags, because the user will lose focus while typing and lose their progress. However, custom JavaScript may allow you to mitigate both of these problems.

When live-updating controls, here are a few general principals to improve the experience when using the API.

* Wrap the element which you are using to indicate the live-updated area (`data-sg-live-update-component`) around the element you are using as a form (`data-sg-live-update-controls`).
* Make sure that the layout returns the form element no-matter what the logic, even if it is empty. Otherwise there will be an error in the console as the API tries to match up between the new content and the DOM. For example, a pagination component should return the main element even if there are no results and no pagination buttons are to be shown.
  * This means the component must also wrap the Siteglide tag \`

\` as this will not render if there is no more than one page of results. \* Make sure the user does not lose focus or the values of form elements they are in the middle of using.

***

#### Methods <a href="#methods" id="methods"></a>

The following guide shows how methods can be used:

* [Using Live Updates Methods](/sitebuilder/using-sitebuilder/live-updates-api/steps-to-use-live-updates-methods.md)

The table shows available methods:

<table data-full-width="true"><thead><tr><th>Method</th><th>Parameters</th><th>Notes</th></tr></thead><tbody><tr><td><code>instance.liveUpdate(params,onBeforeLiveUpdate,onAfterLiveUpdate,changeStateOptions)</code></td><td>1) <code>params</code> - Object - Pass in an object containing the key value pairs you'd like to be added to the GET request. 2) <code>onBeforeLiveUpdate</code> - Function - optional - callback function to run before update 3) <code>onAfterLiveUpdate</code> - Function - optional - Callback function to run after update. 4) See below for changeStateOptions</td><td>Params will override any default params, if they have the same key. The callback functions are especially suitable if you need any one-time side effects. If you need a callback function for every update, we recommend using events instead.</td></tr><tr><td><code>instance.setSuspenseHTML('&#x3C;div>loading&#x3C;/div>')</code></td><td>1) Pass in an HTML String.</td><td>We recommend using template literals. When live-updating begins, this HTML will be inserted into the area which is being live-updated. When the live-updating ends, the HTML will be replaced with the live-updated component HTML. This can also be set when using the constructor.</td></tr><tr><td><code>instance.setSuspenseCSSClassList('class1 class2')</code></td><td>1) ClassList space-separated</td><td>Sets CSS classes on each live-updating component and then removes them once the live-updating is complete. If no components are used, the classes are toggled on the main initiated element. As well as allowing you to change style directly, you can also use it to position suspense HTML within the container. This can also be set when using the constructor.</td></tr><tr><td><code>instance.setModifyHistory({enabled: true, includeHiddenFields: false})</code></td><td>1) Object</td><td>Pass in an object with an <code>enabled</code> boolean and <code>includehiddenFields</code> boolean. This changes the behaviour of each following liveUpdate so that it will update the URL query parameters without reloading the page. Useful for creating shareable links.</td></tr><tr><td><code>instance.setSortHTML({unsorted: '', asc: '', desc: ''})</code></td><td>1) object</td><td>Pass in an object containing an HTML string (recommend template literals) for each of the three button states.</td></tr><tr><td><code>deprecated instance.setDefaultParams(object)</code></td><td>1) object</td><td>Pass in an object containing the key: value pairs of parameters you wish to use as default params to fully replace existing defaultParams. Use of this is not encouraged. Use <code>mergeUpdateParams</code> instead.</td></tr><tr><td><code>instance.mergeDefaultParams(object)</code></td><td>1) object</td><td>Pass in an object containing the key: value pairs of parameters you wish to use as default params. This preserves any existing defaultParams, unless one of your properties matches them, in which case your property will be set.</td></tr><tr><td><code>instance.changeStateTrailingDebounce(event,resetPages = false,changeStateOptions)</code></td><td>1) Normally accepts an event, but when not applicable pass in <code>undefined</code>. 2) pass <code>true</code> if pages should reset to page 1 e.g. if items have been deleted or filtered and pagination has changed (or pass <code>false</code>) 3) See below for <code>changeStateOptions</code></td><td>This queues a debounced live update. If other events in a short period of time also queue an update, only the last will run. This function can be useful in a situation where a user-interaction changes the data in the database but does not alter any filters, and you wish to show the updated data e.g. as a callback function to a Siteglide eCommerce function.</td></tr></tbody></table>

Example of setSortHTML method:

```js
instance.setSortHTML({
  unsorted: `<bold>Sort ASC</bold>`,
  asc: `<bold>Sort DESC</bold>`,
  desc: `<bold>Sort ASC</bold>`
});
```

changeStateOptions

* onlyUpdateComponent allows you fine control over which components should re-render on this update.

Example of changeStateOptions:

```js
instance.changeStateTrailingDebounce(undefined,false,{
  onlyUpdateComponent: ['a','b']
})
```

```liquid
<div data-sg-live-update-component="a">
  //Will re-render this time
</div>
<div data-sg-live-update-component="b">
  //Will not re-render this time
</div>
```

***

#### Events <a href="#events" id="events"></a>

The module JavaScript defines and dispatches the following custom Events. You can watch for these using ordinary JavaScript event listeners. Alternatively, you can use the callback functions on initialisation to achieve the same goal, but note that the callback functions are more appropriate for one-off functions for a particular live-update, while the events below are useful for code which should run every time.

<table data-full-width="true"><thead><tr><th>Target Element</th><th>event type</th><th>detail</th><th>description</th></tr></thead><tbody><tr><td>document</td><td><code>"live_update_constructor_ready"</code></td><td></td><td>After this event, you can run code which uses the Object constructor.</td></tr><tr><td>document</td><td><code>"live_update_script_ready"</code></td><td></td><td>This event fires when the asynchronous module JavaScript is ready and any data-attributes have been read and event listeners set. After this event, you can run code which uses the Object constructor, or access the <code>window.sgLiveUpdatesConfig</code> global variable containing references to each initiated <code>SitegurusLiveUpdate</code> object.</td></tr><tr><td>The element you passed as a parameter when initiating the Object</td><td><code>"live_update_start"</code></td><td><em>instance</em>- the Object created for this element, <em>defaultParams</em>- the parameters you passed in as defaults when initiating, <em>passedParams</em> - the parameters you passed in for this live-update, <em>params</em> - the resulting params of the request</td><td>This event is dispatched when the live-update is about to begin</td></tr><tr><td>The element you passed as a parameter when initiating the Object</td><td><code>"live_update_end"</code></td><td><em>instance</em>- the Object created for this element, <em>defaultParams</em>- the parameters you passed in as defaults when initiating, <em>passedParams</em> - the parameters you passed in for this live-update, <em>params</em> - the resulting params of the request,The total_entries returned, or if you passed the <code>collection</code> parameter, the full data returned from the WebApp</td><td>This event is dispatched when the live-update is about to end</td></tr></tbody></table>

#### Liquid Includes and Functions <a href="#liquid-includes-and-functions" id="liquid-includes-and-functions"></a>

* See [Pagination Include](/sitebuilder/using-sitebuilder/sitebuilder-liquid-includes/pagination.md) for settings specific to live-update data-attributes.

#### Endpoint Logic Reference <a href="#endpoint-logic-reference" id="endpoint-logic-reference"></a>

_This Section is included to provide useful information to advanced users and assist with troubleshooting. It may not be relevant to all users._

After the GET Request is sent with all of your chosen parameters, the context in which the new re-render of the Liquid is output is modified in the following ways:

1. The Siteglide Constants Liquid tag is run, unless the special `sg_skip_siteglide_constants` URL parameter is passed in. You can optionally experiment with this to improve server response time if the content you use does not require it.
2. The tag is given the Siteglide `use_search` and `use_adv_search` parameters set to 'true' automatically. This means that any URL parameters described in this set of documents will be allowed to manipulate the filtering [Filtering](/webapps/layouts/searching-advanced-filtering.md) & [Searching](/webapps/layouts/searching-by-keyword.md).
3. The `{{context.params}}` variables relating to the URL of the endpoint page are overwritten with those of the referring Page. This is to prevent any discrepancies in Layouts using them. Note we do not currently overwrite the `{{context.location}}` or `{{context.headers}}` objects, though future versions of this API might add an option to do this if requested.
4. There is no way to dynamically change the `layout` or the module/webapp `id` parameter- these are ignored. See "Thinking about Security".
5. The following params `range_lt`, `range_lte`, `range_gt` and `range_gte` are inspected. If they contain a date format which includes a dash `-` we convert them to the Unix timestamp which Siteglide expects and context.params is overwritten to reflect the new format. This allows you to skip the step of converting them in JavaScript from the value of a standard HTML field.
6. If the layout is a webapp layout and the `type` param is not set to "detail", we will add the `use_wrapper: 'true'` parameter to the Liquid tag. This means we only support WebApp list layouts with wrappers, as this allows them to be output self-contained. If you need to migrate an existing WebApp Layout to use a wrapper, you can see the differences here: [WebApp List Layouts](/webapps/layouts/webapp-list-layout.md#nNjER)
7. Any custom parameters you wish to send over you can. These can of course be accessed in the logic of the layout itself under `{{context.params}}`.
8. The URL parameters in the table above are read and, if necessary, turned into variables which are passed directly into the Liquid tag as Siteglide parameters.

***

### Using the JavaScript Initialisation <a href="#using-the-javascript-initialisation" id="using-the-javascript-initialisation"></a>

#### Constructor Arguments <a href="#constructor-arguments" id="constructor-arguments"></a>

The following arguments can be passed into the options Object as key:value pairs when initiating the `new SitegurusLiveUpdate` constructor.

e.g.

```javascript
const instance = new SitegurusLiveUpdate({
  defaultParams: {per_page: '20'}
});
```

<table data-full-width="true"><thead><tr><th>parameter</th><th>required</th><th>type</th><th>example</th><th>notes</th></tr></thead><tbody><tr><td>element</td><td>required</td><td>element</td><td><code>document.querySelector('#elementID')</code></td><td>This needs to be the main DOM element that represents the outermost element rendered by your Siteglide Liquid tag. Note by default, the whole component will live-update, but you can change this by defining components within it.</td></tr><tr><td>public_key</td><td>required</td><td>String</td><td><code>'some_public_key'</code></td><td>See Initialising with the Object Constructor in JavaScript</td></tr><tr><td>liveUpdateComponents</td><td>optional</td><td>Array of elements</td><td><code>Array.from(sectionEl.querySelectorAll('[data-sg-live-update-component]'))</code></td><td>Use this to define which areas of your layout you wish to live-update. Any areas outside of these will not live-update and will maintain state and focus during a live-update. If you do not pass a value here, the whle initiated element will live-update instead.</td></tr><tr><td>defaultParams</td><td>optional</td><td>Object</td><td><code>{per_page: '2', pagination_layout: 'default', item_ids: ['1','2']}</code> translates to <code>?per_page=2&#x26;pagination_layout=default&#x26;item_ids=1,2</code></td><td>Any params passed in at a later stage via form controls (using data-attributes) or as parameters on the liveUpdate method will overwrite the defaultParams.</td></tr><tr><td>suspenseHTML</td><td>optional</td><td>HTML String</td><td><code>'&#x3C;div>Loading...&#x3C;/div>'</code></td><td>This HTML replace components' InnerHTML during a live-update. The component element itself remains in the DOM at this point. After live-update, the new content will replace the component so the HTML will not persist after that point.</td></tr><tr><td>suspenseCSSClassList</td><td>optional</td><td>Space-separated list of classes</td><td><code>'class1 class2'</code></td><td>These classes will be added to the component element during a live-update. After live-update, the new content will replace the component so the classes will not persist after that point.</td></tr><tr><td>autoEventListeners</td><td>optional</td><td>Boolean</td><td><code>true</code></td><td>Default is false. You can set this to true to use the functionality of the data-attribute method while actually initiating with the programatic method.</td></tr><tr><td>sortHTML</td><td>optional</td><td>object</td><td><code>{unsorted: '&#x3C;span>&#x3C;/span>', asc: '&#x3C;span>&#x3C;/span>', desc: '&#x3C;span>&#x3C;/span>'}</code></td><td>See the <code>.setSortHTML()</code> method for details. Default value contains an SVG icon for each state.</td></tr></tbody></table>
