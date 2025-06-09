# Truthiness - Using Liquid to determine if a field is empty or blank

How to check if a variable exists/ is null/ is false?

Not all the variables on Siteglide will be stored as either "true" or "false". In many scenarios something may exist in one location, and simply not exist in another . To better explain this i'll use a homepage as an example:

Whether a page is the homepage or not is determined by the is\_homepage variable: `is_homepage` which has the value `true`. However if a Page is not the homepage, rather than `is_homepage` being set to `false`, the `is_homepage` variable doesn't exist.

Say I wanted to run some code on every Page that isn't the homepage, I'd write something like this:

```liquid
{% raw %}
{% if context.page.metadata.is_homepage == false %}
   output content.
{% else %}
   output homepage content.
{% endif %}
{% endraw %}




```

This would work fine if we were on the Homepage, as the variable's value would be true. However, on other Pages, it would not behave as expected, as is\_homepage would be undefined..

Now lets look at the Liquid keyword "blank". This refers to having a value of either: Empty, Null or False.

If I now check "is\_homepage" like so:

```liquid
{% raw %}
{% if context.page.metadata.is_homepage == blank %}
  {% comment %}output content.{% endcomment %}
{% else %}
  {% comment %}output homepage content.{% endcomment %}
{% endif %}
{% endraw %}
```

This will now work!
