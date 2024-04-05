---
title: Building a Custom Payment Gateway
slug: dSVA-
createdAt: 2021-01-07T15:48:52.000Z
updatedAt: 2023-03-03T08:08:57.000Z
---

# Prerequisites

*   Good understanding of Liquid

*   Good understanding of JavaScript

*   Good understanding of GraphQL, including queries, related\_models, mutations and using mutations to send API calls.&#x20;

*   Good understanding of APIs

***

# Introduction

Siteglide have built integrations between its eCommerce Module and three Payment Gateways:

*   Stripe - integrated with all Siteglide eCommerce Features

*   PayPal - for Checkout and Basic Payment Forms

*   Authorize.net - for Basic Payment Forms

In order to focus on improving features for the Payment Gateways we have, we won't be building integrations to any other Payment Gateways at this point. Instead, this Article is intended to help experienced Siteglide Partners build their own Payment Gateway Integrations.&#x20;

***

# Payment Gateway Configuration

We've opened up the Payment Gateway model (model\_schema\_name: "module\_14/payment\_gateway") to allow you to customize it to suit your own Payment Gateway:

| **Field Name**                      | **Field ID**                           | **Purpose/Notes**                                                                                     |
| ----------------------------------- | -------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| Name                                | module\_field\_14/payment\_gateway\_1  | Payment Gateway Display Name                                                                          |
| Active                              | module\_field\_14/payment\_gateway\_2  | Boolean&#xA;&#xA;Only one Payment Gateway should be active at a time.                                 |
| Type                                | module\_field\_14/payment\_gateway\_5  | Payment Gateway Name in snake\_case - Must be unique to your Payment Gateway                          |
| In test mode?                       | module\_field\_14/payment\_gateway\_8  | Boolean                                                                                               |
| Custom Payment Gateway Partial Path | module\_field\_14/payment\_gateway\_19 | Folder path for the partials you will use to include your Gateway code on the Form (see next section) |

# Basic Payment Form Support

The payment flow will look for code in your set Custom Payment Gateway Partial Path. The file it's looking for is `{{Custom Payment Gateway Partial Path}}/basic_payment.liquid`(e.g. `modules/my_ecommerce/payment_gateways/money_take/basic_payment`)

Your code will be included inside the Form - where in the Form Layout you see the tag

`{%- include 'ecommerce/basic_payment', amount: '500', currency: 'gbp' -%}`

To access information about your custom Payment Gateway such as the API Keys, you can output `{{payment_gateway}}` into the layout.

When building you layout consider the following process that needs to be take place.

### Set up Client Side Code on Page Load

Initially set up any Client-side HTML or JavaScript which the Payment Gateway requires to be rendered on Page Load. E.g. elements for securely entering card details.

### Define a Payment Function to run after Form Validation&#x20;

Define a JavaScript function which will set up and carry out the payment transaction. Depending on the complexity of your Payment Gateway, this may include multiple steps.&#x20;

You should assign this function to `window.s_e_payment = my_payment_function`. The Siteglide Form will call this function when validation is complete and it is ready to begin the payment.

The function definition should return a [JavaScript Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) - this will allow the Siteglide Form Submit function to wait for the payment to finish, before it continues submitting the Form.

Your function definition can use the parameter `form` - this contains the DOM element for the Form which has been submitted. This will be used in the JS selectors in the next step to make sure we target the DOM in the correct Form where more than one Form is present on the Page. &#x20;

```javascript
window.s_e_payment = function(form){
	return new Promise(async function (resolve) {
		<!-- Run your payment -->
	});
}
```

All of the following information is available in the HTML DOM and therefore is also accessible via JavaScript.

The parameter `form` from the previous step is used for specificity.&#x20;

See the next step r.e. checking the amount on the Server Side. &#x20;

| **Field**             | **JavaScript Selector**                         | **Purpose/Notes**                                                                                                                                                                                                          |
| --------------------- | ----------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Amount                | `form.querySelector('#s_e_amount').value;`      | The amount of money the customer intends to pay. &#xA;&#xA;For Basic Payment Forms, this value is editable on the Client Side. If you need the original Minimum Amount defined against the Form, run a server -side check. |
| Currency              | `form.s_e_currency('#s_e_currency').value;`     | The currency the customer intends to use.&#xA;&#xA;If you need the original currency set up against the Form, use a server-side check.                                                                                     |
| Form Configuration ID | `form.querySelector('[name="form_id"]').value;` | This Form Configuration ID can be sent to your own Liquid XHR endpoint and used in a GraphQL query to confirm the details of this Form.&#x20;                                                                              |



### Check the Minimum Value is Met

Siteglide Basic Payment Forms have a "Minimum Value" defined in the Form Structure. This can be used in two ways:

*   As the actual value of products or services

*   When the User is choosing their own price e.g. a donation Form, the minimum price the Client will accept in order to not make a loss on the donation when the Payment Gateway's fees are paid.&#x20;

All of our native Payment Gateways include a server-side check to make sure the amount is met- so most likely you'll wish to do the same.&#x20;

In order to do this- your Payment Gateway should make a request to a Liquid Page you create. The Form Configuration ID and Amount should be sent over in your data payload or query parameters.&#x20;

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

```html
{%- assign currency = form_configuration_data.result.items[0].configuration.properties.form_payment_currency.value | downcase -%}
```

```html
{%- assign minimum_amount = form_configuration_data.result.items[0].configuration.properties.form_payment_amount.value | plus: 0 -%}
```

&#x20;On this endpoint, you'll have secure access to these values, so it might make sense to use this same endpoint to:

*   send an API call to your Payment Gateway to set up a Payment Intent (or complete Payment Transaction).

*   run a GraphQL mutation to create a "module\_14/payment" model in the database, (with a status of "Intent Created" or "Payment Complete" as appropriate) (see below)&#x20;

### Create a Record of the Payment in Siteglide

&#x20;In order for the Client to see a record of the Payment in the Siteglide Admin, you must:

*   Create a database object with the model\_schema\_name of module\_14/payment.

*   Via the JavaScript in your Payment function, store the ID of this newly created Payment Model in the hidden HTML field #s\_e\_order\_id. This way it will be submitted with the Form and a relationship will be established between the Payment and the Case- allowing their information to be linked in the Admin.

Depending on the complexity of your Payment Gateway, you may wish to:

*   Create the Payment Model at the same time a Payment Intent is created with the status Intent Created. After capturing funds in a later step, you may wish to update the same model by referring to it by its ID, this time giving it the status Payment Complete.&#x20;

*   Create the Payment Model at the end of the Payment process- to confirm its success. This would immediately be given the status Payment Complete.

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

### Resolve any Errors&#x20;

To halt both your Payment Function and Form Submission and throw errors to the User, you'll need to resolve your Payment Function's promise with an object containing an errors property - an array of objects, each with a message String property.

Note, your Promise should not include a reject, as this will not be used.&#x20;

```javascript
window.s_e_payment = function(form){
	return new Promise(async function (resolve) {
		<!-- Run your payment -->
		<!-- Oops, an error -->
		resolve({ errors: [ { message: my_error } ] });
	});
}
```

### Resolve your Payment

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

***

# Checkout Support

The payment flow will look for code in your set Custom Payment Gateway Partial Path. The file it's looking for is `{{Custom Payment Gateway Partial Path}}/checkout.liquid`(e.g. `modules/my_ecommerce/payment_gateways/money_take/checkout`)

Your code will be included inside the Form - where in the Form Layout you see the tag

`{%- include 'ecommerce/checkout_standard' -%}`

To access information about your custom Payment Gateway such as the API Keys, you can output `{{payment_gateway}}` into the layout.

You may notice that many of the steps are similar to the steps for the Basic Payment Form and you may wish to re-use some of your code.

When building you layout consider the following process that needs to be take place.

### Set up Client Side Code on Page Load

Initially set up any Client-side HTML or JavaScript which the Payment Gateway requires to be rendered on Page Load e.g. elements for securely entering card details.

### Define a Payment Function to run after Form Validation

Define a JavaScript function which will set up and carry out the payment transaction. Depending on the complexity of your Payment Gateway, this may include multiple steps.&#x20;

You should assign this function to `window.s_e_payment = my_payment_function`. The Siteglide Form will call this function when validation is complete and it is ready to begin the payment.

The function definition should return a JavaScript Promise- this will allow the Siteglide Form Submit function to wait for the payment to finish, before it continues submitting the Form.

Your function definition can use the parameter `form` - this contains the DOM element for the Form which has been submitted. This will be used in the JS selectors in the next step to make sure we target the DOM in the correct Form where more than one Form is present on the Page. &#x20;

```javascript
window.s_e_payment = function(form){
	return new Promise(async function (resolve) {
		<!-- Run your payment -->
	});
}
```

### Creating an Order Server-Side

Unlike Basic Payment Forms, the amount to be paid is not stored in a JavaScript variable. Instead, the amount will be calculated using the contents of the User's Cart.

As the process of converting Cart Data to an Order is lengthy, we've opened up our endpoint for your use:

| **Setting**                                                                                                                                                                         | **Value**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| URL                                                                                                                                                                                 | api/ecommerce\_general/order\_pre\_payment\_processor.json                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Method                                                                                                                                                                              | POST                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Required Headers                                                                                                                                                                    | xReq.setRequestHeader('content-type', 'application/json');&#x20;xReq.setRequestHeader('X-CSRF-Token', form.querySelector('\[name=\\'authenticity\_token\\']').value);&#x20;xReq.setRequestHeader('X-Requested-With', 'X-Requested-With: XMLHttpRequest');                                                                                                                                                                                                                                                                                                                                                                                     |
| Body Data:&#x20;*   User ID

*   Email

*   Cart

*   Shipping Method (ID)

*   Order ID (should normally be blank-this is to prevent duplicates)

*   Slug

*   Discount Code (ID) | var data = {    user\_id: form.querySelector('#s\_user\_id').value,&#xA;    email: form.querySelector('#s\_email').value,    cart: form.querySelector('#s\_e\_cart').value,    shipping\_method: form.querySelector('#s\_e\_cart\_shipping').value,    order\_id: form.querySelector('#s\_e\_order\_id').value,    slug: form.querySelector('#s\_e\_slug').value,    discount\_code: form.querySelector('#s\_e\_cart\_discount').value,    form\_id: form.querySelector('\[name=parent\_resource\_id]').value,    hcaptcha: form.querySelector('\[name=h-captcha-response]')? form.querySelector('\[name=h-captcha-response]').value : null}; |
| Response                                                                                                                                                                            | { "order\_id": "xxxxx", "slug": "xxxxx", "errors": { "example\_error\_key": { "id": "xxxxx", "message": "example\_message" }  }  }                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

### Create a Relationship Between the Case and the Order

After receiving your response, you should store the resulting order\_id as the value of the hidden field #s\_e\_order\_id. This will allow the Form to store a relationship between the Order and the Case when the submission is complete. It will also allow you to access that Order when needed server-side.&#x20;

### Check the Order Details Server-Side and Complete the Payment

Depending on the complexity of your Payment Gateway, the payment can either be carried out in a single step, or in multiple steps - this is up to you.

You will however have to send at least one API call to your Payment Gateway from your own Liquid endpoint Page in order to securely send the details of the Order.

To do this, you'll need to run a GraphQL query to fetch the Order, filtering by its ID (the ID returned from the order\_pre\_payment\_processor endpoint) and model\_schema\_name: "module\_14/order".

The table below shows the fields you can access or update in the Order model:

| **Field Name**        | **Field ID**                | **Purpose/Notes**                                                                                                                                                                                                                                                                    |
| --------------------- | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| User ID               | module\_field\_14/order\_1  | &#x20;                                                                                                                                                                                                                                                                               |
| User Email            | module\_field\_14/order\_2  | &#x20;                                                                                                                                                                                                                                                                               |
| Status                | module\_field\_14/order\_3  | Either Intent Created, Payment Complete or a custom status of your choice.&#x20;                                                                                                                                                                                                     |
| Billing Address       | module\_field\_14/order\_4  | Not yet used by Siteglide                                                                                                                                                                                                                                                            |
| Shipping Address      | module\_field\_14/order\_5  | Not yet used by Siteglide                                                                                                                                                                                                                                                            |
| Payment Method        | module\_field\_14/order\_6  | Not yet used by Siteglide. &#xA;&#xA;You must not use this field to store full card numbers. &#xA;&#xA;You may choose to store either an ID or fingerprint (e.g. <https://stripe.com/docs/api/payment_methods>) which your Payment Gateway uses to reference a payment method.&#x20; |
| Shipping Method ID    | module\_field\_14/order\_7  | &#x20;                                                                                                                                                                                                                                                                               |
| Tracking Number       | module\_field\_14/order\_8  | Not yet used by Siteglide                                                                                                                                                                                                                                                            |
| Total Price           | module\_field\_14/order\_9  | &#x20;                                                                                                                                                                                                                                                                               |
| Currency              | module\_field\_14/order\_10 | &#x20;                                                                                                                                                                                                                                                                               |
| Discount Code         | module\_field\_14/order\_11 | &#x20;                                                                                                                                                                                                                                                                               |
| Shipping Method Price | module\_field\_14/order\_12 | &#x20;                                                                                                                                                                                                                                                                               |
| Shipping Method Name  | module\_field\_14/order\_13 | &#x20;                                                                                                                                                                                                                                                                               |
| Discount Code ID      | module\_field\_14/order\_14 | &#x20;                                                                                                                                                                                                                                                                               |

### Resolve any Errors&#x20;

To halt both your Payment Function and Form Submission and throw errors to the User, you'll need to resolve your Payment Function's promise with an object containing an errors property - an array of objects, each with a message String property.

&#x20;Note, your Promise should not include a reject, as this will not be used.&#x20;

```javascript
window.s_e_payment = function(form){
	return new Promise(async function (resolve) {
		<!-- Run your payment -->
		<!-- Oops, an error -->
		resolve({ errors: [ { message: my_error } ] });
	});
}
```

### Resolve your Payment

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

