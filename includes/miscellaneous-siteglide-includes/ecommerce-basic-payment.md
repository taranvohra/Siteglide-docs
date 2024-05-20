
## What is it?

This is used to output payment fields in a basic payment form.

## Where to use?

You should include this on a basic payment form.

## How to use?

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