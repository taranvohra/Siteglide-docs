---
title: Migrate - Convert existing Forms
slug: o1sp-migrate-convert-existing-forms
createdAt: 2021-07-27T10:11:47.000Z
updatedAt: 2023-04-11T10:47:53.000Z
---

This document will cover converting an existing HTML form that has been moved to Siteglide from the CLI Migrate command.  This document assumes that you have [already setup the form](https://help.siteglide.com/article/99-forms-getting-started) within Siteglide and just covers putting that form into the page.

## Set Template

When the page is moved into Siteglide from the CLI Migration flow, it will have a default template applied called "application".&#x20;

This template will need to be replaced with a template made from within Siteglide Admin.  Make sure that you have [created a template](https://help.siteglide.com/article/218-templates-getting-started#2-creating-a-template) and then [applied that template to a page](https://help.siteglide.com/article/218-templates-getting-started#2-adding-templates-to-pages).&#x20;

This is neccesary as the template will have some automatic included scripts that is used within form submission.

## Replace Form

Your page will have a section in your page where the existing form has been running.  This will look something like the below:

```html
<form>
    <div class="form-input">
        <input type="text" id="name" />
    </div>
    <div class="form-input">
        <input type="email" id="email" />
    </div>
</form>
```

Although your form will be different, it will always start and end with a `<form>` tag. After finding that part of your page you should delete this area of the page and replace that with your newly created Siteglide form [using the toolbox](https://help.siteglide.com/article/100-pages-getting-started#2-code)
