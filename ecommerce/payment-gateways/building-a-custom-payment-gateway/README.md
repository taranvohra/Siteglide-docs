---
title: Building a Custom Payment Gateway
slug: dSVA-
createdAt: 2021-01-07T15:48:52.000Z
updatedAt: 2023-03-03T08:08:57.000Z
---

# 💻 Building a Custom Payment Gateway

## Prerequisites

* Good understanding of Liquid
* Good understanding of JavaScript
* Good understanding of GraphQL, including queries, related\_models, mutations and using mutations to send API calls.
* Good understanding of APIs

## Introduction

Siteglide have built integrations between its eCommerce Module and three Payment Gateways:

* Stripe - integrated with all Siteglide eCommerce Features
* PayPal - for Checkout and Basic Payment Forms
* Authorize.net - for Basic Payment Forms

In order to focus on improving features for the Payment Gateways we have, we won't be building integrations to any other Payment Gateways at this point. Instead, this Article is intended to help experienced Siteglide Partners build their own Payment Gateway Integrations.

***

## Payment Gateway Configuration

We've opened up the Payment Gateway model (model\_schema\_name: "module\_14/payment\_gateway") to allow you to customize it to suit your own Payment Gateway:

| **Field Name**                      | **Field ID**                           | **Purpose/Notes**                                                                                     |
| ----------------------------------- | -------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| Name                                | module\_field\_14/payment\_gateway\_1  | Payment Gateway Display Name                                                                          |
| Active                              | module\_field\_14/payment\_gateway\_2  | Boolean Only one Payment Gateway should be active at a time.                                          |
| Type                                | module\_field\_14/payment\_gateway\_5  | Payment Gateway Name in snake\_case - Must be unique to your Payment Gateway                          |
| In test mode?                       | module\_field\_14/payment\_gateway\_8  | Boolean                                                                                               |
| Custom Payment Gateway Partial Path | module\_field\_14/payment\_gateway\_19 | Folder path for the partials you will use to include your Gateway code on the Form (see next section) |

Use GraphQL to create a record in this table using the filelds above.

## Next Steps

Now your Payment Gateway exists, it's time to give it some functionality. You can add support for one or more of the following:

<table data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td></td><td><a data-mention href="steps-to-support-checkout-with-your-custom-payment-gateway.md">steps-to-support-checkout-with-your-custom-payment-gateway.md</a></td><td></td></tr><tr><td></td><td></td><td><a data-mention href="steps-to-support-basic-payment-forms-with-your-custom-payment-gateway.md">steps-to-support-basic-payment-forms-with-your-custom-payment-gateway.md</a></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>
