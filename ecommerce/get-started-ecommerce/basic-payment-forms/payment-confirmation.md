---
title: Payment Confirmation Emails
slug: rZ6a-
createdAt: 2021-02-19T10:48:13.000Z
updatedAt: 2023-04-06T15:42:43.000Z
---

# 📋 Step-by-step Basic Payment Confirmations

Use Emails to send confirmation messages to customers, including a detailed breakdown of their Basic Payment Submission

## Prerequisites

* You have installed eCommerce Module v1.1.4 or later. Check out [Modules Overview](https://help.siteglide.com/article/131-modules-getting-started) to find out how you can install the latest version.
* You have set up a [Basic Payment Form](https://developers.siteglide.com/basic-payment-forms-tutorial) using the Stripe Payment Gateway

## Introduction

You can now add details of a customer's Basic Payment Form to Workflow and Autoresponder transactional emails. Give your Client and the customer peace of mind, as well as valuable records for their safekeeping. Within the email, you can also access any fields that were submitted along with the original Form. Learn more here: [Dynamic Content in Workflow and Autoresponder Emails](https://developers.siteglide.com/dynamic-content-in-workflow-and-autoresponder-emails)

## Step 1) Include the Payment Summary Feature

To include the details of the customer's most recent Order, include the following Liquid tag:

```liquid
{% raw %}
{% include 'ecommerce/payment_details', layout: 'default' %}
{% endraw %}


```

This can be outputted in one of two places:

* Inside the body of an [automation email](../../../cms/automations/dynamic-content-in-workflow-and-autoresponder-emails.md) e.g. autoresponder or workflow
* Inside a [Form Confirmation Layout](../../../cms/forms/guides-forms/form-confirmation-pages.md)

Placing in either of these locations will allow the system to identify the last submitted Form case and, if there is one, the associated payment.

## Step 2) Create or Find a Layout

### File Structure

You can use an existing Layout, or create a new one in this File Structure: `layouts/modules/module_14/payment/my_layout.liquid`

{% content-ref url="../basic-payment-forms-folder-structure.md" %}
[basic-payment-forms-folder-structure.md](../basic-payment-forms-folder-structure.md)
{% endcontent-ref %}

{% hint style="info" %}
**Note**

Unlike the similar Order Details Layout, Payment Details is simpler, so there are no wrapper and item files.
{% endhint %}

## Step 3) Develop the Layout

Inside your automation email body, you'll have access to the Form object: `{{form.properties}}` This contains the fields submitted with the Form. Learn more here: [Dynamic Content in Workflow and Autoresponder Emails](../../../cms/automations/dynamic-content-in-workflow-and-autoresponder-emails.md) You'll still have access to these fields throughout the Payment Details Layouts as they will be inherited.

\*\*\*Accessing Payment Details \*\*\*The layout file will have access to the `this` object, which will contain details about the Payment: `{{this}}` Within this object, you'll have access to the following fields:

| **Tag**                            | **Description**       | **Example Output** |
| ---------------------------------- | --------------------- | ------------------ |
| \{{this.currency\}}                | Currency code         | gbp                |
| \{{this.currency\_symbol \}}       | Currency symbol       | £                  |
| \{{this.amount\_paid\}}            | Amount Paid           | 100                |
| \{{this.amount\_paid\_formatted\}} | Amount Paid Formatted | 1.00               |
| \{{this.payment\_id\}}             | Stripe Payment ID     | pi\*               |
