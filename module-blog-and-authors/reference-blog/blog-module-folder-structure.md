# 🌳 Blog & Author Module Folder Structure

See general module folder strucutre for folder structure in common with all modules:

{% content-ref url="../../developer-tools/go-further-dev-marketplace/building-for-marketplace/modules-folder-structure-introduction.md" %}
[modules-folder-structure-introduction.md](../../developer-tools/go-further-dev-marketplace/building-for-marketplace/modules-folder-structure-introduction.md)
{% endcontent-ref %}

\
\
Blog module layouts may contain optional extra files for components like author lists, categories etc.

Replace "custom\_example" with the name of your own custom layout. You can add as many of these as you like to the module\_3 folder.

There is also a form directory for storing form layouts for front-end module/ author item submission.

```
└───marketplace_builder
    └───views
        └───partials
            └───modules
                ├───module_3
                │   │   collection.liquid
                │   │
                │   ├───custom_example
                │   │   ├───archive
                │   │   │       sidebar.liquid
                │   │   │       sidebar_years.liquid
                │   │   │       sidebar_years_and_date_search.liquid
                │   │   │
                │   │   ├───author
                │   │   │   ├───detail
                │   │   │   │       item.liquid
                │   │   │   │       wrapper.liquid
                │   │   │   └───list
                │   │   │           item.liquid
                │   │   │           wrapper.liquid
                │   │   │
                │   │   ├───categories
                │   │   │   └───list
                │   │   │           item.liquid
                │   │   │           wrapper.liquid
                │   │   │
                │   │   ├───detail
                │   │   │       item.liquid
                │   │   │       wrapper.liquid
                │   │   │
                │   │   ├───list
                │   │   │       item.liquid
                │   │   │       wrapper.liquid
                │   │   │
                │   │   └───sidebar
                │   │           search.liquid
                │   │           wrapper.liquid
                │   │
                │   └───form
                │           default.liquid
                │
                └───module_6
                    │   collection.liquid
                    │   ├───detail
                    │   │       item.liquid
                    │   │       wrapper.liquid
                    │   └───list
                    │           item.liquid
                    │           wrapper.liquid
                    └───form
                            default.liquid
```
