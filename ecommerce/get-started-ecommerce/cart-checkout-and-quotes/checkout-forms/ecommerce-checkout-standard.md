# 🔹 Checkout Form Layouts

## Checkout Form Layout

Mostly Checkout Form Layouts are developed in the same way as [standard CMS Form Layouts](../../../../cms/forms/forms-reference.md), with a few differences included below:

### ecommerce/checkout\_standard

#### What is it?

This liquid include used to output payment fields in a checkout form.

#### Where to use?

You should include this in the layout file for a checkout form at the position in the layout where you would expect the card payment elements to appear.

#### How to use?

_Outputting 1 payment gateway option_

```liquid
{% raw %}
{%- include 'ecommerce/checkout_standard' -%}
{% endraw %}


```

This will output the Payment Gateway that you most recently updated in Siteglide Admin.

_Outputting multiple payment gateway options_

```liquid
{%- include 'ecommerce/checkout_standard'
  id: '123'
  default: 'true'
-%}

```

This will output the Payment Gateway with the ID you select. When outputting by ID, you should select which is the default option.

#### Payment Method Options

When using Stripe as your Payment Gateway, the default payment method option is locked to 'Card Only' (`type: 'card_only'`).

Alternatively you can show other payment method options such as Klarna or Apple Pay. You can control exactly which options show by configuring them in your Stripe Dashboard here -> https://dashboard.stripe.com/settings/payment\_methods Then you need to update your code to include the 'type' parameter with a value of 'payment' as follows:

```liquid
{%- include 'ecommerce/checkout_standard'
  id: '123'
  type: 'payment'
-%}
```

#### Switching active Payment Gateway from Multiple Options

Once you've added multiple Payment Gateways to your form using the include above, you can add JavaScript to switch between them on the client side:

[Switching Between Multiple Payment Method Options](../../payment-gateways/switching-gateway.md)
