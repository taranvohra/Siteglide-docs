
# Introduction

Once you've added a Host to Events, you can use Datasources to output the Host's Details on the Event List or Detail Layouts.&#x20;

# Syntax

Add the following Liquid:

```html
{% include "modules/siteglide_authors/get/get_item_author"
   author_id: this.properties.module_field_12_4
   author_layout: "design_system/1/author"
   author_layout_type: "detail"
%}
```

