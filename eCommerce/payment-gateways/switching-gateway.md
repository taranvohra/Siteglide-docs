---
title: Switching Between Multiple Payment Method Options
slug: 3861-multiple-payment-method-options
createdAt: 2021-11-02T14:26:21.000Z
updatedAt: 2024-01-29T12:23:57.692Z
---

# Steps

## Step 1

Use the [ecommerce/checkout\_standard](docId\:WdXVXmm5wUE2tzGD5Px-5) include to output multiple payment gateways inside your checkout form Liquid layout file.&#x20;

## Step 2

Once you have multiple options, you'll need a way to tell the system which to use.&#x20;

The following JS function will do that for you:

```javascript
s_e_set_payment_gateway('Stripe');

s_e_set_payment_gateway('PayPal');
```

Pass in the name of the Payment Gateway you wish to switch to as the only argument.&#x20;

This can be applied to any action you like, such as clicking a radio button, or opening an accordion. e.g.

:::codeblocktabs
```html
<input type="radio" name="paymentGateway" id="paymentGateway1" value="Stripe"><label for="paymentGateway1">Pay with Stripe</label>
<input type="radio" name="paymentGateway" id="paymentGateway2" value="PayPal"><label for="paymentGateway2">Pay with PayPal</label>
```

```javascript
const paymentGatewayCheckboxes = document.querySelectorAll('[name="paymentGateway"]');
paymentGatewayCheckboxes.forEach(function(item) {
  item.addEventListener('change', function(e) {
    const radio = e.currentTarget;
    s_e_set_payment_gateway(radio.value);
  });
})
```
:::

If the JS function is not called, the default payment gateway from the multiple available gteways will be used.








