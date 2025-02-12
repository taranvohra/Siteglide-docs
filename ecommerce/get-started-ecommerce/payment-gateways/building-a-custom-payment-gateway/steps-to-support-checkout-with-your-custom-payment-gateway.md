# 📋 Steps to Support Checkout with your Custom Payment Gateway

## Pre-Requisites

{% content-ref url="./" %}
[.](./)
{% endcontent-ref %}

{% content-ref url="../../../../eCommerce/get-started-ecommerce/cart-checkout-and-quotes/about-cart-checkout-and-quotes.md" %}
[about-cart-checkout-and-quotes.md](../../../../eCommerce/get-started-ecommerce/cart-checkout-and-quotes/about-cart-checkout-and-quotes.md)
{% endcontent-ref %}

## Checkout Support

The payment flow will look for code in your set Custom Payment Gateway Partial Path. The file it's looking for is `{{Custom Payment Gateway Partial Path}}/checkout.liquid`(e.g. `modules/my_ecommerce/payment_gateways/money_take/checkout`)

Your code will be included inside the Form - where in the Form Layout you see the tag

To access information about your custom Payment Gateway such as the API Keys, you can output `{{payment_gateway}}` into the layout.

You may notice that many of the steps are similar to the steps for the Basic Payment Form and you may wish to re-use some of your code.

When building you layout consider the following process that needs to be take place.

### Step 1) Set up Client Side Code on Page Load

Initially set up any Client-side HTML or JavaScript which the Payment Gateway requires to be rendered on Page Load e.g. elements for securely entering card details.

### Step 2) Define a Payment Function to run after Form Validation

Define a JavaScript function which will set up and carry out the payment transaction. Depending on the complexity of your Payment Gateway, this may include multiple steps.

You should assign this function to `window.s_e_payment = my_payment_function`. The Siteglide Form will call this function when validation is complete and it is ready to begin the payment.

The function definition should return a JavaScript Promise- this will allow the Siteglide Form Submit function to wait for the payment to finish, before it continues submitting the Form.

Your function definition can use the parameter `form` - this contains the DOM element for the Form which has been submitted. This will be used in the JS selectors in the next step to make sure we target the DOM in the correct Form where more than one Form is present on the Page.

```javascript
window.s_e_payment = function(form){
	return new Promise(async function (resolve) {
		<!-- Run your payment -->
	});
}
```

### Step 3) Creating an Order Server-Side

Unlike Basic Payment Forms, the amount to be paid is not stored in a JavaScript variable. Instead, the amount will be calculated using the contents of the User's Cart.

As the process of converting Cart Data to an Order is lengthy, we've opened up our endpoint for your use:

| **Setting**           | **Value**                                                                                                                                                                                                                                       |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| URL                   | api/ecommerce\_general/order\_pre\_payment\_processor.json                                                                                                                                                                                      |
| Method                | POST                                                                                                                                                                                                                                            |
| Required Headers      | xReq.setRequestHeader('content-type', 'application/json'); xReq.setRequestHeader('X-CSRF-Token', form.querySelector('\[name=\\'authenticity\_token\\']').value); xReq.setRequestHeader('X-Requested-With', 'X-Requested-With: XMLHttpRequest'); |
| Body Data: \* User ID |                                                                                                                                                                                                                                                 |

* Email
* Cart
* Shipping Method (ID)
* Order ID (should normally be blank-this is to prevent duplicates)
* Slug
* Discount Code (ID) | var data = { user\_id: form.querySelector('#s\_user\_id').value, email: form.querySelector('#s\_email').value, cart: form.querySelector('#s\_e\_cart').value, shipping\_method: form.querySelector('#s\_e\_cart\_shipping').value, order\_id: form.querySelector('#s\_e\_order\_id').value, slug: form.querySelector('#s\_e\_slug').value, discount\_code: form.querySelector('#s\_e\_cart\_discount').value, form\_id: form.querySelector('\[name=parent\_resource\_id]').value, hcaptcha: form.querySelector('\[name=h-captcha-response]')? form.querySelector('\[name=h-captcha-response]').value : null}; | | Response | { "order\_id": "xxxxx", "slug": "xxxxx", "errors": { "example\_error\_key": { "id": "xxxxx", "message": "example\_message" } } } |

### Step 4) Create a Relationship Between the Case and the Order

After receiving your response, you should store the resulting order\_id as the value of the hidden field #s\_e\_order\_id. This will allow the Form to store a relationship between the Order and the Case when the submission is complete. It will also allow you to access that Order when needed server-side.

### Step 5) Check the Order Details Server-Side and Complete the Payment

Depending on the complexity of your Payment Gateway, the payment can either be carried out in a single step, or in multiple steps - this is up to you.

You will however have to send at least one API call to your Payment Gateway from your own Liquid endpoint Page in order to securely send the details of the Order.

To do this, you'll need to run a GraphQL query to fetch the Order, filtering by its ID (the ID returned from the order\_pre\_payment\_processor endpoint) and model\_schema\_name: "module\_14/order".

The table below shows the fields you can access or update in the Order model:

| **Field Name**        | **Field ID**                | **Purpose/Notes**                                                                                                                                                                                                                                                                                         |
| --------------------- | --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| User ID               | module\_field\_14/order\_1  |                                                                                                                                                                                                                                                                                                           |
| User Email            | module\_field\_14/order\_2  |                                                                                                                                                                                                                                                                                                           |
| Status                | module\_field\_14/order\_3  | Either Intent Created, Payment Complete or a custom status of your choice.                                                                                                                                                                                                                                |
| Billing Address       | module\_field\_14/order\_4  | Not yet used by Siteglide                                                                                                                                                                                                                                                                                 |
| Shipping Address      | module\_field\_14/order\_5  | Not yet used by Siteglide                                                                                                                                                                                                                                                                                 |
| Payment Method        | module\_field\_14/order\_6  | Not yet used by Siteglide. You must not use this field to store full card numbers. You may choose to store either an ID or fingerprint (e.g. [https://stripe.com/docs/api/payment\_methods](https://stripe.com/docs/api/payment\_methods)) which your Payment Gateway uses to reference a payment method. |
| Shipping Method ID    | module\_field\_14/order\_7  |                                                                                                                                                                                                                                                                                                           |
| Tracking Number       | module\_field\_14/order\_8  | Not yet used by Siteglide                                                                                                                                                                                                                                                                                 |
| Total Price           | module\_field\_14/order\_9  |                                                                                                                                                                                                                                                                                                           |
| Currency              | module\_field\_14/order\_10 |                                                                                                                                                                                                                                                                                                           |
| Discount Code         | module\_field\_14/order\_11 |                                                                                                                                                                                                                                                                                                           |
| Shipping Method Price | module\_field\_14/order\_12 |                                                                                                                                                                                                                                                                                                           |
| Shipping Method Name  | module\_field\_14/order\_13 |                                                                                                                                                                                                                                                                                                           |
| Discount Code ID      | module\_field\_14/order\_14 |                                                                                                                                                                                                                                                                                                           |
| Subtotal Price        | module\_field\_14/order\_15 |                                                                                                                                                                                                                                                                                                           |
| Subtotal Before Tax   | module\_field\_14/order\_16 |                                                                                                                                                                                                                                                                                                           |
| Subtotal Tax Amount   | module\_field\_14/order\_17 |                                                                                                                                                                                                                                                                                                           |
| Shipping Option Price | module\_field\_14/order\_23 |                                                                                                                                                                                                                                                                                                           |
| Total Before Tax      | module\_field\_14/order\_25 |                                                                                                                                                                                                                                                                                                           |
| Total Tax Amount      | module\_field\_14/order\_26 |                                                                                                                                                                                                                                                                                                           |
| Cart Data             | module\_field\_14/order\_27 |                                                                                                                                                                                                                                                                                                           |
| Shipping Data         | module\_field\_14/order\_30 |                                                                                                                                                                                                                                                                                                           |

### Step 6) Resolve any Errors

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

### Step 7) Resolve your Payment

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
