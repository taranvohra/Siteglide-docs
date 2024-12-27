# 📋 How to Set Up a Shopping Cart and Guest Checkout - Tutorial

### Prerequisites

* You have installed the eCommerce Module
* You have set up a Payment Gateway
* You have added Products to the database
* You have set up a Product List View
* You have set up Product Detail Pages
* _Using PayPal as a Payment Gateway?_ There are additional setup instructions [here](/ecommerce/get-started-ecommerce/payment-gateways/paypal-custom-params.md).

### Introduction

The Siteglide Ecommerce Module makes it easy to set up a secure and reliable Shopping Cart and Checkout flow. As usual, you can customise your layouts at every step.

In this tutorial, we will show you how to create the simplest Cart and Checkout flow- the Guest Checkout. Users can buy Products without having to sign in, but their details are stored in the CRM so the Site Owner can send them their Products.

In future tutorials we will show how to extend this with the following features:

* Use the Secure Zone Module to Sign Up and Login users at different stages of their shopping experience.
* Use Product Attributes to add Products with variations to your shopping Cart.
* Use Categories to Create Pages which display different lists of Products.
* Add a Cart Summary to the Header

### Getting Started: How to Set Up a Cart and Guest Checkout Flow

#### Step 1- The Add to Cart Button

Make sure your Product Detail pages have an add to Cart Button in their layout’s item.liquid file.

Learn more about Product Detail pages [here](/ecommerce/get-started-ecommerce/cart-checkout-and-quotes/product-views/product-detail.md).

![](https://d258lu9myqkejp.cloudfront.net/attachment\_images/09bec6936a6d6b6df748b7b4d793a9bd3e35619c1a44369f1508ff70eabc0bd679bbc6c1-f720-4782-a09c-c66699\_dv7ljb.png)

This liquid include tag will add the "Add to Cart" Button:

```liquid
{% raw %}
{% include 'ecommerce/cart_add' -%}
{% endraw %}
```

This needs to be in the item.liquid file to work, because this will have access to the correct data for this Product.

#### Step 2 - The Cart

Create a new Page for your Cart and use liquid to include the Cart.

(Note- the Cart does not need to be on it’s own page, but this is the easiest place to start.)

Use this liquid to include the Cart layout in your page.

```liquid
{% raw %}
{%- include 'ecommerce/cart', layout: 'cart', remove_default_css: 'false' -%}
{% endraw %}
```

Use the `layout` parameter to select the folder which contains the wrapper.liquid and the item.liquid file you would like to use for your layout. For now, you can use the "cart" layout which is included in the Ecommerce Module.

Use the `remove_default_css` parameter to choose if you want to remove `siteglide_example.css` from output or not.

Learn more about Cart Layouts [here](/ecommerce/get-started-ecommerce/cart-checkout-and-quotes/cart/cart-layouts.md)

#### Step 3 - Create a Form for your Checkout Page

This will store a paying User against the CRM and submit their payment details securely via your chosen Payment Gateway.

You can add a form by navigating to `CMS/Forms` in the left hand Menu and then clicking the "+ Add New Form" button in the top right of the page. Learn more about forms [here](/cms/forms/quickstart-forms.md).

You will need to add the following information when creating your form:

* Form Name: e.g. Checkout Form
* Redirect URL - This is the relative URL you want a user to be redirected to after submission of payment details e.g. a confirmation page.
* In the payments tab, toggle "Use as a payment form?" to on
* Payment Form Type will appear under the payments tab. Select "Standard Checkout".

Save your changes.

#### Step 4- Create a new Page for your Checkout.

Learn more about pages [here](/cms/pages/quickstart-pages.md)

#### Step 5- Add the Checkout form to your Checkout Page

Include the Checkout Layout in your page:

```liquid
{% raw %}
{% include 'ecommerce/checkout', form_id: '2', layout: 'default' -%}
{% endraw %}
```

The form\_id parameter should be the id of your Checkout Form. If you use the Toolbox to add this code, you can lookup your form by name.

The layout parameter should refer to the folder which contains your form layout file. This file exists here:

`layouts/forms/form_2/default.liquid`

For now, you can use the "default" layout that is included with the eCommerce module.

If the page is visited while the user has an empty cart, an alternative "empty" layout will show. The default form layout will automatically add an empty layout at the path:

`layouts/modules/module_14/checkout/default/empty.liquid`

If you create a custom layout, you should also create an empty.liquid file, renaming the default folder in the filepath above with the name of your form layout.

#### Step 6: Test your eCommerce flow.

Remember, you will need to use the test cards from your chosen Payment Gateway. Find more information [here](/ecommerce/get-started-ecommerce/payment-gateways/README.md)

Users will be added to the CRM in Admin.

You can see the records of transactions in Admin by navigating to the Orders list or finding the User in the CRM.

### Orders

After a User has submitted your Checkout form, an order will be automatically generated. You can see a list of orders under `ECOMMERCE/Orders` in the left-hand menu.

Click on the name of the order for more information.

### A note on Inventory

As a user buys a Product, the Inventory decreases accordingly.

A User cannot buy a Product if its Inventory is 0, but you can also hide Products that have sold out from the Product List Views.