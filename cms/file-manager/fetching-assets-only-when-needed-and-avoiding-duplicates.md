---
description: >-
  Teleporting Scripts to the Head and Footer with siteglide_head_scripts and
  siteglide_footer_scripts or using context.exports to avoid duplicates
---

# 🔹 siteglide\_head\_scripts and siteglide\_footer\_scripts Explained

### Introduction

Typically when building a website, we have one or two core stylesheets and JavaScript files that contain the styling for your entire website.

When building large sites, however, these files can contain many thousands of lines of code. This can mean that loading the head files for the entire website on each and every page, can become unwieldy and slow.

`siteglide_head_scripts` and `siteglide_footer_scripts` can be used anywhere on a page and automatically move their contents to either the `<head>` or to before the closing `</body>` tag respectively.

This allows you to include a JS file only when it becomes relevant to a particular snippet of Liquid code, yet still output that `<script>` or `<link>` tag file a maximum of one time per page and in the most optimum position in the DOM.

#### Head Scripts

`siteglide_head_scripts` moves the contained assets into the `<head>` of your page when it renders. You must include `,,` on the end of each line within this liquid tag.

```liquid
{% raw %}
{% content_for 'siteglide_head_scripts' %} <link rel="stylesheet" href="{{'css/modules/module_3/design_system/1/sidebar.min.css' | asset_url}}" />,,{% endcontent_for %}
{% endraw %}
```

#### Footer Scripts

`siteglide_footer_scripts` moves the contained assets to the bottom of the body tag on your page when it renders. You must include `,,` on the end of each line within this liquid tag.

```liquid
{% raw %}
{%- content_for 'siteglide_footer_scripts' %} <link rel="stylesheet" href="{{ 'css/modules/module_9/custom.css' | asset_url}}" />,,{%- endcontent_for %}
{% endraw %}
```

#### Troubleshooting

**Problem**

My JavaScript console has the error: `Uncaught SyntaxError: Unexpected end of input`?

**Solution**

This error can occur if you use single-line comments in your inline JavaScript and then wrap that script inside the head or footer scripts. It's because the newlines are removed from the JavaScript- meaning the single-line comments do not end when they should.

You can fix it by moving your JavaScript to an external file or replacing single-line comments `//` with opening `/*` and closing `*/` JavaScript comments.

#### Performance and Avoiding Duplicates

When you use `content_for` you can add resources from many different files and they'll all output together in the `<head>` or before the closing tag. While this is convenient, you should be especially wary of accidentally including the exact same resource twice and slowing down your page.

To help avoid this, Siteglide will attempt to check the tags you've added for any duplicates before outputting. This happens on the server-side. Adding two commas ,, at the end of each line, allows this functionality to work.

We'd still recommend you check your Page Source for any duplicate resources. It's still possible for this to happen if you add the same resource to `siteglide_head_scripts` from two different Layouts with different CDN links each time. Also it can happen if you send one tag to the `siteglide_head_scripts` and another to the `siteglide_footer_scripts.`

Duplicate checking checks for duplicate tags, it doesn't follow the links and check for duplicate content. If you always load from our CDN using `| asset_url` the risk of this is reduced.

#### Using content\_for with your own namespace

The platformOS docs explain how you can add any namespace to the `content_for` tag and use it in conjunction with the yield tag to send any variable from the Page to the Page Template.

Content For: [https://documentation.platformos.com/api-reference/liquid/platformos-tags#content\_for](https://documentation.platformos.com/api-reference/liquid/platformos-tags#content\_for)

Yield: [https://documentation.platformos.com/api-reference/liquid/platformos-tags#yield](https://documentation.platformos.com/api-reference/liquid/platformos-tags#yield)

If using this, we'd recommend again that you check for any duplicate resources, as at the time of writing there is a known issue with this technique. For now, there are two ways to make this work:

* Use our namespaces listed above
* Use the `flush: 'true'` parameter to prevent duplicates occurring. This empties the namespace clean each time you add something- meaning you can only add content to the namespace once.

### Alternatives - Using context.exports

Another way of avoiding duplicate entries of assets in your code, only pulling them in when the page needs them is to use the context.exports variable to keep track of them. This is the method most often used by SiteBuilder.

```liquid
{% raw %}
{% if context.exports.sitebuilder.live_update_JS_loaded == blank %}
  <script async src="{{'modules/module_86/js/v1-5/sitegurus_live_update_javascript_api.min.js' | asset_url }}"></script>
  {% assign live_update_JS_loaded = true %}
  {% export live_update_JS_loaded, namespace: sitebuilder %}
{% endif %}
{% endraw %}
```

The if statement checks if the \<script> has already been outputted; the next line outputs the \<script>, if not.

The next two lines store a new variable in exports to make sure the same code will know not to output the same again.

This method does not have the benefit of "teleporting" your code to the `<head>` or closing `</body>` tag, but it works well with `<script>` tags with the `async` or `defer` attributes.
