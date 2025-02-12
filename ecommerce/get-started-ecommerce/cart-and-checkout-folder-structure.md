# 🌳 Cart and Checkout Folder Structure

Some layouts have a wrapper and an item file, while other layouts have a single Liquid file.

{% hint style="info" %}
Checkout and Quote Forms use ordinary Form Layouts, despite using a different Liquid tag to output them. \
\
The marketplace\_builder/views/partials/layouts/modules/module\_14/checkout directory doesn't store a Checkout layout, instead it stores an "empty" file which will be displayed instead of Checkout if the Cart is empty.
{% endhint %}

```
marketplace_builder
└───views
    └───partials
        └───layouts
            ├───forms
            │    └───form_1
            │       │    default.liquid
            │       │    custom_layout.liquid
            │       │    sitebuilder_layout.liquid
            │       └─── sitebuilder_layout_components
            │               array_custom.liquid
            │               basic_payment.liquid
            │               ...
            └───modules
                ├───module_5
                │   └───user_orders
                │       default.liquid
                │       order_list_custom_layout.liquid
                └───module_14
                    ├───checkout
                    │   ├───custom_layout
                    │   │    empty.liquid
                    │   └───default
                    │        empty.liquid
                    ├───components
                    │   ├───add_to_cart_button
                    │   │   default.liquid
                    │   │   custom_layout.liquid
                    │   ├───currency_changer
                    │   │   ├───default
                    │   │   │       item.liquid
                    │   │   │       wrapper.liquid
                    │   │   └───custom_layout
                    │   │           item.liquid
                    │   │           wrapper.liquid
                    │   ├───reorder_button
                    │   │       default.liquid
                    │   │       custom_layout.liquid
                    │   └───tax_code_changer
                    │       ├───default
                    │       │       item.liquid
                    │       │       wrapper.liquid
                    │       └───custom_layout
                    │               item.liquid
                    │               wrapper.liquid
                    ├───discount_code
                    │   │   custom_layout.liquid
                    │   ├───basic_payment
                    │   │       default.liquid
                    │   ├───cart
                    │   │       default.liquid
                    │   └───subscription
                    │           default.liquid
                    ├───order
                    │   │   collection.liquid
                    │   ├───default
                    │   │   └───detail
                    │   │           item.liquid
                    │   │           wrapper.liquid
                    │   ├───email
                    │   │   └───detail
                    │   │           item.liquid
                    │   │           wrapper.liquid
                    │   └───custom_layout
                    │       └───detail
                    │               item.liquid
                    │               wrapper.liquid
                    ├───product
                    │   collection.liquid
                    │   ├───custom_product_layout
                    │   │   ├───detail
                    │   │   │   item.liquid
                    │   │   │   wrapper.liquid
                    │   │   └───list
                    │   │       item.liquid
                    │   │       wrapper.liquid
                    │   ├───custom_cart_layout
                    │   │   └───list
                    │   │       item.liquid
                    │   │       wrapper.liquid
                    │   └───product_feed
                    │       └───list
                    │           item.liquid
                    │           wrapper.liquid
                    ├───product_attributes
                    │      custom_attributes_layout.liquid
                    └───shipping_option
                           default.liquid
                           custom_shipping_layout.liquid
```
