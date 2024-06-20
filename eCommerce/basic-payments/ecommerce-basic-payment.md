# 👀 Basic Payment Forms Reference

## Including on a Page

To include a Basic Payment Form on the Page, use the same syntax as a [standard form](../../forms/forms-reference.md):

```liquid
{% raw %}
{%- include 'form', id: '10', layout: 'default' -%}
{% endraw %}
```

## Form Layouts

### ecommerce/basic\_payment Liquid Tag

#### What is it?

This is used to output payment fields in a basic payment form.

#### Where to use?

You should include this _inside_ a basic payment form layout.

#### How to use?

```liquid
{%- include 'ecommerce/basic_payment'
  amount: '500'
  currency: 'usd'
  id: '10'
-%}
```

| Parameter | Type    | Notes                                                                                                                                                        |
| --------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| amount    | Integer | The amount to be charged in cents/pence (e.g. 500 = $5.00)                                                                                                   |
| currency  | String  | The currency to charge the user                                                                                                                              |
| id        | Integer | The ID of the Payment Gateway to be used. If not included, then the system will output the Payment Gateway that you most recently updated in Siteglide Admin |

{% hint style="info" %}
Also see [Switching Payment Gateways](../payment-gateways/switching-gateway.md)
{% endhint %}

## Payment Confirmation Layouts

{% content-ref url="payment-confirmation.md" %}
[payment-confirmation.md](payment-confirmation.md)
{% endcontent-ref %}

```
{% raw %}
{% include 'ecommerce/payment_details', layout: 'default' %}
{% endraw %}
```

