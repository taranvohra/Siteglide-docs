# 👀 Includes Reference

## The Include Tag and Custom Paths

The Liquid tag `include` is usually used to insert a Liquid Partial into a Liquid File.&#x20;

{% embed url="https://documentation.platformos.com/api-reference/liquid/include" %}

Sometimes this can link to one of your files directly, simply pass in a String containing a custom path to your file. The path must start relative to the partials folder and must not include the file extension:

{% content-ref url="includes-file-structure.md" %}
[includes-file-structure.md](includes-file-structure.md)
{% endcontent-ref %}

Sometimes it will link to a hidden Siteglide Module file, which may in turn include one of your customisable "layout" Liquid files.

### Types of Include

To include one of Site's common include types, use these below and pass in the ID of the include (or the filename without the extension which will be the same). Name is a completely optional parameter.

```liquid
{% raw %}
{% include 'header', id: '1', name: 'optional to help code readability' %}
{% include 'footer', id: '1', name: 'optional to help code readability' %}
{% include 'content_section', id: '1', name: 'optional to help code readability' %}
{% include 'code_snippet', id: '1', name: 'optional to help code readability' %}
{% endraw %}
```

### Inheritance

The include tag will always pass down all variables initiated above it to the file that has been included.

These can be either implicit or explicitly passed:

```liquid
{% raw %}
{% assign implicit_variable = 'a' %}
{% include 'my_file', explicit_variable: 'b' %}
{% assign varible_with_no_scope = 'c' %}
{% endraw %}
```

For this example, `implicit_variable` and `explicit_variable` will have scope inside the partial file when it is rendered, but `varible_with_no_scope` will not, simply because it is initialised after the include tag in the page.&#x20;

There are also alternative tags which have a different inheritance behaviour:

{% embed url="https://documentation.platformos.com/api-reference/liquid/platformos-tags#function" %}

{% embed url="https://documentation.platformos.com/api-reference/liquid/platformos-tags#theme-render-rc" %}

If you want to pass variables from the partial file up to the page, you need to use either of these methods:

{% embed url="https://documentation.platformos.com/api-reference/liquid/include#private-variables-and-exporting-them" %}

{% embed url="https://documentation.platformos.com/api-reference/liquid/platformos-tags#function" %}
