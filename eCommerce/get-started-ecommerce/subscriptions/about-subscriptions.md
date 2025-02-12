# 💡 About Subscriptions

## Prerequisites

- Each Site owning organisation (Agency or Client) will need their own activated Stripe account
- Your eCommerce Module should be at least version 1.0.0
- Your Secure Zones Module should be at least version 0.10.0

## Upgrading

If you were using the Beta version of eCommerce Subscriptions (versions 0.14.1 and lower) and you have not yet upgraded your eCommerce Module, your Sites will continue to work as normal.

However, after upgrading to the eCommerce Module 1.0.0, Stripe webhooks must be set up. You can follow steps [3 + 4](/eCommerce/go-further-ecommerce/subscriptions/setting-up.md#step-3-set-up-the-webhook-endpoints-in-your-stripe-account) here to do this.

## Introduction

Our integration with Stripe Billing allows you to create Subscription Products and bill customers on a regular basis.

In this overview Article, we'll list the available features and link you to more documentation and articles.

## Overview of Subscription Documentation

- [Setting up your Payment Gateway for Subscriptions](/eCommerce/go-further-ecommerce/subscriptions/setting-up.md)
- [Creating Subscriptions Products](/eCommerce/get-started-ecommerce/subscriptions/managing-subscriptions/creating-subscriptions-products.md)
- [Changing the Price and Billing Interval](/eCommerce/get-started-ecommerce/subscriptions/managing-subscriptions/changing-price-and-billing-interval.md)
- [Creating a Form for Signing Up and changing Payment Details](/eCommerce/get-started-ecommerce/subscriptions/managing-subscriptions/creating-a-form-for-signing-up-and-changing-payment-details.md)
- [The Subscription Detail Layout](/eCommerce/get-started-ecommerce/subscriptions/subscriptions-detail.md)
- [Subscriptions List View](/eCommerce/get-started-ecommerce/subscriptions/subscriptions-list.md)
- [User Subscriptions - List the logged in User's Subscription Orders](/eCommerce/get-started-ecommerce/subscriptions/user-subscriptions.md#outputting-the-user_subscriptions-list)
- [eCommerce Subscriptions - Editing the "Subscription User Action Required" System Page and Email](/eCommerce/get-started-ecommerce/subscriptions/subscription-action-required.md)
- [Cancelling Subscriptions](/eCommerce/get-started-ecommerce/subscriptions/cancelling-subscriptions.md)
- [Subscription Order Status Explained](/eCommerce/get-started-ecommerce/subscriptions/managing-subscriptions/subscription-order-status-explained.md)
- [Terms and Conditions (Good Practice)](/eCommerce/get-started-ecommerce/subscriptions/managing-subscriptions/terms-and-conditions-good-practice.md)

## eCommerce Subscriptions Features

Our integration with Stripe Billing allows you to:

- Create Subscription Products and assign a single recurring price to each
- Display a List View of available Subscription Products
- Display a Detail Page of Details on a particular Subscription Product, which can also include a Form which allows customers to Sign Up to the Subscription.
- Store customers' card details securely on Stripe. As with the rest of our Payment Gateway integration with Stripe, we use Stripe Elements so that card details never touch our servers.
- Allow Stripe to make automated attempts to charge customers on a recurring basis
- Handle 3D Secure Authorisation requests from the customer's bank (meeting Strong Customer Authentication regulations) in two ways: either directly on the payment form itself, or if this is required on a recurring payment, the customer will receive an email sending them back to site where they can re-authorise the payment.
- Handle payment failures of all kinds on initial or recurring payments. On recurring payments the customer will receive an email sending them back to the site where they can enter and verify a new payment method.
- When payments are not made, Stripe will make automated attempts to retry. Once it has exhausted these attempts, you can decide what it does next using your Stripe dashboard settings.

## Features using eCommerce Subscriptions and Secure Zones

The Subscriptions feature now requires that you also install the Secure Zones Module.

A Subscriptions customer must be logged into at least one Secure Zone (for example this could be called "My Account") so that we are able to identify them when they wish to manage their Subscriptions.

Along with the Secure Zones module, you can also:

- Sign a User up to one or more Secure Zones when they sign up to a Subscription. These could for example, allow access to the content or services that the User has signed up for.
- If the Subscription is marked as "past_due", the Secure Zones will not immediately be removed- this is to give the customer time to update their payment details. If no payment is made, Stripe will change the status again.
- Remove the User from one or more Secure Zones when Stripe marks the Subscription Status as "incomplete_expired", "unpaid" or "cancelled"
- Return Users to Secure Zones when a new payment method is added and a Subscription is renewed.
