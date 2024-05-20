# 👀 ecommerce/checkout\_standard

### What is it?

This is used to output payment fields in a checkout form.

### Where to use?

You should include this in the layout file for a checkout form at the position in the layout where you would expect the card payment elements to appear.

### How to use?

#### Outputting 1 payment gateway option

```liquid
{% raw %}
{%- include 'ecommerce/checkout_standard' -%}
{% endraw %}

```

This will output the Payment Gateway that you most recently updated in Siteglide Admin.

#### Outputting multiple payment gateway options

```liquid
{%- include 'ecommerce/checkout_standard'
  id: '123'
  default: 'true'
-%}
```

This will output the Payment Gateway with the ID you select. When outputting by ID, you should select which is the default option.

#### Switching active Payment Gateway from Multiple Options

Once you've added multiple Payment Gateways to your form using the include above, you can add JavaScript to switch between them on the client side:

[Switching Between Multiple Payment Method Options](<../../Siteglide Developer Documentation/Switching Between Multiple Payment Method Options.md>)
