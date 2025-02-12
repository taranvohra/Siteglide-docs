# 👀 Basic Payment Forms Reference

## Including on a Page

To include a Basic Payment Form on the Page, use the same syntax as a [standard form](../../../cms/forms/forms-reference.md):

```liquid
{% raw %}
{%- include 'form', id: '10', layout: 'default' -%}
{% endraw %}


```

## Form Layouts

### Authorize.net Specific Instructions

{% content-ref url="authorize.net-basic-payment-forms.md" %}
[authorize.net-basic-payment-forms.md](authorize.net-basic-payment-forms.md)
{% endcontent-ref %}

### PayPal Specific Instructions

{% content-ref url="paypal-basic-payment-forms.md" %}
[paypal-basic-payment-forms.md](paypal-basic-payment-forms.md)
{% endcontent-ref %}

### ecommerce/basic\_payment Liquid Tag

#### What is it?

This is used to output payment fields in a basic payment form.

#### Where to use?

You should include this _inside_ a basic payment form layout.

#### How to use?

```liquid
{% raw %}
{%- include 'ecommerce/basic_payment'
  amount: '500'
  currency: 'usd'
  id: '10'
-%}
{% endraw %}
```

| Parameter | Type    | Notes                                                                                                                                                        |
| --------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| amount    | Integer | The amount to be charged in cents/pence (e.g. 500 = $5.00)                                                                                                   |
| currency  | String  | The currency to charge the user                                                                                                                              |
| id        | Integer | The ID of the Payment Gateway to be used. If not included, then the system will output the Payment Gateway that you most recently updated in Siteglide Admin |

{% hint style="info" %}
Also see [Switching Payment Gateways](../payment-gateways/switching-gateway.md)
{% endhint %}

### s\_e\_amount Field

This HTML input field with the ID s\_e\_amount can be used to modify the amount which will be paid when the Form is submitted, see:

{% content-ref url="steps-to-allow-user-to-decide-amount-they-will-pay.md" %}
[steps-to-allow-user-to-decide-amount-they-will-pay.md](steps-to-allow-user-to-decide-amount-they-will-pay.md)
{% endcontent-ref %}

[#a-note-on-security](/eCommerce/get-started-ecommerce/basic-payment-forms/basic-payments.md#a-note-on-security "mention")

## Payment Confirmation Layouts

{% content-ref url="payment-confirmation.md" %}
[payment-confirmation.md](payment-confirmation.md)
{% endcontent-ref %}

```
{% raw %}
{% include 'ecommerce/payment_details', layout: 'default' %}
{% endraw %}
```
