---
title: List View
slug: 3iPV-
createdAt: 2021-02-19T12:24:11.000Z
updatedAt: 2023-03-03T08:09:58.000Z
---

This view allows you to display available Subscription products for customers to browse through.

# Introduction

&#x20;The Subscriptions List View displays a list of Subscription products. Like other List Views, it can be sorted and filtered via Liquid.&#x20;

This is slightly different from the `user_subscriptions` List view in the Secure Zones Module. This can be used to display a List of Subscription Orders belonging to a User. [Learn more here](https://developers.siteglide.com/user-subscriptions-list-the-logged-in-users-subscription-orders).

# Outputting a List View

&#x20;You can use the type parameter to output a List Layout in most Liquid files:

```html
{% include "module", id: "14/subscription"
   item_ids: subscription_id
   type: "list"
   layout: 'my_layout' 
%}
```

# File Structure

Subscription Layouts can be found at the path: `layouts/modules/module_14/subscription`
Within this folder, you can create a folder for each Layout. Each Layout folder can contain a further "list" folder containing the `wrapper` and `item` files it needs.&#x20;

![](https://downloads.intercomcdn.com/i/o/224826419/38930a154d559d6c0445b9c9/image.png)

# Developing the List Layout

## The Wrapper

&#x20;The `wrapper.liquid` file should be used to add any HTML structure you may require around your main list.

You must include the following Liquid, which will in turn loop over the Items and output the `item.liquid` file for each Subscription Item. Most fields are specific to the Item and will only be available inside the `item.liquid` file.&#x20;

```html
{%- include 'modules/siteglide_ecommerce/ecommerce/get/get_subscriptions'
    item_layout: 'item' 
-%}
```

## Fields

*Subscription Fields*

*   `{{this}}`- Output all fields as JSON

*   `{{this.id}}`

*   `{{this.weighting}}`

*   `{{this.release_date}}`

*   `{{this.expiry_date}}`&#x20;

*   `{{this['Description']}}`

*   `{{this['Interval']}}`

*   `{{this['Interval Count']}}`

*   `{{this.full_slug}}` - URL for the Product Detail Page

*   `{{this['Secure Zones']}}` - Array containing the IDs of Secure Zones associated with this Subscription.

*   `{{this.price.id}}`

*   `{{this.price.currency}}`

*   `{{this.price.price_charge}}` - The chargeable price of this Subscription each Interval. Integer format.

*   `{{this.price.price_display}}` - A field for displaying a secondary price of your choice, e.g. recommended retail price. This is not used by the integration. Integer format.

*   `{{this.price.currency_symbol}}`

*   `{{this.price.price_charge_formatted}}` - The chargeable price of this Subscription each Interval. Currency format

*   `{{this.price.price_display_formatted}}` - A field for displaying a secondary price of your choice, e.g. recommended retail price. This is not used by the integration. Currency format.

*Subscription Order Fields
*You'll see when developing a [Subscription Detail Page](https://developers.siteglide.com/detail-layout) that when the User is logged in, it is also possible to access fields relating to a subscription\_order the User has made for that Subscription product already.&#x20;

This is not currently available on the List view- as the List view is designed as a way to browse Subscription products. To allow the user to view and manage their Subscription Orders, we recommend the [User Subscriptions view](https://developers.siteglide.com/user-subscriptions-list-the-logged-in-users-subscription-orders).