When you use URL query parameters e.g. "?page=2" to control dynamic content on Siteglide, you can help search engines understand these.

# Introduction

Query parameters are a really useful way to pass infomation to the Server to help it deliver dynamic, relevant content.&#x20;

The problem with query parameters is that sometimes they make the same page look like multiple Pages with "duplicate content". This is not ideal from an SEO point of view as Search Engines like to offer Users unique Pages relevant to their search terms.&#x20;

Let's say we have the "About" page and this contains a WebApp which can be searched.

We have the main URL:`/about`
but search engines have incorrectly identified other URLS:&#x20;

*   `/about?keyword=hello%20world`

*   `/about?keyword=hello%20mars`

# Using Canonical URL

In your Page Template in the \<head> you can set a recommendation that where query parameters are used, the Canonical URL should be treated as the most important version of the Page to index, whereas other variations are subsidiary and should not be ranked unfavourably for being similar to the Canonical "main" version .

You can do this by setting the main part of the URL as the canonical URL. In this example, this will be applied to every Page which uses this [Page Template](/cms/pages/page-templates/README.md), but you may wish to use an if statement to only apply it on certain Pages.

```liquid
{% raw %}
<head>
  <!-- Stops Search Engines treating the same page with different URL parameters as duplicate pages -->
  <link rel="canonical" href="{{context.headers.PATH_INFO}}">
</head>
{% endraw %}
```

In the example, we use the "context.headers" object to read the URL of the page, specifically the "PATH\_INFO" which excludes query parameters, but includes slugs. This means you don't need to change this for each page- the liquid dynamically works out the current URL without query parameters. You can (and should) adjust this based on your site's structure and SEO needs.

# Using Robots.txt

Adding the following to your robots.txt file (see [System Pages](/pages-and-page-templates/get-started-pages/system-pages.md)) would stop Search Engines from crawling any Pages using URL parameters: `Disallow: /*?*`

You could be more specific and just make sure the variant Pages created by Pagination are not included: `Disallow: /*?*page=*`

When following these examples, make sure to double-check you are not excluding query parameters which genuinely should be crawled as Pages in their own right. Each Site will have different SEO needs.&#x20;

See the same question on StackOverflow for more details: <https://stackoverflow.com/questions/9149782/ignore-urls-in-robot-txt-with-specific-parameters>