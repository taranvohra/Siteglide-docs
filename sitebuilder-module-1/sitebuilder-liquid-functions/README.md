# 👀 SiteBuilder Liquid Functions

### Introduction <a href="#introduction" id="introduction"></a>

In this section of the documentation, we'll cover some common Liquid functions which SiteBuilder adds into Layouts so you can understand what this code is doing and, if you like, use them yourself.

A Liquid function is similar to an `include` tag except that they return a single variable instead of printing to the page. They are also close to being "pure" functions in that they do not inherit variables other than the ones you pass to them explicitly inside the tag, making them more reliable and less prone to unexpected side-effects.

Read more about Liquid functions here: [Liquid Functions](https://documentation.platformos.com/api-reference/liquid/platformos-tags#function).

### Versioning <a href="#versioning" id="versioning"></a>

These functions can be modified by future versions of SiteBuilder. The `/v1/` in the path will be updated for newer versions of the functions. Newly installed Layouts will use the new version, but your existing code can continue to use the older versions, for backwards compatibility.
