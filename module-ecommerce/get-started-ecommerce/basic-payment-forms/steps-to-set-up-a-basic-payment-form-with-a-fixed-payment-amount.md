# 📋 Steps to Set up a Basic Payment Form (with a Fixed Payment Amount)

## Step 1) Head to CMS / Forms

## Step 2) Create a New Form

<figure><img src="../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

## Step 3) Add a Name and Redirect URL. Set up any Custom Fields you wish to add

<figure><img src="../../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Step 4) In the Payments Tab, Toggle Payments on and Select Basic Payment

<figure><img src="../../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
For a basic fixed-amount set up, set the minimum payment value to exactly what you want users filling in the Form to Pay.\
\
For charitable donations and invoice payments, set the minimum payment to something minimal like $5 which avoids you making a loss on payment gateway fees for tiny transactions. Then look to [steps-to-allow-user-to-decide-amount-they-will-pay.md](../../../ecommerce/get-started-ecommerce/basic-payment-forms/steps-to-allow-user-to-decide-amount-they-will-pay.md "mention")
{% endhint %}

## Step 5) Optionally, Give Lifetime Access to a Secure Zone to Users Who Pay

In the Secure Zones tab, pick a Secure Zone. Access will be granted when payment is made and the Form is submitted.

<figure><img src="../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

## Step 6) Save the Form

<figure><img src="../../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Step 7) Output your Form on a Page

Back in CMS Forms, find the ID for your newly created Form:

<figure><img src="../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

Use this ID in the Liquid tag when you insert the Form on the Page (or use Toolbox as a quick shortcut):

```
{% raw %}
{% include 'form', id: '11', layout: 'default' %}
{% endraw %}


```

Your Payment Form is now set up and ready to accept payments using the minimum payment value you set.

## Step 8) Testing

If your Payment Gateway is in 'Test Mode', then you may need to enter card details specific to the testing environment.

{% content-ref url="../../../ecommerce/introduction-1/test-cards.md" %}
[test-cards.md](../../../ecommerce/introduction-1/test-cards.md)
{% endcontent-ref %}

## Step 9) Install a SiteBuilder Layout or Create your Own Layout

{% hint style="info" %}
If you are using the Stripe Payment Gateway, this step is optional.
{% endhint %}

For PayPal or Authorize.net, you will need to follow the relevant extra steps:

{% content-ref url="../../../ecommerce/get-started-ecommerce/basic-payment-forms/authorize.net-basic-payment-forms.md" %}
[authorize.net-basic-payment-forms.md](../../../ecommerce/get-started-ecommerce/basic-payment-forms/authorize.net-basic-payment-forms.md)
{% endcontent-ref %}

{% content-ref url="../../../ecommerce/get-started-ecommerce/basic-payment-forms/paypal-basic-payment-forms.md" %}
[paypal-basic-payment-forms.md](../../../ecommerce/get-started-ecommerce/basic-payment-forms/paypal-basic-payment-forms.md)
{% endcontent-ref %}

See SiteBuilder to install a plug and play, themed Form Layout for your payment Form:

{% content-ref url="broken-reference/" %}
[broken-reference](broken-reference/)
{% endcontent-ref %}

And set your Form to use it with the layout parameter.

See the Forms Reference for creating your own Layout:

{% content-ref url="../../../cms/forms/forms-reference.md" %}
[forms-reference.md](../../../cms/forms/forms-reference.md)
{% endcontent-ref %}

## Step 10) Optionally, set your Basic Payment Form to Allow Users to Choose How Much they Pay

By default, the Form will charge the minimum amount, but for some use cases like donations or invoices, you may want to allow them to pay more:

{% content-ref url="../../../ecommerce/get-started-ecommerce/basic-payment-forms/steps-to-allow-user-to-decide-amount-they-will-pay.md" %}
[steps-to-allow-user-to-decide-amount-they-will-pay.md](../../../ecommerce/get-started-ecommerce/basic-payment-forms/steps-to-allow-user-to-decide-amount-they-will-pay.md)
{% endcontent-ref %}
