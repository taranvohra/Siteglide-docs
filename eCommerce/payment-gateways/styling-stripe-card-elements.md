---
title: How to style the Card Fields in any Payment Form using the Stripe Payment Gateway?
slug: eReY-
createdAt: 2021-02-18T14:33:39.000Z
updatedAt: 2023-03-03T08:09:58.000Z
---

The Stripe Payment Gateway provides its own iframe to accept Card Details securely so direct styling isn't possible. Instead use JavaScript.

# Introduction

The Stripe Payment Gateway provides its own iframe to accept Card Details securely so it's not possible to have full access to the HTML structure so you can apply your own styles. Instead, you can use JavaScript to pass your styles safely to Stripe.&#x20;

This method will work on any kind of Payment Form which uses Stripe. This includes:

*   [Basic Payment Form](https://developers.siteglide.com/basic-payment-forms-tutorial)

*   Checkout

*   Subscription Sign Up

# Setting Styles

## Setting up the JavaScript Variable

Styles are passed securely to Stripe using JavaScript, rather than your traditional method of applying styles directly with a CSS file.&#x20;

To do this, create a global JavaScript variable `stripe_style` at the top of your Form Layout or Page. Its value should be an object like the following:

```javascript
<script>
var stripe_style = {
  base: {
    color: '#DDA0DD', //Sets CSS property "color" of "base" variant
    '::placeholder': {
      color: '#DDA0DD' // Sets CSS property of placeholders within the "base" variant
    }
  }
}
</script>
```

## Available Selectors and CSS properties

As in the example above- the `stripe_style` variable is passed a JavaScript object.&#x20;

You can see Stripe's full definition of how this object should be structured using their documentation here: <https://stripe.com/docs/js/appendix/style>. The first set of keys e.g. base represents a "variant" or state the elements might be in. Nested within this, certain allowed CSS properties may be set.&#x20;

# Renaming the Classes - Advanced

You can ask Stripe to rename some of the available classes by redefining the `classes` object. To do this in Siteglide, create a global variable `stripe_classes`:

```javascript
<script>
var stripe_classes = {
    classes: {
        base: "my-custom-container-class" //Renames the base class from the default "StripeElement" to "my-custom-container-class". 
    }
}
</script>
```

Any styles you set in the `stripe_styles` object to base will still apply after changing the class, unless you specifically override them.&#x20;

You can see a full reference for the available properties for this object in the Stripe documentation here: <https://stripe.com/docs/js/elements_object/create_element?type=card#elements_create-options-classes>