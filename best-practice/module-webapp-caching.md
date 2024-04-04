***Note: Experimental***

You can improve performance of your website by implementing caching on your Module/WebApp calls.

### How do I use it?

Add a new parameter to your Module/WebApp include of `cache: 'true'`

```liquid
{%-
    include 'webapp'
    id: '9'
    layout: 'custom'
    cache: 'true'
-%}
```

### How does it work?

Caching works by generating a cache key. If the cache key value is the same each time the include loads, then the content will be loaded from cache. If that cache key value changes, then the content is loaded from the database.

The cache key is generated using the following information:

*   Module/WebApp ID

*   Most recent delete date of an item in the Module/WebApp - *So when an item is deleted, the content is reloaded to remove it*

*   Most recent update date of an item in the Module/WebApp - *So when an item is updated, the latest version is loaded*

*   Layout name - *In case you have multiple calls to a Module/WebApp on a page, this ensures the different layout is loaded in the correct the place*

*   URL parameters - *This needs to be taken into account for when search is being used, so the content returned is the relevant results*

### Why is it experimental?

This feature is new to Siteglide, and there are some situations where it may not work. For example:

*   We need to add more information to the cache key, such as `sort_type` and `per_page`

*   It's unclear how this will perform if there's a lot of nested DataSources in the layout, or calls to other Modules/WebApps/data

### What if it doesn't work?

1.  Remove the `cache` parameter, and you will revert to loading from the database each time

2.  Get in touch, and we'll investigate why it didn't work for your use-case, and we'll then be able to apply improvements across the board to the feature.***

    ***

