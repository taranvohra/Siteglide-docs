# 🌳 Pages and Page Templates File Structure

All Liquid files live somewhere inside the views folder.

Since Page Templates are called Layouts in platformOS, this is their name in the file structure.&#x20;

[Page Templates](page-templates.md) (Layouts) in a Siteglide site should be stored in a templates sub-folder and named by their unique ID in Siteglide.&#x20;

[Pages ](about-pages.md)can be anywhere in the pages folder. They can have any file name and use any subfolders you like. By default their URL will be relative to the pages folder, but you can change this using the slug in YAML, or by changing the URL in the Siteglide Admin.

<pre><code>marketplace_builder/
├── views/
│   ├── layouts/
│   │   └── templates/
│   │       ├── 1.liquid
│   │       └── 2.liquid
│   ├── pages/
│   │   ├── system_pages/
│   │   │   └── 404.liquid
<strong>│   │   ├── home.liquid
</strong>│   │   └── about.liquid
│   └── partials/
</code></pre>

We've only shown one [system page](system-pages-explained.md) as an example, more are available.
