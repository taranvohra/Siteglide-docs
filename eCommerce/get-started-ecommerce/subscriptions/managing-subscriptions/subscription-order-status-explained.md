# Subscription Order Status Explained

## Introduction

Subscription Orders in Siteglide represent an individual User's Subscription to a specific Product. Their status is explained here.

You can use it to track which Subscription Orders need action from the User and which are Active and generating income.

## Subscription Order Status

Available statuses in Siteglide are:

- Incomplete - It was not possible to pay the first invoice on a new Subscription. Access to Secure Zones will not be granted.
- Active - A Subscription is active and Stripe was able to successful pay the latest invoice. Access to Secure Zones will be granted.
- Past Due - It was not possible to pay the most recent invoice on a new Subscription. As a Subscription Order enters this status, Siteglide will send a System Email notification to the User telling them what they can do to return the Subscription Order to Active. We won't remove access to Secure Zones at this stage. Access to Secure Zones will not be removed yet, but it will be if the status changes to `Cancelled` or `Unpaid`.
- Unpaid - Stripe has decided not to continue attempts to pay the latest invoice. Your Stripe Dashboard settings allowed this Subscription Order to remain in the database in case a renewal is still possible. Access to Secure Zones will be removed.

The following statuses will cause the Subscription Order to be deleted on Siteglide and the Subscription to be deleted on Stripe, so will never be seen here. Read more about Subscription Statuses and what you can do to control what Stripe does with persistently unpaid Subscriptions [here](/eCommerce/go-further-ecommerce/subscriptions/setting-up.md).

- Incomplete Expired - Stripe has decided not to continue attempts to pay the first invoice. We deleted the Subscription Order from the Database to save space. Other options may be available in future. Access to Secure Zones will be removed.
- Cancelled - Stripe has decided not to continue attempts to pay the latest invoice. Your Stripe Dashboard settings caused this Subscription Order to be deleted from the database to save space. Access to Secure Zones will be removed.
