# Creating a Form for Signing Up and changing Payment Details

## Introduction

In this article, we'll look at how you can set up a Form which will:

- Allow Users to Sign Up for a Subscription
- Allow Users to change the payment method Stripe will be charging for an existing Active Subscription, or a Subscription which is "past_due" and requires a change in payment method.
- Allow users to authorise an existing payment method using 3D secure.
- Re-activate a Subscription that is no longer Active- this may include any Subscription with either the "incomplete" or "unpaid" status.

In a standard Subscriptions flow, all these use-cases are handled by a single Form so that we can identify the User, their current Subscriptions and work out the most appropriate course of action.

You'll also be able to use the same form for any Subscription Product. You can set which Subscription Product the Form will sign users up to, by outputting the Form on that Subscription's Detail Page.

## Creating the Form

Firstly, navigate to CMS > Forms and select the "Add New Form" button:

![Image](/.gitbook/assets/Siteglide-Subscriptions-Creating-a-Form-Payment-Details-1.png)

Add details to the Form as you normally would. (To recap standard Form creation in Siteglide - [see here](/cms/forms/quickstart-forms.md).)

When setting the name, remember this can be a Form for all Subscriptions, so you don't need to name it after a product.

## Setting the Form as a Payment Form

Next, in the payments tab, toggle Payments on and select Subscription from the Payment form type options.

![Image](/.gitbook/assets/Siteglide-Subscriptions-Creating-a-Form-Payment-Details-2.png)

## Adding Secure Zones

It's important that all Users who sign up to Subscriptions have an account with an email and password on Siteglide. This will allow them to manage their Subscriptions.

[Learn more about creating Secure Zones](/modules/core-modules/secure-zones/quickstart-secure-zones.md)

The easiest way to do this is to set a Secure Zone to this Subscription Form to serve as the User's account - it will make sure that User's are given the chance to sign up for an account - or log in - at the same time as they sign up for the Subscription and enter payment details.

You can do this by adding any Secure Zone to the Form in the Secure Zones tab:

![Image](/.gitbook/assets/Siteglide-Subscriptions-Creating-a-Form-Payment-Details-3.png)

If you already have a Secure Zone which serves this purpose on your Site, you can of course use it here. We'd recommend not using a Secure Zone directly associated with a Subscription, as this could be removed from a User if they cancel their Subscription.

## Outputting the Form

In order to use the Form, it must be outputted inside a Subscription Detail Layout. This defines which Subscription the Form will sign customers up for.

There are two main places where this will need to be as a minimum:

- The Page where you want Users to sign up to the Subscription. Most commonly this will be the Subscription's Detail Page.
- The System Page where Users will be sent via email if a payment method needs updating or authorising. We'll include the Detail View for the correct Subscription automatically, but you may select the Detail Layout used.

### Outputting the Form inside a Detail Layout

You can include the Form by adding the standard Liquid for including a Form:

`{% raw %}{% include 'form', id: '10', layout: 'default' %}{% endraw %}`

You'll need to use the ID of your Subscription Form which you'll be able to find in the Admin.

### Outputting the Form on the Subscription System Page

We'll output a Detail View on the System Page for you, you'll just need to select a Subscription Detail Layout of your choice where Form has already been included as above.

We'll explain in more detail here: Editing the ["Subscription User Action Required" System Page and Email](/eCommerce/get-started-ecommerce/subscriptions/subscription-action-required.md)

