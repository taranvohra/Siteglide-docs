# 👀 Reference: Categories

## Global List of Categories

### Outputting the Categories Data Variable as JSON

The following Liquid outputs a JSON object containing the details of all Categories:

`{{context.exports.categories.data}}`

This object stores every category in key-value pairs where the key is the ID of the Category and the value is an object containing all other available fields.

## Accessing a specific Category via ID

As the Categories data Object is a key map, you can access any specific category by accessing the object and then passing in the Category's ID in square brackets: \
\
`{{context.exports.categories.data['1234']}}`

## Accessing a Category's Fields

Once you've accessed the value of that Category via it's ID, you can access that Category's Fields using dot notation. For example, here we'll access its name: \
\
`{{context.exports.categories.data['1234']}}.name}}`

Other available fields are:

* `id` - the ID of the Category
* `name` - the name of the Category
* `parent` - the ID of the Parent Category if there is one
* `slug` - the end of the URL for the Category Detail Page which is unique to this Item
* `meta_title` - the meta-title of the Category
* `meta_desc` - the meta-description of the Category
* `og_title` - the open graph title of the Category
* `og_desc` - the open graph description of the Category
* `og_type` - the open graph type of the Category
* `twitter_type` - the twitter type of the Category
* `full_slug` - the full (relative) URL for the Category Detail Page

## Looping over all Categories on the Site

If you wish to display all the Categories on the Site, you can loop over them all. Inside the For Loop you can display any HTML or Category fields you like.

```liquid
{% raw %}
{% for category in context.exports.categories.data %}
  {{category[0]}} <!-- Category ID -->
  {{category[1]}} <!-- Current Category JSON Object -->
  {{category[1].name}} <!-- Accessing current Category's field e.g. name -->
{% endfor %}
{% endraw %}

```

If you want to skip any Categories, you can use Liquid if statements and the `continue` tag to do this:

```liquid

{% raw %}
{% for category in context.exports.categories.data %}
  {% if category[1].name == "name_of_category_I_want_to_skip" %}
    {% continue %}
  {% endif %}
  {{category[1].name}} <!-- Accessing current Category's field e.g. name -->
{% endfor %}
{% endraw %}
```

### Filtering WebApps and Modules

```
{% include 'module'
   id: '3'
   layout: 'default'
   per_page: '20'
   sort_type: 'properties.name'
   sort_order: 'asc'
   category_ids: '1,2' 
%}
```

See more here:

{% content-ref url="../advanced-categories/filtering-webapps-and-modules-by-categories.md" %}
[filtering-webapps-and-modules-by-categories.md](../advanced-categories/filtering-webapps-and-modules-by-categories.md)
{% endcontent-ref %}

## Category Detail Pages

{% hint style="info" %}
:computer: Siteglide-CLI tip:  We strongly advise against editing the Category Detail Page itself on Siteglide CLI, as it could be changed at any time by the system. Stick to editing the Category Detail Layout!
{% endhint %}

Default Fields

The following tags are available within the Category Detail Layout:

| **Field Name** | **Liquid Tag**         | **Description**      |
| -------------- | ---------------------- | -------------------- |
| Category Name  | `{{ this.name }}`      | Name of the category |
| Category URL   | `{{ this.full_slug }}` | URL of the category  |
| Category ID    | `{{ this.id }}`        | ID of the cateogory  |

You can use any of the Liquid which you can use on Pages in the Category Detail Layout:

{% content-ref url="../../pages-and-page-templates/accessing-page-data/" %}
[accessing-page-data](../../pages-and-page-templates/accessing-page-data/)
{% endcontent-ref %}

Category Detail Pages give you additional features including Breadcrumbs, Parent Category Lists, Child Category Lists and more.

### Breadcrumbs

Output breadcrumb of Categories to the current Category page using the defined layout:`<div data-gb-custom-block data-tag="-" data-0='category_breadcrumbs' data-1=', layout: ' data-2='breadcrumb'></div>`

### Parent Category List

Output parent Categories using the defined layout: `<div data-gb-custom-block data-tag="-" data-0='category_parent' data-1=', layout: ' data-2='parent'></div>`

### Child Category List

Output child Categories using the defined layout: `<div data-gb-custom-block data-tag="-" data-0='category_children' data-1=', layout: ' data-2='children'></div>`

### Items in this Category

Output all items categorised to the current Category Page using the defined layout: `<div data-gb-custom-block data-tag="-" data-0='category_items' data-1=', layout: ' data-2='items'></div>`

Note that this will only output items in this specific Category. To output all items that belong to sub-Categories, then add another parameter of `show_all_sub_items: 'true'`.

### Output Filtered WebApp, Module and Product Items in this Category

You can use the Category ID `{{this.id}}` to filter WebApp, Module or Product Lists and display the Items with this Category assigned (and those belonging to Categories which are children of this Category).

We'll include some examples here of how the `{{this.id}}` variable can be used specifically on the Category Detail Page to filter by that Detail Page's Category dynamically:[ Learn more about filtering WebApps and Modules by Category](https://developers.siteglide.com/filtering-webapps-and-modules-by-categories)

### Products

For example, the following code will output Products on the Category Detail Page, filtered by that Category:

```liquid
{%- include 'ecommerce/products'
    layout: "my_layout"
    category_ids: this.id
    type: 'list' 
-%}

```

### WebApps

Change the ID to fetch different WebApps.

```liquid
{%- include 'webapp'
    id: '1'
    layout: "my_layout"
    category_ids: this.id
    type: 'list' 
-%}

```

### Modules

Module 3 refers to the Blog; you can change the ID to fetch different Modules.

```liquid
{%- include 'module'
    id: '3'
    layout: "my_layout"
    category_ids: this.id
    type: 'list' 
-%}
```

## WebApp and Module Layouts

To access the category which belongs to the item currently being outputted in a WebApp layout or a Module layout's item.liquid layout, access the category\_array field in:

```liquid
{{this.properties.category_array}}
```

See more:

{% content-ref url="../advanced-categories/outputting-categories-on-webapp-module-ecommerce-layouts.md" %}
[outputting-categories-on-webapp-module-ecommerce-layouts.md](../advanced-categories/outputting-categories-on-webapp-module-ecommerce-layouts.md)
{% endcontent-ref %}
