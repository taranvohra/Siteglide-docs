---
title: PayPal - Custom Parameters
slug: ps0q-paypal-custom-parameters
createdAt: 2021-09-16T07:14:15.000Z
updatedAt: 2023-04-06T15:54:15.000Z
---

PayPal allows you to include different parameters as part of the SDK such as disabling payment options that are unwanted, as per the following link -> [https://developer.paypal.com/docs/checkout/reference/customize-sdk](https://developer.paypal.com/docs/checkout/reference/customize-sdk/)

To use these parameters add this code to top of your Form layout, containing the parameters you want:

```liquid
{% raw %}
{%- capture data -%}&disable-funding=sofort{%- endcapture -%}
{%- export data, namespace: "s_paypal_options" -%}
{% endraw %}
```

This specific example will stop Sofort being offered as a payment option.