# 📋 PayPal Basic Payment Forms

#### Prerequisites

* You have set up a PayPal Payment Gateway, with the required authentication: [Payments Gateways](../introduction-1/)

## Introduction

The PayPal Payment Gateway is compatible with Basic Payment Forms and Checkout Forms. However, there are a few differences to take into account when you choose this Payment Gateway.

## Step 1) Removing the Submit Button

PayPal creates its own secure Submit Buttons for the payment Form. This means you should remove the default submit button from the Form Layout if you are using the PayPal Payment Gateway. We've included an error log in the JavaScript console to remind developers of this.

## Step 2) Adding Custom Error Functions without the Submit Button

As custom error functions are normally passed in as an argument on the submit button's onclick listener, we've had to provide an alternative means to attach this: a global JavaScript variable.. You can set this in a \<script> tag inside your Form Layout like so:

```xml
<script>
function error_function() {
//Do something
};
window.s_e_paypal_error = error_function;	
<script>
```

## Step 3) Using a Custom JavaScript Notification/Message is Recommended with PayPal

We recommend using a Custom Error Notification with PayPal. JavaScript alert messages are sometimes covered by the secure PayPal browser window- meaning the User Experience can become impaired. We'd recommend outputting error messages directly on the Page instead or using a library like [Sweet Alert 2](https://sweetalert2.github.io/).

You can see an example which does this in our updated [Custom Error Function](https://developers.siteglide.com/custom-javascript-validation-for-forms) Article.
