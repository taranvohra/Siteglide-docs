# 🔹 Social Sharing JS

The Sitegurus social sharing is a light wrapper around an open source JavaScript Plugin called Vanilla Sharing. It was added in order to save time and easily allow the functions to be implemented using data-attributes.

### Normally included in <a href="#normally-included-in" id="normally-included-in"></a>

Layouts where sharing functionality is needed.

We use `context.exports` to make sure the script is only loaded once on the page:

### Script Code <a href="#script-code" id="script-code"></a>

```liquid
{% raw %}
{% if context.exports.module_86.sitegurus_social_share_api != true %}
  <script async id="sitegurus_social_share_api" src="{{'modules/module_86/js/sitegurus_social_share_api.js' | asset_url}}" charset="utf-8"></script>
  {% assign sitegurus_social_share_api = true %}
  {% export sitegurus_social_share_api, namespace: "module_86" %}
{% endif %}
{% endraw %}
```

### Usage <a href="#usage" id="usage"></a>

We use [vanilla-sharing documentation](https://www.npmjs.com/package/vanilla-sharing) and power it using data-attributes, so this documentation is vital for understanding usage.

Add `data-s-g-social-feature` to a `<button>` element to make it a sharing button. The value of the attribute should be the name of one of the functions listed in the vanilla-sharing documentation, or you can also use `data-s-g-social-feature="clipboard"` which creates a button for copying the URL to the clipboard.

Add `data-s-g-option-<option-name>="<option-value>"` to the same element to add options from the vanilla-sharing documentation. Any array type options like `data-s-g-option-hashtags="hashtag,hashtag2,hashtag3"` should be given a comma-seperated string value and we'll convert these to an array for you.

The `data-s-g-option-url` is normally a required option and if you leave it blank, we'll default to the current page URL!

Full Twitter example:

```liquid
<button data-s-g-social-feature="tw" data-s-g-option-url="https://sitegurus.io" data-s-g-option-hashtags="test,testing,ilovetesting">Tweet about Sitegurus!</button>
```
