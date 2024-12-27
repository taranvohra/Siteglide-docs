---
title: Basic Payment Forms - Tutorial
slug: XRsP-
createdAt: 2021-02-19T09:57:47.000Z
updatedAt: 2023-04-06T15:53:56.000Z
---

# 💡 About Basic Payment Forms

Basic Payments are a way to take a payment when a form is submitted. They may be useful for allowing Users to pay invoices etc.

## Prerequisites

* You have installed the eCommerce Module in Site Settings
* You have set up a [Payment Gateway](/eCommerce/get-started-ecommerce/payment-gateways/README.md)
* Using PayPal as a Payment Gateway? There are additional setup instructions [here](/eCommerce/get-started-ecommerce/payment-gateways/paypal-custom-params.md).

## Introduction

Basic Payments are a way to take a payment against a standard Form submission.

You set the currency, and the minimum payment value in Form Builder.

When submitting the form, a value is sent to our payment processor, and validated server-side to check that it's higher than the minimum payment value you have set.

Here's 3 examples of when you'd use this payment system:

1. If you're sending invoices to a customer, and want them to pay online, they can enter their invoice number (in a custom field) and the amount to pay. You would then check 'offline' that the value paid matches that on the invoice. In this case you'd set the minimum payment value as '0.00'.
2. You know the exact value you want the users to pay (for example $10.00), so you set the minimum payment value as '10.00'. This is validated server-side to make sure they cannot pay less than that.
3. You want to charge a variable amount based on their form selections, and know the minimum value that should be. For example, the charge might be $10.00 as standard, but then have some optional custom fields that bring the price up to $20.00. See the section below: "Changing the Price based on User Form Input".

### A note on Security

Remember, this kind of payment is designed for use cases where the customer intends to make a charitable donation or pay an invoice that is due. It is possible for the customer to modify the JavaScript and pay less (but not less than the minimum payment value). You should only use this kind of payment either when the customer does have a genuine choice, or the Client will be reconciling invoices and chasing where the correct amount has not been paid.
