The following code example can be added to a Page Template and applied to the home/start page of a site to load a different start page for different domains added to the site.

This method does however remove some of the ease of editing for the client, as they will not be able to use Visual Editor to manage the pages that are setup this way. We'll look at adding a smoother point and click version to Admin later.

One use case for this approach would be where a client has a small chain of businesses that each have their own domain to target the area closest to them. Each of the sites are very small and the website structure is reasonably similar, and so it makes sense for the client to be able to manage all of them from the same Admin.

```html
{% assign domain = context.location.host -%}

{% case domain %}

{% when 'www.domainone.com' or 'domainone.com'  -%}

  {% content_for siteglide_head_scripts -%}
    <title>Home - Domain One</title>
  {% endcontent_for -%}
  {%- include 'content_section', id: '17', name: 'Domain One Page' -%}

{% when 'www.domaintwo.com' or 'domaintwo.com' -%}

  {% content_for siteglide_head_scripts -%}
    <title>Home - Domain Two</title>
  {% endcontent_for -%}
  {%- include 'content_section', id: '15', name: 'Domain Two Page' -%}

{% else -%}

  {% content_for siteglide_head_scripts -%}
    <title>Home - Other Domain</title>
  {% endcontent_for -%}
  {%- include 'content_section', id: '16', name: 'Other Domain Page' -%}
{% endcase -%}
```

I'll now explain the code snippet above and how it works. 

On the first line we get the current domain (`context.location.host` ) when the page loads and assign it so that it has a name of `domain` .

Next, we open a `case` to check the result of `domain` . 

For each of the alternate domains we would like to check for, we create a `when` within the `case` . We include two versions of the domain to catch the majority of users. One that includes the [www](). and another that does not.

Inside each `when` we call in a content section that should contain all of the page content. We also define an SEO page title to match our page and wrap that in `siteglide_head_scripts` to automatically move it to the head on page load (Check out this document to find out more: [Siteglide Scripts](https://help.siteglide.com/article/224-siteglide-scripts)).

We then add an `else` at the end of the `case` to cover the default domain e.g. "if neither of these alternate domains are used, then do this" which acts somewhat like a catch all.

Finally, we close the `case`.

Using the above example, visitors will see unique page content to each domain when they visit. When they click on links on the page, they will continue to other pages on the site while keeping the same domain unless you hard code a full domain URL on a link. Please note that by adding more than one domain to a site, technically all content is accessible via all domains. Though you can effectively make content hidden from domains by not adding it to pages, it could still be accessed.
