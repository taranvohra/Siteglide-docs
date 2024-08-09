# ℹ️ About Page Templates

Page Templates are used for organising the repeatable content you will want to display on multiple pages, including Headers and Footers

## Introduction

Page Templates are used to easily and consistently apply the same global content to pages, such as: Headers, Footers, Global Stylesheets and Analytics Tracking Scripts.

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

</div>
```

While editing a Page, you can assign a Template using the Page Template drop down and then clicking Save.

Note: Toolbox functionality will soon be added to the templates section of Admin, allowing you to easily select elements to add to the page.

## Page Templates on platformOS

Page Templates on Siteglide are called Layouts on platformOS: [https://documentation.platformos.com/developer-guide/pages/layouts](https://documentation.platformos.com/developer-guide/pages/layouts)
