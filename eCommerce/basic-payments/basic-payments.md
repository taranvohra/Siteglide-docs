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
* You have set up a [Payment Gateway](https://help.siteglide.com/article/161-ecommerce-subscriptions-setting-up-your-payment-gateway-and-settings)
* Using PayPal as a Payment Gateway? There are additional setup instructions [here](https://help.siteglide.com/article/165-payment-gateways).

## Introduction

Basic Payments are a way to take a payment against a standard Form submission.

You set the currency, and the minimum payment value in Form Builder.

When submitting the form, a value is sent to our payment processor, and validated server-side to check that it's higher than the minimum payment value you have set.

Here's 3 examples of when you'd use this payment system:

1. If you're sending invoices to a customer, and want them to pay online, they can enter their invoice number (in a custom field) and the amount to pay. You would then check 'offline' that the value paid matches that on the invoice. In this case you'd set the minimum payment value as '0.00'.
2. You know the exact value you want the users to pay (for example $10.00), so you set the minimum payment value as '10.00'. This is validated server-side to make sure they cannot pay less than that.
3. You want to charge a variable amount based on their form selections, and know the minimum value that should be. For example, the charge might be $10.00 as standard, but then have some optional custom fields that bring the price up to $20.00. See the section below: "Changing the Price based on User Form Input".

## Setting up a Basic Payment Form with a fixed payment amount

The following steps are for setting up a Basic Payment Form which will accept a fixed payment amount e.g. all customers submitting the Form will pay the same.

The same steps should also be followed if you intend the amount paid to be decided based on the User's interaction with the Form- but there will be additional steps described below.

### Step 1 - Payment Gateways

Basic Payment is available using the following Payment Gateways:

* [Stripe](https://stripe.com/)
* [PayPal](https://www.paypal.com/)
* [Authorize.net](https://www.authorize.net/)

Note: depending on the Payment Gateway, some specific fields may be needed in order to capture the necessary payment details. Those fields will be specified in step 5.

### Step 2 - (Optional) Secure Zones

In order to use Secure Zones in this process, they first need to be set up. For instructions on how to use Secure Zones on a Form, [click here](https://help.siteglide.com/article/99-forms-getting-started#2-adding-secure-zones).

If you apply a Secure Zone to the Form, then the user will be given access after a successful payment.

### Step 3 - Create a Form

When creating a Form, navigate to the 'Payments' tab.

Here you should enter the following data:

* Use as a payment form? - Toggle to 'true'
* Payment form type - Basic Payment Form
* Currency - Choose from the dropdown of supported currencies
* Minimum payment value - The minimum amount a user can pay to submit this Form

For further instructions on how to set up Forms, [click here](https://help.siteglide.com/article/99-forms-getting-started#2-creating-and-editing-forms).

### Step 4 - (Optional) Editing your Form layout to apply Payment Gateway specific code

Please see below for code relevant to your Payment Gateway.

**Stripe** There is no extra code required for Stripe.

[Authorize.net](http://authorize.net) You must include 3 extra fields for [Authorize.net](http://authorize.net) to work.

| **Field Name** | **Example**                                                                        | **Notes**                                                          |
| -------------- | ---------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| Card Number    | \<input id="s\_e\_card\_num" class="required" type="text" />                       |                                                                    |
| Card Expiry    | \<input id="s\_e\_card\_exp" class="required" type="text" placeholder="MM-YYYY" /> | The data format must follow that in the placeholder in our example |
| Card CVV       | \<input id="s\_e\_card\_cvv" class="required" type="text" />                       |                                                                    |

### Step 5 - Testing

To test your new Basic Payment Form, you first must put it on a Page. You can do so using Toolbox's 'Insert Form' feature.

Once you have created a Page and navigated to it, you will need to fill in the fields and submit.

If your Payment Gateway is in 'Test Mode', then you may need to enter card details specific to the testing environment. You can find those under 'Test Cards' on our [Payment Gateways documentation page](https://help.siteglide.com/article/165-payment-gateways).

## Changing the Amount to be Paid based on the User's Form Input

![](https://downloads.intercomcdn.com/i/o/235432449/908d4f34110742c41cef6d88/image.png)

In some use-cases you may wish the amount to be paid to depend on the User's input into the Form Fields e.g.

* The User is making charitable donations. The minimum payment is $2, but they can choose to donate any amount above that they wish.
* The User will select options on the Form that will inform a logical function to decide how much they need to pay.

Both use-cases will require you to write a JavaScript function which will update the value of the amount due.

### Using Liquid to Fetch the Currency and Minimum Amount from Admin

You may find the following Liquid tags helpful while developing:

| **Liquid** | **Role**                                                                                  | **Example** |
| ---------- | ----------------------------------------------------------------------------------------- | ----------- |
|            | The currency for the Form defined in Admin                                                | gbp         |
|            | The symbol for the currency for the Form defined in Admin                                 | £           |
|            | The `minimum payment` value defined in Admin, in the lowest denomination of that currency | 100         |
|            | The `minimum payment` value defined in Admin, formatted                                   | 1.00        |

### Writing the function

The end goal of such a JavaScript function will be to set the value of hidden field with the ID "s\_e\_amount". The default value of this field will be the same as the minimum payment value you set in Admin, until it is changed via JavaScript. The final value should be an integer (whole number) of the number of cents that will be paid.

We'll give you an example of how this JavaScript may work here. You can adapt this example to suit your use case. The important thing is that you set the value of the field with the ID "s\_e\_amount".

### Example - Allowing the User to enter any value they wish

The following example allows the User to enter an amount of their choice into an input in the Form. Our function changes the format, then sets the value of the hidden field. Note that the entire example should sit inside a Liquid

tag.

```liquid
<div class="row mt-4">

  <div class="col">

    <label for="user_chooses_amount_to_pay">
      How much can you afford to donate (pounds and pence e.g. 10.00)?</label>

    <div style="display: flex; align-items: center;">

      <span style="margin-right: 5px;">{{context.exports.currency_map.data['GBP']}}</span>

      <input class="form-control" 
             id="user_chooses_amount_to_pay" 
             type="text" 
             placeholder="10.00">

    </div>

    <script>

      function changeAmountToPay() {

          var output = document.querySelector('#s_e_amount');

        output.value = parseInt(event.target.value * 100); 
        //As the end result must be in cents / pennies, we multiply the given value by 100 and make sure it is an integer. 

      }

      var input = document.querySelector('#user_chooses_amount_to_pay');

      input.addEventListener('keyup', changeAmountToPay); 
    </script>

  </div>

</div>
```

### Example - Using URL parameters to change the value of s\_e\_amount

This example shows how you can add an "amount" parameter to the URL- if this parameter exists then the `s_e_amount` will be updated.

The following Javascript can be added to your Basic Payment Form's Layout. The first half of the function will store the amount parameter within the "amount" variable, the second half checks if "amount" exists (this prevents "null" from getting added to `s_e_amount`) if so then `s_e_amount` is updated with the new price:

```javascript
window.addEventListener('DOMContentLoaded', (event) => {

    //fetch amount param from the URL
      const urlParams = new URLSearchParams(window.location.search);
      const amount = urlParams.get('amount');
      
    //set s_e_amount value to amount from url param
      if(amount) { document.querySelector('#s_e_amount').value = amount; };

  });
```

### A note on Security

Remember, this kind of payment is designed for use cases where the customer intends to make a charitable donation or pay an invoice that is due. It is possible for the customer to modify the JavaScript and pay less (but not less than the minimum payment value). You should only use this kind of payment either when the customer does have a genuine choice, or the Client will be reconciling invoices and chasing where the correct amount has not been paid.

## Related Articles

Basic payment forms are just one of the ways that Siteglide eCommerce can take payments from customers. You can also use:

* [Checkout](https://developers.siteglide.com/cart-checkout-and-orders-flow-with-secure-zones-module-tutorial)
* [Subscriptions](https://help.siteglide.com/article/184-ecommerce-subscriptions-introduction)
