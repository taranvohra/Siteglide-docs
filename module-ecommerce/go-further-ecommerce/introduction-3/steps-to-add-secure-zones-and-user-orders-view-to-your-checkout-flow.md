# 📋 Steps to Add Secure Zones and User Orders View to your Checkout Flow

## Pre-Requisites

* You have read [How to Set Up a Shopping Cart and Guest Checkout](../../get-started-ecommerce/cart-checkout-and-quotes/steps-to-implement-a-guest-checkout-flow.md)
* You have Installed the eCommerce Module
* You have installed the Secure Zones Module

## Introduction

Siteglide eCommerce is even more powerful with Secure Zones. With the security of a Secure Zone, you can show your Users more sensitive data about their shopping experience.

## Step 1) Create a Secure Zone

Create a Secure Zone which will used by shoppers on your eCommerce site.

Alternatively, you can use a Secure Zone that you have created already.

Find out more about the Secure Zones Module here:

{% content-ref url="../../../module-secure-zones/get-started-secure-zones/introduction.md" %}
[introduction.md](../../../module-secure-zones/get-started-secure-zones/introduction.md)
{% endcontent-ref %}

## Step 2) Create a "My Orders" Page in a Secure Zone

Create a new page which will display a list of Products Users have ordered.

{% hint style="info" %}
Make a note of the Page slug, because you will want to add this to the Checkout Form’s "Redirect URL" field later.
{% endhint %}

In CMS / Pages, open the Page you have chosen and open the Details tab. Click the Secure Zones accordion to reveal the "Select a Secure Zone" field.

<figure><img src="../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

Click in this to open a drop-down list of your Secure Zones and select the one you wish to be accessed by Users after they complete Checkout.

## Step 3) Set the Checkout Form Redirect to your Orders Page

Make sure your Checkout Form is still in "Test Mode" unless the Site is Live.

The [previous article](../../get-started-ecommerce/cart-checkout-and-quotes/steps-to-implement-a-guest-checkout-flow.md) explained how to create a Checkout Form. Here we will modify this form so that it also either signs in a User or logs them in, depending on their current status.

Find Forms in the Siteglide Admin’s left-hand side menu under CMS / Forms. Select your checkout Form in the list:

<figure><img src="../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Next, click the "View Form" button to edit:

<figure><img src="../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

In the "Redirect URL" field add your Orders [Page slug](steps-to-add-secure-zones-and-user-orders-view-to-your-checkout-flow.md#step-2-create-a-my-orders-page-in-a-secure-zone), preceded by a forward slash. E.g. /my-orders

## Step 4) Add the Secure Zone to the Checkout Form

Select the Secure Zones tag and then click in the Secure Zones Input field to see a dropdown of Secure Zones you have already created.

<figure><img src="../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

Select the Secure Zone you want to log your Users in to when they complete the form.

Press the "Save" Button to save your changes. At this point:

Completing the Checkout Form will log Users in to the Secure Zone It will also redirect the Users to the My Orders Page The Users will be allowed to access the My Orders Page, because they are logged into the Secure Zone. Other Users who are not logged in will be unable to access the My Orders Page.

## Step 5) Create an Orders List Layout

As Orders List Layouts are for showing secure information about Users, they are stored under the following file structure:

`module_5/user_orders/name_of_my_layout.liquid`

{% content-ref url="../../reference-ecommerce/cart-and-checkout-folder-structure.md" %}
[cart-and-checkout-folder-structure.md](../../reference-ecommerce/cart-and-checkout-folder-structure.md)
{% endcontent-ref %}

Create a new file in the user\_orders folder and give it a name of your choice. Make a note of the name you gave it.

{% hint style="success" %}
[SiteBuilder](../../../module-sitebuilder/get-started-sitebuilder/about-sitebuilder.md) has an out-of-the-box Orders List design ready for you in a Bootstrap 5 or Tailwind version.\
![](<../../../.gitbook/assets/image (14).png>)
{% endhint %}

## Step 6) Add Orders layout to the Orders Page

Add the following liquid to your Orders page to output a list of the current logged-in User’s Orders:

```
{% raw %}
{%- include 'user_orders', layout: 'name_of_my_layout', sort_type: 'id', sort_order: 'asc', show_pagination: 'false' %}
{% endraw %}

```

The layout parameter should take the name of the list layout you created.

## Step 7) Develop your Layout

Your layout will have access to the "orders" object. You can loop over each order in the "Order" object with the following liquid (the "order" variable can be renamed to anything you like). For example:

```
{% raw %}
{% for order in orders %}
  <!-- {{order.id}} etc. -->
{% endfor %}
{% endraw %}


```

See the orders reference for available fields:

{% content-ref url="orders/orders-reference.md" %}
[orders-reference.md](orders/orders-reference.md)
{% endcontent-ref %}

## Next Steps

You could add a Secure Zone to other pages related to your eCommerce flow, for example the Cart, in the same way you did with the Orders page. You could redirect the users to a login page when they visit the Cart page and are not logged in.

Learn more about Secure Zones here.
