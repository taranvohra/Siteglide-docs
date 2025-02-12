# 📋 Steps to Support Basic Payment Forms with your Custom Payment Gateway

## Pre-Requisites

{% content-ref url="./" %}
[.](./)
{% endcontent-ref %}

{% content-ref url="../../../../eCommerce/get-started-ecommerce/basic-payment-forms/basic-payments.md" %}
[basic-payments.md](../../../../eCommerce/get-started-ecommerce/basic-payment-forms/basic-payments.md)
{% endcontent-ref %}

## Basic Payment Form Support

The payment flow will look for code in your set Custom Payment Gateway Partial Path. The file it's looking for is `{{Custom Payment Gateway Partial Path}}/basic_payment.liquid`(e.g. `modules/my_ecommerce/payment_gateways/money_take/basic_payment`)

Your code will be included inside the Form - where in the Form Layout you see the tag

```liquid
{% raw %}
{% include "ecommerce/basic_payment",
  amount: '500',
  currency: 'usd',
  id: '10' 
%}
{% endraw %}
```

To access information about your custom Payment Gateway such as the API Keys, you can output `{{payment_gateway}}` into the layout.

When building you layout consider the following process that needs to be take place.

### Step 1) Set up Client Side Code on Page Load

Initially set up any Client-side HTML or JavaScript which the Payment Gateway requires to be rendered on Page Load. E.g. elements for securely entering card details.

### Step 2) Define a Payment Function to run after Form Validation

Define a JavaScript function which will set up and carry out the payment transaction. Depending on the complexity of your Payment Gateway, this may include multiple steps.

You should assign this function to `window.s_e_payment = my_payment_function`. The Siteglide Form will call this function when validation is complete and it is ready to begin the payment.

The function definition should return a [JavaScript Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Promise) - this will allow the Siteglide Form Submit function to wait for the payment to finish, before it continues submitting the Form.

Your function definition can use the parameter `form` - this contains the DOM element for the Form which has been submitted. This will be used in the JS selectors in the next step to make sure we target the DOM in the correct Form where more than one Form is present on the Page.

```javascript
window.s_e_payment = function(form){
	return new Promise(async function (resolve) {
		<!-- Run your payment -->
	});
}
```

All of the following information is available in the HTML DOM and therefore is also accessible via JavaScript.

The parameter `form` from the previous step is used for specificity.

See the next step r.e. checking the amount on the Server Side.

| **Field**             | **JavaScript Selector**                         | **Purpose/Notes**                                                                                                                                                                                                |
| --------------------- | ----------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Amount                | `form.querySelector('#s_e_amount').value;`      | The amount of money the customer intends to pay. For Basic Payment Forms, this value is editable on the Client Side. If you need the original Minimum Amount defined against the Form, run a server -side check. |
| Currency              | `form.s_e_currency('#s_e_currency').value;`     | The currency the customer intends to use. If you need the original currency set up against the Form, use a server-side check.                                                                                    |
| Form Configuration ID | `form.querySelector('[name="form_id"]').value;` | This Form Configuration ID can be sent to your own Liquid XHR endpoint and used in a GraphQL query to confirm the details of this Form.                                                                          |

### Step 3) Check the Minimum Value is Met

Siteglide Basic Payment Forms have a "Minimum Value" defined in the Form Structure. This can be used in two ways:

* As the actual value of products or services
* When the User is choosing their own price e.g. a donation Form, the minimum price the Client will accept in order to not make a loss on the donation when the Payment Gateway's fees are paid.

All of our native Payment Gateways include a server-side check to make sure the amount is met- so most likely you'll wish to do the same.

In order to do this- your Payment Gateway should make a request to a Liquid Page you create. The Form Configuration ID and Amount should be sent over in your data payload or query parameters.

The Endpoint Page should run an `admin_form_configurations` query:

```graphql
query(
	$fc_id: ID!
){
	result: admin_form_configurations(
		filter: {
			id: {
				value: $fc_id
			}
		}
	){
		items: results{
			configuration
		}
	}
}
```

In the results of this query, you'll be able to verify the true minimum amount and currency. You can compare these to the s\_e\_amount value calculated on the Front-end. Depending on the result\_name you choose - the values from this example query of note are:

```liquid
{% raw %}
{%- assign currency = form_configuration_data.result.items[0].configuration.properties.form_payment_currency.value | downcase -%}
{% endraw %}



```

```liquid
{% raw %}
{%- assign minimum_amount = form_configuration_data.result.items[0].configuration.properties.form_payment_amount.value | plus: 0 -%}
{% endraw %}


```

On this endpoint, you'll have secure access to these values, so it might make sense to use this same endpoint to:

* send an API call to your Payment Gateway to set up a Payment Intent (or complete Payment Transaction).
* run a GraphQL mutation to create a "module\_14/payment" model in the database, (with a status of "Intent Created" or "Payment Complete" as appropriate) (see below)

### Step 4) Create a Record of the Payment in Siteglide

In order for the Client to see a record of the Payment in the Siteglide Admin, you must:

* Create a database object with the model\_schema\_name of module\_14/payment.
* Via the JavaScript in your Payment function, store the ID of this newly created Payment Model in the hidden HTML field #s\_e\_order\_id. This way it will be submitted with the Form and a relationship will be established between the Payment and the Case- allowing their information to be linked in the Admin.

Depending on the complexity of your Payment Gateway, you may wish to:

* Create the Payment Model at the same time a Payment Intent is created with the status Intent Created. After capturing funds in a later step, you may wish to update the same model by referring to it by its ID, this time giving it the status Payment Complete.
* Create the Payment Model at the end of the Payment process- to confirm its success. This would immediately be given the status Payment Complete.

The key fields you will need to set on the Payment Model are shown in the following table:

| Field Name                                                                                       | Field ID                     | Purpose / Notes                                                                                 |
| ------------------------------------------------------------------------------------------------ | ---------------------------- | ----------------------------------------------------------------------------------------------- |
| Payment ID                                                                                       | module\_field\_14/payment\_1 | The Payment Gateway's ID for this Payment Intent                                                |
| Gateway ID                                                                                       | module\_field\_14/payment\_2 | Optional - The ID of the Payment Gateway in Siteglide that handled this payment.                |
| Gateway Type                                                                                     | module\_field\_14/payment\_4 | Optional - The type of the Payment Gateway in Siteglide that handled this payment.              |
| Status                                                                                           | module\_field\_14/payment\_5 | The status of this Payment: Intent Created, Payment Complete or a custom Status of your choice. |
| Charge ID (Stripe), Capture ID (PayPal) or use for a similar purpose in another Payment Gateway. | module\_field\_14/payment\_6 | Optional                                                                                        |
| Currency                                                                                         | module\_field\_14/payment\_7 | The actual currency used.                                                                       |
| Amount                                                                                           | module\_field\_14/payment\_8 | The actual amount to be paid.                                                                   |

### Step 5) Resolve any Errors

To halt both your Payment Function and Form Submission and throw errors to the User, you'll need to resolve your Payment Function's promise with an object containing an errors property - an array of objects, each with a message String property.

Note, your Promise should not include a reject, as this will not be used.

```javascript
window.s_e_payment = function(form){
	return new Promise(async function (resolve) {
		<!-- Run your payment -->
		<!-- Oops, an error -->
		resolve({ errors: [ { message: my_error } ] });
	});
}
```

### Step 6) Resolve your Payment

Once your my\_payment\_function payment function is complete and the funds have been captured, you will want to let the Siteglide Form Submit Function finish submitting the Form. To do this, resolve the Promise (without an errors object):

```javascript
window.s_e_payment = function(form){
	return new Promise(async function (resolve) {
		<!-- Run your payment -->
		resolve('complete');
        <!-- Form Submission continues -->
	});
}
```
