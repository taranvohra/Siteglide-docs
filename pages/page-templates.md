# Page Templates

Page Templates are used for organising the repeatable content you will want to display on multiple pages, including Headers and Footers

## Introduction

[Page Templates](https://help.siteglide.com/article/218-templates-getting-started) are used to easily and consistently apply the same global content to pages, such as: Headers, Footers, Global Stylesheets and Analytics Tracking Scripts.

## Adding Page Templates

You can create a new page template by navigating to `CMS / Templates` and clicking the blue “+ Add new template” button. New Templates are automatically added to the drop down in Pages once created.

## Editing Page Templates

You can edit existing Templates by clicking the edit button next to each, while looking at the list of templates.

## An Example Page Template

Page content will be outputted where the liquid tag `{{content_for_layout}}` is located within your Template.

Here is how a generic Page Template file should be structured:

```liquid
{% raw %}
{% include 'site/constants' -%}
<!doctype html><html lang="en">
  <head>
    {% include 'code_snippet', item: '1', name: 'SEO' -%}
    {% include 'code_snippet', item: '2', name: 'HTML Head' -%}
  </head>
  <body>
    <section id="visualEditor" style="display: none">
      {% include 'site/visualEditor'-%}
    </section>
    {% include 'header'
       template: "1"
       header_image: "images/fido/logo-white-bg.svg"
       group_id: "11149" -%}
    <main>
      {{content_for_layout}}
    </main>
    {% include 'footer', template: "1" -%}
    {% include 'site/visualEditor' type: 'js'-%}
{% endraw %}
  </body>
</html>
```

While editing a Page, you can assign a Template using the Page Template drop down and then clicking Save.

Note: Toolbox functionality will soon be added to the templates section of Admin, allowing you to easily select elements to add to the page.
