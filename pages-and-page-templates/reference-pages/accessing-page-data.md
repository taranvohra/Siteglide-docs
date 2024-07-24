# 🔧 Tags for Pages and Templates

{% hint style="info" %}
Not a Developer?\
\
In the Siteglide Admin, you can either Modify Page Content using the low-code route of the Siteglide Studio, or edit the code in the code tab. \
\
When in the code tab, you can use the Toolbox to quickly find useful snippets of code.&#x20;
{% endhint %}

## Liquid for Page Templates only

Determines where in the Page Template the dynamic content of the Page itself will sit:

```liquid
{{content_for_layout}}
```

Note though that the Page is actually rendered by the server before the Page Template, this allows Liquid to pass data from the Page to the Page Template either using Page Metadata or the `content_for` and `yield` tags.

{% embed url="https://documentation.platformos.com/api-reference/liquid/platformos-tags#yield" %}
Can receive a String in the Page Template from a content\_for tag in the page
{% endembed %}

* `{{context.page.metadata}}` - outputs the metadata of the page, though meta fields are usually automatically outputted for you inside "constants"
* `{{context.page.metadata.name}}` - outputs the Name field of the page

{% hint style="info" %}
If using CLI, check [Page Templates with Siteglide-CLI](../go-further-pages/page-templates-with-cli.md)[ ](../go-further-pages/pages-with-siteglide-cli.md)for details on Page Template only Liquid which is hidden on the Siteglide Admin.
{% endhint %}

## Liquid for Pages only

{% embed url="https://documentation.platformos.com/api-reference/liquid/platformos-tags#content-for" %}
Can send a string from a page or partial/include to the page template
{% endembed %}

{% hint style="info" %}
If using CLI, [Pages with CLI ](../go-further-pages/pages-with-siteglide-cli.md)for details on Page only Liquid which is hidden on the Siteglide Admin.
{% endhint %}

## Liquid for either Pages or Page Templates

Browse the rest of the documentation to find dynamic Liquid features you can insert into your Pages and Page Templates using Liquid tags. Almost any Liquid is suitable for outputting in either.

[about-liquid.md](../../liquid-templating-language/about-liquid.md "mention")

[alternatives-to-storing-server-side-code-in-fields.md](../../webapps-databases/go-further-webapps/alternatives-to-storing-server-side-code-in-fields.md "mention")

[Broken link](broken-reference "mention")

[Broken link](broken-reference "mention")

### Liquid Variables

For the full documentation on the platformOS `context` variable, see here: [https://documentation.platformos.com/developer-guide/variables/context-variable#displaying-the-context-object](https://documentation.platformos.com/developer-guide/variables/context-variable#displaying-the-context-object)

#### Site Data

* `{{context}}` - outputs the full extent of site data available by default on this current file

#### URL Parameters

* `{{context.location.pathname}}` - outputs the full url path such as "/first-part/second-part"
* `{{context.params.slug}}` - outputs the first part of your url path such as "/first-part"
* `{{context.params.slug2}}` - outputs the second part of your url path such as "/second-part"
* `{{context.params.myparam}}` - outputs the value of ?myparam=true

#### Page Data

* `{{context.exports.webapp_1.data.result.items[0].name}}` - Access data that has been fetched using a query earlier in the Page

## Example of URL based breadcrumbs:

This takes the URL path of the page, splits it based on / and titleizes the items.

```liquid
{% raw %}
{% assign slugSplit = context.location.pathname | remove_first: '/' | split: '/' %}
<ul>
    <li>
        <p>Home</p>
        <i class="fal fa-chevron-right"></i>
    </li>
    {% for item in slugSplit %}
        {% if forloop.last == true %}
            <li>
                <p>{{item | titleize}}</p>
            </li>
        {% else %}
            <li>
                <p>{{item | titleize}}</p>
                <i class="fal fa-chevron-right"></i>
            </li>
        {% endif %}
    {% endfor %}
{% endraw %}
</ul>
```
