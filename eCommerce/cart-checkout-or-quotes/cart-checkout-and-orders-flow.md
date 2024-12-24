---
title: Cart, Checkout and Orders Flow with Secure Zones Module - Tutorial
slug: 0tKU-
createdAt: 2021-02-19T09:40:35.000Z
updatedAt: 2023-04-06T15:38:18.000Z
---

This Tutorial shows you how to use the eCommerce and Secure Zones Modules together

## Prerequisites:

*   You have read [How to Set Up a Shopping Cart and Guest Checkout](https://help.siteglide.com/article/163-how-to-set-up-a-shopping-cart-and-guest-checkout-tutorial)

*   You have installed the [eCommerce Module](https://help.siteglide.com/article/200-getting-started-with-siteglide-ecommerce)

*   You have installed the [Secure Zone Module](/crm/quickstart-crm.md)

*   *Using PayPal as a Payment Gateway?* There are additional setup instructions [here](https://help.siteglide.com/article/165-payment-gateways).

## Introduction

Siteglide eCommerce is even more powerful with Secure Zones. With the security of a Secure Zone, you can show your Users more sensitive data about their shopping experience.

## 1) Create a Secure Zone

Create a Secure Zone which will used by shoppers on your eCommerce site. Alternatively, you can use a Secure Zone that you have created already. Find out more about the Secure Zones Module [here](/crm/quickstart-crm.md#2-creating-and-editing-a-secure-zone).

## 2) Create a "My Orders" Page in a Secure Zone

![](https://siteglide-52c14a1a8a9b.intercom-attachments-1.com/i/o/163533694/4e550e2d1436b94c1f3fc26e/orders_secure_zone.jpg)

Create a new page which will display a list of Products Users have ordered. Learn more about creating Pages here. Make a note of the Page slug, because you will want to add this to the Checkout Form’s "Redirect URL" field later.

Click the Secure Zones accordion to reveal the "Select a Secure Zone" field. Click in this to open a drop-down list of your Secure Zones and select the one you wish to be accessed by Users after they complete Checkout.

![](https://siteglide-52c14a1a8a9b.intercom-attachments-1.com/i/o/163533699/38512098b8e57b8e3780419c/orders_secure_zone_select.png)

## 3) Add the Secure Zone to the Checkout Form

![](https://siteglide-52c14a1a8a9b.intercom-attachments-1.com/i/o/163533709/a38f01187f2eef19fddc80b5/form_secure_zone.jpg)

Make sure your Checkout Form is still in "Test Mode" unless the Site is Live.

The document How to Set Up a Shopping Cart and Guest Checkout, explained how to create a Checkout Form. Here we will modify this form so that it also either signs in a User or logs them in, depending on their current status.Find Forms in the Siteglide Admin’s left-hand side menu under CMS / Forms. Select the pencil icon on the right hand side of your Checkout Form to edit the structure of your form.

In the "Redirect URL" field add your Orders Page slug, preceded by a forward slash. E.g. `/my-orders`

Select the Secure Zones tag and then click in the Secure Zones Input field to see a dropdown of Secure Zones you have already created.

Select the Secure Zone you want to log your Users in to when they complete the form.

Press the "Save" Button to save your changes. At this point:

1.  Completing the Checkout Form will log Users in to the Secure Zone

2.  It will also redirect the Users to the My Orders Page

3.  The Users will be allowed to access the My Orders Page, because they are logged into the Secure Zone.

4.  Other Users who are not logged in will be unable to access the My Orders Page.

## 4) Create an Orders List Layout

As Orders List Layouts are for showing secure information about Users, they are stored under the following file structure:

*   `layouts`
    *   `modules`
        *   `module_5`
            *   `user_orders`
                *   `name_of_my_layout.liquid`

Create a new file in the user\_orders folder and give it a name of your choice. Make a note of the name you gave it.

## 5) Develop your Layout

Your layout will have access to the "orders" object.
You can loop over each order in the "Order" object with the following liquid (the "order" variable can be renamed to anything you like):

```liquid
{% raw %}
{%- for order in orders -%}

{%- endfor -%}
{% endraw %}
```

Inside this loop, you can access the following fields. (If you have renamed the order variable, make sure you also rename it when outputting the fields.)

| **Field Name**   | **Liquid Tag**                | **Description**                                       |
| ---------------- | ----------------------------- | ----------------------------------------------------- |
| Order ID         | {{ order.id }}                | The unique ID of the order                            |
| Order URL        | {{ order.slug }}              | The unique slug of the order                          |
| Order Full URL   | {{ order.full\_slug }}        | The unique slug of the order including Order Slug     |
| User ID          | {{ order.user\_id }}          | The unique ID of the Current User                     |
| User Email       | {{ order.email }}             | The email address of the User who completed the Order |
| Status           | {{ order.status }}            | The status of the Order                               |
| Billing Address  | {{ order.billing\_address }}  | Not yet available                                     |
| Shipping Address | {{ order.shipping\_address }} | Not yet available                                     |
| Payment Method   | {{ order.payment\_method }}   | Not yet available                                     |
| Shipping Method  | {{ order.shipping\_method }}  | Coming soon!                                          |
| Tracking Number  | {{ order.tracking\_number }}  | Not yet available                                     |
| Price            | {{ order.price }}             | The Price paid for the Order as a decimal             |
| Currency         | {{ order.currency }}          | The currency the Order was made in                    |

## 6) Add Orders layout to the Orders Page

Add the following liquid to your Orders page to output a list of the current logged-in User’s Orders:
```
{% raw %}
{%- include 'user_orders', layout: 'my_orders_list_layout', sort_type: 'id', sort_order: 'asc', show_pagination: 'false' %}
{% endraw %}
```

The layout parameter should take the name of the list layout you created.

## Other Ways to Use Secure Zones with eCommerce

You could add a Secure Zone to other pages related to your eCommerce flow, for example the Cart, in the same way you did with the Orders page. You could redirect the users to a login page when they visit the Cart page and are not logged in.

&#x20;Learn more about Secure Zones [here](/crm/quickstart-crm.md).
