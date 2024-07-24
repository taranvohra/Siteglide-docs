---
title: Migrate - Convert existing Forms
slug: o1sp-migrate-convert-existing-forms
createdAt: 2021-07-27T10:11:47.000Z
updatedAt: 2023-04-11T10:47:53.000Z
---

# 🔼 Siteglide CLI Migrate Command - Converting Forms

{% hint style="info" %}
This article refers to working with forms after using the Siteglide-CLI command to migrate a static website. \
\
This is only necessary if you have used this command and are setting up Forms within the Siteglide Admin.
{% endhint %}

### Set Template

When the page is moved into Siteglide from the CLI Migration flow, it will have a default template applied called "application".

This template will need to be replaced with a template made from within Siteglide Admin. Make sure that you have [created a template](https://help.siteglide.com/article/218-templates-getting-started#2-creating-a-template) and then [applied that template to a page](https://help.siteglide.com/article/218-templates-getting-started#2-adding-templates-to-pages).

This is neccesary as the template will have some automatic included scripts that is used within form submission.

### Replace Form

Your page will have a section in your page where the existing form has been running. This will look something like the below:

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

Although your form will be different, it will always start and end with a `<form>` tag. After finding that part of your page you should delete this area of the page and replace that with your newly created Siteglide form using the Toolbox.
