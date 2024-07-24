# 📋 Steps to Allow User to Decide Amount they Will Pay

## Pre-Requisites

First, set up a Basic Payment Form with a minimum payment amount by following the steps here:

{% content-ref url="steps-to-set-up-a-basic-payment-form-with-a-fixed-payment-amount.md" %}
[steps-to-set-up-a-basic-payment-form-with-a-fixed-payment-amount.md](steps-to-set-up-a-basic-payment-form-with-a-fixed-payment-amount.md)
{% endcontent-ref %}

## When is this Useful?

In some use-cases you may wish the amount to be paid to depend on the User's input into the Form Fields e.g.

* The User is making charitable donations. The minimum payment is $2, but they can choose to donate any amount above that they wish.
* The User will select options on the Form that will inform a logical function to decide how much they need to pay.

Both use-cases will require you to write a JavaScript function which will update the value of the amount due.

## Step 1) Using Liquid to Fetch the Currency and Minimum Amount from Admin

You may find the following Liquid tags helpful while developing:

| **Liquid**                                                              | **Role**                                                                                  | **Example** |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------- |
| `{% include 'ecommerce/basic_payment_currency' %}`                      | The currency for the Form defined in Admin                                                | gbp         |
| `{% include 'ecommerce/basic_payment_currency', format: 'symbol' %}`    | The symbol for the currency for the Form defined in Admin                                 | £           |
| `{% include 'ecommerce/basic_payment_min_amount' %}`                    | The `minimum payment` value defined in Admin, in the lowest denomination of that currency | 100         |
| `{% include 'ecommerce/basic_payment_min_amount', format: 'decimal' %}` | The `minimum payment` value defined in Admin, formatted                                   | 1.00        |

## Step 2) Writing the function

The end goal of such a JavaScript function will be to set the value of hidden field with the ID "`s_e_amount`". The default value of this field will be the same as the minimum payment value you set in Admin, until it is changed via JavaScript. The final value should be an integer (whole number) of the number of cents that will be paid.

We'll give you an example of how this JavaScript may work here. You can adapt this example to suit your use case. The important thing is that you set the value of the field with the ID "`s_e_amount`".

### Example 1 - Allowing the User to enter any value they wish

The following example allows the User to enter an amount of their choice into an input in the Form. Our function changes the format, then sets the value of the hidden field. Note that the entire example should sit inside a Liquid `{% form %}` tag.

{% tabs %}
{% tab title="Liquid" %}
```liquid
<div class="">
  <label for="user_chooses_amount_to_pay">
    How much can you afford to donate (pounds and pence e.g. 10.00)?
  </label>
  <div style="display: flex; align-items: center;"
    <span style="margin-right: 5px;">{{context.exports.currency_map.data['GBP']}}</span>
    <input class="form-control" 
      id="user_chooses_amount_to_pay" 
      type="text" 
      placeholder="10.00"
    >
  </div>
</div>

```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
function changeAmountToPay() {
  var output = document.querySelector('#s_e_amount');
  output.value = parseInt(event.target.value * 100); 
  //As the end result must be in cents / pennies, we multiply the given value by 100 and make sure it is an integer. 
}
var input = document.querySelector('#user_chooses_amount_to_pay');
input.addEventListener('keyup', changeAmountToPay);
```
{% endtab %}
{% endtabs %}

### Example 2 - Using URL parameters to change the value of s\_e\_amount

This example shows how you can add an "amount" parameter to the URL- if this parameter exists then the `s_e_amount` will be updated.

The following Javascript can be added to your Basic Payment Form's Layout. The first half of the function will store the amount parameter within the "amount" variable, the second half checks if "amount" exists (this prevents "null" from getting added to `s_e_amount`) if so then `s_e_amount` is updated with the new price:

```javascript
window.addEventListener('DOMContentLoaded', (event) => {
      //fetch amount param from the URL
      const urlParams = new URLSearchParams(window.location.search);
      const amount = urlParams.get('amount');
      //set s_e_amount value to amount from url param
      if(amount) {
            document.querySelector('#s_e_amount').value = amount;
      };
});
```

An example URL might be, to set the price to 20.00 or 2000 pence/cents:

```
/page-url?amount=2000
```

