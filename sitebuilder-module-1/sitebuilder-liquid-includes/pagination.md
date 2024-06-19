# 🔹 Pagination

### The Pagination Include <a href="#the-pagination-include" id="the-pagination-include"></a>

This include was designed to keep SiteBuilder layouts tidy by abstracting common pagination logic out of layouts.

It can be used to determine where in the layout the pagination layout should be displayed. Just move the tag to where you need it.

The include is an alternative to the documented Siteglide feature [How to Move Pagination](https://developers.siteglide.com/pagination-layouts#VgKjd); it just adds a few extra SiteBuilder features.

_Important_ The include will only output pagination if the main Liquid tag has the parameters `use_pagination: 'true'` and `pagination_layout` set. Otherwise, it will do nothing.

#### Example <a href="#example" id="example"></a>

```liquid
<section class="p-8">
  <!-- Main Layout here -->
  <!-- Use the below Liquid tag to choose where your pagination will be outputted -->
  
{% raw %}
{% include "modules\module_86\private\views\partials\front_end\includes\v1\pagination", live_updates: 'false', lock_per_page: 'true' %}
{% endraw %}

</section>
```

#### parameters <a href="#parameters" id="parameters"></a>

| Parameter       | Type                      | Required                    | Notes                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| --------------- | ------------------------- | --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `live_updates`  | Boolean 'true' or 'false' | optional                    | This is to be used alongside the [live\_updates](https://www.sitegurus.io/documentation/sitebuilder/live\_updates/introduction) feature. Setting to true will add data-attributes needed to wrap the layout in elements which have both the data-sg-live-update-controls and data-sg-live-update-component attributes. It will also include a hidden field to set `per_page` as a default parameter to that inherited from the main tag, as well as hidden fields for defaults for `show_pagination` and `pagination_layout`. |
| `lock_per_page` | Boolean 'true' or 'false' | optional, default is 'true' | This is to be used alongside the [live\_updates](https://www.sitegurus.io/documentation/sitebuilder/live\_updates/introduction) feature and the `live_updates` parameter above. Set this to 'false' if you have another control to set `per_page`, else, set to 'false' to automatically set per\_page to the same value inherited from the module tag.                                                                                                                                                                       |

### Versions <a href="#versions" id="versions"></a>

#### V1 - original release <a href="#v1-original-release" id="v1-original-release"></a>

The original logic inside the function is as follows. You can use this to make a copy and modify if you wish in your own layouts.

```liquid
{% raw %}
{% if live_updates == 'true' %}
  <div data-sg-live-update-component="pagination">
    <div data-sg-live-update-controls="pagination">
      {% if lock_per_page == 'true' or lock_per_page == blank %}<input type="hidden" name="per_page" value="{{per_page}}">{% endif %}
      <input type="hidden" name="show_pagination" value="{{show_pagination}}">
      <input type="hidden" name="pagination_layout" value="{{pagination_layout}}">
      {%- if _show_pagination == 'false' and pagination_layout != blank and pagination_layout != "default" -%}
        {%- include 'modules/siteglide_system/get/get_pagination', pagination_layout: _pagination_layout -%}
      {%- endif -%}
    </div>
  </div>
{% else %}
  {%- if _show_pagination == 'false' and pagination_layout != blank and pagination_layout != "default" -%}
    {%- include 'modules/siteglide_system/get/get_pagination', pagination_layout: _pagination_layout -%}
  {%- endif -%}
{% endif %}
{% endraw %}
```
