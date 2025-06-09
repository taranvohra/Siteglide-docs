# Minimum Payments

## Introduction

Discount Codes can cause the payment total due to be smaller than your Client may wish- or even 0.

When accepting payments, most Clients won't want to handle very small payments e.g. less then 50 cents.

## Why are small charges a problem?

Stripe's payment gateway will, in fact, refuse to process payments smaller than its minimum payment amounts, which will lead to bad User Experience as Payments will fail.

PayPal will accept these small payments, but will charge the Client potentially more than they make on the transaction.

## The solution for Basic Payment Forms and Checkout

This Article will explain the two main solutions to these small charges:

* Recommended - The Agency and Client can set Minimum Spend against each discount Code
* Fallback - While applying discounts, Siteglide rounds payments up to an absolute minimum the Payment Gateway will accept.

In the future, we plan to change the flow so that Siteglide will accept 100% discounts in the Checkout by skipping the Payment step. For now- we'll recommend alternatives if you need this functionality.

## Avoiding Small Charges

In the following section, we'll refer to the "minimum desired spend". By this, we mean either:

* The lowest value order your Client is willing to accept (bearing in mind they still need to pay the charges due to the Payment Gateway on this Order).
* If using Stripe, this will be at least 50 of your currency's lowest denomination e.g. cents
* If using PayPal, this will be at least 1 of your currency's lowest denomination e.g. cents.

## Setting the Minimum Spend as the Agency or Client

The main method the Agency and Client have at their disposal to prevent this is the Minimum Spend field when creating or editing their Discount Codes.

This field should be set up to make sure that if it's value has the discount applied, the total price due would still exceed the minimum desired spend.

E.g.

For percentage discounts - you should check that if the percentage discount is applied to the value in "minimum spend" it won't leave a total which is lower than the minimum desired spend:

e.g. In this example, let's assume it's only economically viable for the Client to accept spends of 50 cents or more- this is their "Desired Minimum Spend" (your Client's may well be different!).

In the screenshot below- even with a 90% discount, the minimum spend is high enough to avoid excessively small charges:

$5.00 multiplied by 90 divided by 100 is a saving of $4.50.

$5 dollars with a $4.50 dollar discount leaves a remaining payment due of $0.50.

For value discounts the calculation is simpler - "Minimum spend" minus "value" should be greater than minimum desired spend.

E.g. For a $9.50 discount, you need a "Minimum Spend" of $10 to prevent discounts from allowing a spend below $0.50.

As explained below, Siteglide will take its own steps to avoid very small charges, but using the Minimum Spend field is the easiest way to make these limits clear to Users, improving their experience. It also allows the Client to decide if their minimum desired spend is greater than the Payment Gateway's value.

How Siteglide Handles Small Charges on Basic Payment Forms and Checkout While applying discounts, Siteglide will automatically check if the total price due is below the absolute minimum needed for the Payment Gateway to accept the Payment.

If this is the case, Siteglide will automatically adjust the total price due to:

For Stripe, 50 of your currency's lowest denomination e.g. cents For PayPal, 1 of your currency's lowest denomination e.g. cents This will display on the Cart, and be the total amount actually charged to the User's Card.

## Informing Users

Again, setting a reasonable Minimum Spend is the preferable solution to this issue, but in the case that Siteglide does need to fall-back and round charges up to the minimum payment, you can inform the Users of this with a message.

This code can be used inside your Discount Code Layout:

```liquid
{% raw %}
{%- if discount_saving_maximum_reached == true -%}<!-- Message here --><p>Minimum total price reached. Unfortunately we cannot accept payments below this price. To make the most of your discount, try adding another item to your cart.{%- endif -%}
{% endraw %}
```

## Subscriptions

Stripe Subscriptions handle this problem differently. The variable discount\_saving\_maximum\_reached will always return false for Subscriptions discounts, as we will never manually cap the amount of Discount for these kinds of payment.

Firstly, Subscriptions allow you to give 100% discounts- this effectively creates one form of "free trial".

Secondly, if Stripe judge a Subscription invoice to be for an un-economically small sum, they will carry that charge over to the next invoice. In the same way, if the discount gives a greater reduction in cost than the spend, the customer will receive credit in the Stripe account, which will be carried over into the next invoice. If you do not wish for this behaviour, see Setting Minimum Spend above!

## What if I actually want to apply 100% discounts on Basic Payment Forms and Checkout?

Currently, it is not possible to offer 100% discounts on Checkout using Stripe or PayPal.

In the future, we intend to better support 100% discounted Orders by completing the Order without carrying out a Payment, however, we expect values between 0 and the Payment Gateway's minimum to continue to be rounded up.

The following alternative Form types do currently allow Users to complete them with Payments of 0:

Our Quote Only feature for these customers- as this does allow Orders to be created without any charges being made- meaning the Client will not be charged. Our Basic Payment Form with Stripe will already skip payment if the amount due is exactly zero and the Minimum payment value field attached to the Form in Admin is also 0.
