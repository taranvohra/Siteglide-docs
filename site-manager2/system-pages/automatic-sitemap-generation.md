You can output a list of pages using the following include:

```liquid
{% raw %}
{% include 'sitemap', layout: 'xml', types: 'pages' -%}
{% endraw %}
```

- layout - xml or html - These are set layouts for each type. html will output in <ul><li> format.

- types - Choose what types of content you want to show, by submitting a comma separated list from these options: pages,webapps,modules,products

The sitemap will only show items that are enabled, have a detail view, have a slug and are within their released/expired timeframe.

For best results, use this include on your sitemap.xml System Page (with the xml layout) or your own custom Page (with the html layout)