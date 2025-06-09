# Changing Price and Billing Interval

## Introduction

Most database items in the Siteglide database can be safely edited without affecting existing customers. For example, you can change the price of a physical product and everyone would expect to pay the new price for the product in future.

For Subscriptions, we've set it up so that Price changes on a Subscription will not affect existing subscribers. Instead only new subscribers will have to pay the new price.

Currently, we don't support allowing customers to choose their Plan when signing up to a Subscription. Instead, only the most recently created Plan will be available for new customers. We may add this functionality in the future, but for now, we suggest creating separate Subscription items with different periods and chargeable prices if you want to give customers different payment options for the same services.

## Glossary

* Subscription (on Siteglide) - equivalent to a Product on the Stripe Dashboard - This is a Subscription Product which can be connected to a Plan. Plan (on Siteglide) - equivalent to a Plan on the Stripe Dashboard. This defines the price charged and the interval between charges.
* Subscription Order (on Siteglide) - equivalent to a Subscription on the Stripe Dashboard - This is a record of the order a customer has made to subscribe to a Subscription. It holds a record of the Plan and Pricing that the customer originally signed up for. It also has a status, which keeps track of whether this Subscription Order is "Active". Creating a New Plan Changing the Price of a Subscription will Create a new Plan There are three main variables that will affect the amount users will pay for a Subscription:
* Chargeable Price
* Interval
* Interval Count Changing the "chargeable price" will create a new Subscription Plan on Stripe and make this the default Plan for new customers.

Changing the Interval or Interval Count will not trigger an API call to Stripe to create a new Plan on its own.

If you want the new Plan to have a new Interval you should follow the following steps:

1. Change the Interval and/or Interval Count on Siteglide
2. Save the Chargeable Price in the prices tab on Siteglide. This will create a new Plan which will include the new values for Interval and Interval Count. (Changing the price before saving is optional- all that's needed to create the new Plan is to "save" the prices tab- you can leave it the same if you wish).

## How a new Plan affects existing customers

Existing customers will not be affected by the new Plan. Their Subscription Order will be connected to the original Plan they signed up to.

## How a new Plan affects new customers

New customers will not be shown information about the old Plan. They will sign up to the newest Plan only.
