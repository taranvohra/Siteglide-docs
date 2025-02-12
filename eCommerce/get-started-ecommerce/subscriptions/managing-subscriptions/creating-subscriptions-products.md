# Creating Subscription Products

## Prerequisites

- Before you add Subscription Products, make sure you follow the steps [in this article](/eCommerce/go-further-ecommerce/subscriptions/setting-up.md) to set up the integration between your Stripe account and your Siteglide Site.
- You will need to have installed the Secure Zones Module on your Site, as this is required by Subscriptions.

## Introduction

Now you've set up your Payment Gateway, this article will explain how you can add Subscription products using the Siteglide Admin.

We'll also explain how you can set prices for these products and define which Secure Zones a customer will gain access to while they have an active Subscription to each Product.

We'll be adding additional features in later releases which will expand your options in future.

## Adding Products

You can view a list of existing Subscription products and add new ones under `ECOMMERCE > Subscriptions`

![](/.gitbook/assets/Siteglide-Subscriptions-Creating-Subscription-Products-1.png)

### Step 1 - Add Details

Add all the information you need to about the Subscription product, add SEO metadata and assign to Categories if you wish.

### Step 2 - Set the Interval

Here you need to define the length of time each billing cycle will last.

You need to choose:

- An interval unit from the available options
- An integer for the number of days / weeks / months

In future we plan to add additional options here. However, if you need to have alternate payment plans for the same Product now, we recommend you create multiple Subscription items each with the same details, but with different intervals and prices.

### Step 3 - Save

Saving at this point will send an API Call to Stripe to create the product in Test and Live mode. Once created, it will be possible to add additional options and further tabs will appear.

### Step 4 - Pricing

Pricing works in a similar way to other eCommerce Products.

You currently must choose the same currency as your Site currency.

The chargeable price is the price your customers will pay each interval.

The display-only price is available if you need to display the price without sales tax, a recommended retail price- etc.

![](/.gitbook/assets/Siteglide-Subscriptions-Creating-Subscription-Products-2.png)

### Step 5 - Secure Zones

If you would like to use your Site to deliver content or services to customers who sign up to a Subscription, you can do this with Secure Zones.

In the Secure Zones tab, select the Secure Zones that you'd like to assign to customers while they have an active Subscription.

The same list of Secure Zones will also be taken away from the User when their Subscription is cancelled, so we recommend that you don't include a generic "Account" Secure Zone here, or your Users may also lose this when their subscription ends.

If you would like to learn more about creating and using Secure Zones, [see here](/modules/core-modules/secure-zones/quickstart-secure-zones.md).


### Using your Stripe Account

You'll notice Stripe gives you the option to add additional Products in the Stripe Dashboard. We'd recommend for now that you create Subscription Products within the Siteglide Admin- as this will mean we only provide options to add features that are fully supported by the integration.