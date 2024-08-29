---
title: Switching Between Multiple Payment Method Options
slug: 3861-multiple-payment-method-options
createdAt: 2021-11-02T14:26:21.000Z
updatedAt: 2024-01-29T12:23:57.692Z
---

# 📋 Steps to Switching Payment Gateway

## Step 1 - Create a Payment Form

Create a Form in the Siteglide Admin and turn on the setting to use it as a payment form. (Basic Payment Form and Checkout will be supported as both support at least 2 payment gateways.)

## Step 2 - Create a Custom Form Layout

{% hint style="info" %}
:genie:You can use [SiteBuilder](../../../sitebuilder/setup-sitebuilder/layouts/about-layouts/static-and-dynamic-form-layouts.md) to quickly create a custom Form Layout
{% endhint %}

In Code Editor or CLI, make a copy of the default form layout, ready to customise it.

In any Page, output your form and select the custom layout with the layout parameter. E.g. if your form ID is `1`, your layout should be at `marketplace_builder/views/partials/layouts/forms/form_1/`my-custom-layout`.liquid`

```liquid
{% raw %}
{%- include 'ecommerce/checkout', form_id: '1', layout: 'my-custom-layout' -%}
{% endraw %}


```

For Basic Payment forms:

```liquid
{% raw %}
{% include 'form', id: '2', layout: 'my-custom-layout' %}
{% endraw %}


```

## Step 3

For Checkout Forms, use the ecommerce/checkout\_standard include to output multiple payment gateways inside your checkout form Liquid layout file.

```liquid






 
```

For Basic Payment Forms:

```liquid






 
```

## Step 4

Once you have multiple options, you'll need a way to tell the system which to use.

The following JS function will do that for you:

```javascript
s_e_set_payment_gateway('Stripe');

s_e_set_payment_gateway('PayPal');
```

Pass in the name of the Payment Gateway you wish to switch to as the only argument.

This can be applied as a callback to any JS event you like, such as clicking a radio button, or opening an accordion. e.g.

{% tabs %}
{% tab title="Liquid" %}
```liquid

<fieldset>
  <legend>Select a payment gateway:</legend>
  <div>
    <input type="radio" id="123" name="paymentGateway" value="123" checked />
    <label for="123">Stripe</label>
  </div>
  <div>
    <input type="radio" id="456" name="paymentGateway" value="456" />
    <label for="456">PayPal</label>
  </div>
</fieldset>
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript

const paymentGatewayCheckboxes = document.querySelectorAll('[name="paymentGateway"]');
paymentGatewayCheckboxes.forEach(function(item) {
  item.addEventListener('change', function(e) {
    const radio = e.currentTarget;
    s_e_set_payment_gateway(radio.value);
  });
})
```
{% endtab %}
{% endtabs %}

If the JS function is not called, the default payment gateway from the multiple available gteways will be used.
