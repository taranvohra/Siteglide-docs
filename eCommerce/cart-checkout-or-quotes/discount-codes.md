---
title: Discount Codes Layout
slug: whi0-
createdAt: 2021-02-19T10:55:07.000Z
updatedAt: 2024-03-18T16:01:47.001Z
---

This Article explains how to output a Discount Codes Layout in either Basic Payment Form, Cart, Checkout or Subscription Layouts

# Introduction

Discount Codes allow your Client to provide special offers to their customers.

&#x20;You can learn how to [set up Discount Codes in the Admin](https://help.siteglide.com/article/188-products-attributes) here.

&#x20;The role of a Discount Code Layout is to give the customer an opportunity to enter and apply a Discount Code on your Site. Additionally, once a code is applied, the Layout will give the customer information about how their code has been applied along with any terms and conditions, and the opportunity to remove the code.

&#x20;This Article will explain how you can include a Discount Codes Layout in either your:

*   Cart wrapper.liquid file

*   Checkout Form Layout (Discount Code Layouts for the Cart and Checkout will have the same syntax).

*   Basic Payment Form Layout - This will have slightly different syntax due to the unique properties of Basic Payment Forms, but we'll cover this below.

*   Subscription Form Layout - This will have slightly special considerations because the discount has the potential to be applied to all invoices for a specified number of months. It's also possible to use Subscription Discount Codes to take 100% off the price giving a free trial.&#x20;

Once a customer uses the button in the Layout to successfully add a Discount Code, this will be stored in their session alongside any Cart Data. We'll store one code at a time for each payment type, with Basic Payment Forms storing their codes in `{{context.session.basic_payment_discount}}`, Cart saving its codes in `{{context.session.cart_discount}}` and Subscriptions saving their codes in `{{context.session.subscription_discount}}`.

When a customer completes a Payment Form, the Server-side checks will apply the code and reduce the amount they are charged. This means your Site will be secure and safe against malicious users choosing their own discounts.

# Step 1 - Including the Layout inside the Cart, Checkout, Basic Payment Form or Subscription Form Layout

The screenshot below shows how the Discount Code Layout can be nested inside the Cart. However, step 1 also applies in all kinds of Layout.

![](https://downloads.intercomcdn.com/i/o/199477696/a362c3c7c59e264ce4041584/image.png)

## 1a - Add your Layout

The following Liquid will add the Layout:

```liquid
{% raw %}
{% include 'ecommerce/discount_code'
   layout: "cart/default" 
%}
{% endraw %}
```

The only parameter you'll need will be `layout` which refers to the file name of the Layout. We'll look at where to create the Layout files in Step 2.&#x20;

## 1b - Optional - Adding Support for Refreshing Layout instead of whole Page

In order to better support adding Discount Code Layouts on Forms, we've added the option to reload just the Layout, instead of the whole Page. The main benefit of this is that Users will not have to refill their form data after adding a Discount Code. We'll discuss this more in Step 3) b)

For now, you can add the data-attribute `data-s-e-refresh-layout-discount-code` to the element which serves as a wrapper for your Layout e.g.

```liquid
{% raw %}
<div data-s-e-refresh-layout-discount-code>
{% include 'ecommerce/discount_code', layout: "cart/default" %}
</div>
{% endraw %}
```

&#x20;In a Cart Layout, you may also wish to set prices to automatically update when the discount code is added.&#x20;

You can add the following data-attributes:

*   `data-s-e-live-cart-currency` - the element will be filled dynamically with the Cart currency when the Layout refreshes

*   `data-s-e-live-cart-total` - the element will be filled dynamically with the updated Cart Total Price.

e.g.

```liquid
{% raw %}
<p class="text-uppercase"><strong>TOTAL PRICE:</strong> 
<span data-s-e-live-cart-currency></span>
<span data-s-e-live-cart-total>
{% include 'ecommerce/price_total'
            format_type: 'formatted' -%}</span></p>
{% endraw %}
```

## Related Layout Development Docs

*   [Developing Cart Layouts](https://developers.siteglide.com/cart-layouts)

*   [Checkout Tutorial](https://help.siteglide.com/article/163-how-to-set-up-a-shopping-cart-and-guest-checkout-tutorial)

*   [Basic Payment Form Tutorial](https://developers.siteglide.com/basic-payment-forms-tutorial)

# Step 2 - Create Layout Files or Choose the Discount Code Layout

A Discount Code Layout will typically contain:

*   An input field for the customer to enter a discount code

*   A button which allows them to submit the code

*   A button which allows them to remove a code (if perhaps the code is no longer valid and blocking payment).

*   Feedback to the user regarding successful and unsuccessful attempts to apply their discount code.

*   Essential HTML, JavaScript and Liquid which controls functionality

## File Structure

Discount Code Layouts will be stored here, inside: `layouts/modules/module_14/discount_code`

You'll just need a single Liquid file with the same name as your Layout. Optionally, you can use folders to organise Layouts of different types.

![](https://downloads.intercomcdn.com/i/o/275360458/ce153269ea626984e773d50f/image.png)

If you haven't already, make sure your layout parameter in the Liquid tag matches the name of your Layout File. Any custom folders like 'cart/' should also be added to the layout parameter path.

&#x20;As there are subtle differences in implementation depending on the type of payment, we've created three different default layouts to help you get started:

*   "basic\_payment/default"

*   "cart/default"

*   "subscription/default"

&#x20;For steps 3  and onwards, you may find it easier to copy and edit the code from the default Layout, but we'll break this down into steps here so you can see all the elements you'll need.&#x20;

# Step 3 - Add HTML and Liquid to allow a Customer to enter a Discount Code

![](https://downloads.intercomcdn.com/i/o/275363970/4d7bd514586bd8af7a6a810a/image.png)

## 3a - Add an \<input> element and \<label>

```liquid
{% raw %}
<label class="mb-3" for="s_e_discount_code">Discount Code</label>
<input class="form-control" 
       id="s_e_discount_code" 
       data-s-e-discount-code {% if discount_code != blank %} 
       value="{{discount_code}}" 
       readonly="true"{%- endif -%}>
{% endraw %}
```

*HTML Attributes Explained:*

| **Code**                                                                                                                                                                        | **Purpose**                                                                                                                                                                     | **Required** |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ |
| data-s-e-discount-code                                                                                                                                                          | Attribute should be added to input field                                                                                                                                        | Yes          |
| value="{%- if discount\_code != blank -%}{{discount\_code}}{%- endif -%}"&#xA;&#xA;or &#xA;&#xA;{% if discount\_code != blank %}value="{{discount\_code}}" readonly{% endif -%} | If a code is already successfully added, it will be autofilled.&#x20;or&#x20;Any successful code is autofilled and the current field value is readonly until removed in step b) | One of these |


3b - Add an "Apply" button
--------------------------

When adding the 'Apply' button, you can customise how the JavaScript will behave on successful and unsuccessful attempts to add a Discount.

&#x20;In the examples below, we'll show the basic options recommended for different types of Layout, then explain the full range of options you have for JavaScript behaviour.

### Applying to a Cart Layout:

```javascript
<button class="btn btn-primary sg-btn sg-btn-primary" 
        id="s_e_discount_apply" 
        onclick="s_e_cart_discount_code(
{
  spend: '{{context.exports.cart_base_price.data | json}}',
  reload: true
  
}
)">Apply Code</button>
```

### Applying to a Checkout Form Layout:

```javascript
<button class="btn btn-primary sg-btn sg-btn-primary" 
        id="s_e_discount_apply" 
        onclick="s_e_cart_discount_code(
{
  spend: '{{context.exports.cart_base_price.data | json}}',
  reload: false
}
)">Apply Code</button
```

### Applying to a Basic Payment Form Layout:

```javascript

<button class="btn btn-primary sg-btn sg-btn-primary " 
        id="s_e_discount_apply" 
        onclick="s_e_cart_discount_code(
{ 
  spend: document.querySelector('#s_e_amount').value,
  reload: false
}
);">Apply Code</button>
```

### Applying to a Subscription Layout:

{% hint style="info" %}
## Note

We recommend hiding the apply button after the Subscription Order has been created and the Discount Code has been redeemed. See Subscription Specific Instructions.
{% endhint %}

```javascript
<button class="btn btn-primary sg-btn sg-btn-primary" 
        id="s_e_discount_apply" 
        onclick="s_e_cart_discount_code(
{
  spend: {{spend}},
  reload: false
}
);">Apply Code</button>
```

### 3c - JavaScript Options Explained

&#x20;At this stage, you have a choice about whether you'd like the whole Page to reload after a successful Discount Code is added, or whether you'd like to only reload the Discount Code Layout itself.

We'd strongly recommend that for Layouts on Forms that you set `reload: false` as this will prevent the User having to re-enter their Form data, and will preserve any custom amount chosen on the Basic Payment Form.

Note also that the value of `spend` will be different for Basic Payment Forms:

*   Basic Payment Forms store the `spend` value in `document.querySelector('#s_e_amount').value` - as this can be dynamically changed by JavaScript, there is no Liquid value for it.

*   Cart and Checkout Forms can use the Liquid value: `'{{context.exports.cart_base_price.data | json}}'`

*   Subscriptions store the spend in `{{spend}}`

| **Option**                                                                                                                               | **Required / Default**                                                                                                                                                                                              | **Notes**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ---------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| spend:&#x20;*   document.querySelector('#s\_e\_amount').value

*   '{{context.exports.cart\_base\_price.data \| json}}'

*   '{{spend}}' | Required - no default                                                                                                                                                                                               | Basic Payment Forms use&#xA;spend: document.querySelector('#s\_e\_amount').value&#xA;- as this can be dynamically changed by JavaScript, there is no Liquid value for it.&#xA;Cart and Checkout Forms can use the Liquid value:spend: '{{context.exports.cart\_base\_price.data \| json}}'                                                                                                                                                                                                                         |
| reload:&#x20;*   true

*   false                                                                                                         | default: true                                                                                                                                                                                                       | Setting true will refresh the entire Page.&#x20;Setting false will refresh the Discount Code Layout only. &#xA;&#xA;We'd strongly recommend that for Layouts on Forms that you set reload: false as this will prevent the User having to re-enter their Form data, and will preserve any custom amount chosen on the Basic Payment Form.&#x20;**If you select **`false`**, you must add the data-attribute data-s-e-refresh-layout-discount-code to the element which wraps around the Layout&#xA;see Step 1) b)** |
| error\_cb:&#x20;*   custom JavaScript function name (don't call the function yet!)&#xA;&#xA;error\_cb: myErrorFunction                   | default:&#xA;*   A JavaScript alert message will display the error.&#xA;&#xA;                                                                                                                                       | For arguments and how to customise your own function, head to step 6.                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| success\_cb:&#x20;*   custom JavaScript function name (don't call the function yet!)&#xA;&#xA;success\_cb: mySuccessFunction             | default:&#x20;*   Depending on the reload option, will reload the Page or Layout

*   If reload is false and the Payment Type is Checkout, will update the total Price by running the s\_e\_cart\_update\_prices(); | For arguments and how to customise your own function, head to step 7.                                                                                                                                                                                                                                                                                                                                                                                                                                              |

# Step 4 - Add HTML and Liquid to allow a Customer to Remove a Discount Code

You can optionally add a button to the Layout which will allow the customer to remove a Discount Code that has already been applied.&#x20;

```javascript
{%- if discount_code != blank -%}

<button class="btn btn-danger" 
        id="s_e_discount_remove" 
        onclick="s_e_cart_discount_code_remove(
{
reload: false
}
)">Remove Code</button>

{% endif %}
```

The Liquid IF statement helps make sure the button is only displayed if there is a code present to be removed.&#x20;

The JavaScript function will make the button functional.

| **Option**                       | **Required / Default**                                                                                      | **Notes**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| reload:&#x20;*   true

*   false | default: true                                                                                               | Setting true will refresh the entire Page.&#x20;Setting false will refresh the Discount Code Layout only. &#xA;&#xA;We'd strongly recommend that for Layouts on Forms that you set reload: false as this will prevent the User having to re-enter their Form data, and will preserve any custom amount chosen on the Basic Payment Form.&#x20;If you select false, you must add the data-attribute data-s-e-refresh-layout-discount-code to the element which wraps around the Layout&#xA;see Step 1) b)
---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| success\_cb:                     | Default:&#x20;Depending on how you set the refresh setting, will refresh the Page or the Layout. &#xA;&#xA; | For arguments and how to customise your own function, head to step 8.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |

*Why is this helpful?*
Although we check Discount Codes are valid when they are added, there are cases where the code is no longer valid by the time the customer reaches the Checkout, for example:

*   The User may have adjusted the quantity of items in the Cart, causing the spending amount to drop lower than the minimum payment allowed by the Discount Code.

*   The Code may have been close to expiry.

Adding a "remove" button gives the User a clear way to solve any problems stopping them from completing their purchase.

{% hint style="info" %}
## Note

You cannot remove a Subscription Discount Code after the Subscription Order has been created and the Discount redeemed. See Subscription Specific Instructions.
{% endhint %}

# Step 5 - Add HTML and Liquid to give the customer feedback

![](https://downloads.intercomcdn.com/i/o/275390532/8012bc29bd3d48d929009382/image.png)

## 5a - Displaying the Discount Amount

On Page refresh (or if you've chosen `reload: false` on Layout refresh), after a successful Code is applied, the following Liquid will explain the minimum spend needed and the discount available.

Depending on where your Layout is, different syntax may be needed to fetch the currency to display.

### On Cart and Checkout Layouts:

```liquid
{% raw %}
{% if discount_code != blank -%}
<p>Discount: 
    <span style="color: red;">
        -{{context.exports.cart_currency.data}}
        {%- include 'modules/siteglide_ecommerce/ecommerce/price_formatter'
                     price_data: discount_amount -%}
                     </span>
                     </p>
                     {% endif %}
{% endraw %}
```

### On Basic Payment Layouts:

```liquid
{% raw %}
{%- if discount_code != blank -%}
<p>Discount: 
    <span style="color: red;">
        -{% include 'ecommerce/basic_payment_currency'
                     format: 'symbol' %}
                     {%- include 'modules/siteglide_ecommerce/ecommerce/price_formatter'
                                  price_data: discount_amount -%}
                                  </span>
                                  </p>
{%- endif -%}
{% endraw %}
```

### On Subscription Layouts:

&#x20;On Subscription Layouts it is important to know whether or not the Subscription Order has been created, if it has, then the Discount will already be redeemed. The difference in display needs to account for the fact that a redeemed discount is time-limited.&#x20;

For both situations, we can use the fields inside the discount variable to access details on the Discount.&#x20;

*Before the Subscription Order is Created
*At this stage, we can use general details of the discount which is applied, but not yet redeemed, from the `this` object.

```liquid
{% raw %}
{%- if discount_code != blank -%}
  <p>Discount: 
  <span style="color: red;">
    -{{this.price.currency_symbol}}
    {%- include 'modules/siteglide_ecommerce/ecommerce/price_formatter'
                 price_data: discount_amount -%}
                 </span>
  every 
    {% if this['Interval Count'] != "1" %}
      {{this['Interval Count']}} {{this['Interval']}}
    {% else %}
      {{this['Interval'] | pluralize: 1}}
    {% endif %}
    for {{discount.number_of_months_to_discount}} 
    {% if discount.number_of_months_to_discount == 1 %}
      month
    {% else %}
      months
    {% endif %}
  </p>
{%- endif -%}
{% endraw %}
```

*After the Subscription Order is Created and the Discount Redeemed
*At this stage, we can use details of the actual discount code stored against the Subscription Order. As this is time limited, we may also wish to give details of how much longer the Discount will be active for and the specific Subscription Order will provide these details.

```liquid
{% raw %}
{%- if discount_code != blank -%}
  <p>Discount redeemed: 
    <span style="color: red;">
      {{this.price.currency_symbol}}
      {%- include 'modules/siteglide_ecommerce/ecommerce/price_formatter'
                   price_data: discount_amount -%}
    </span> saved every 
    {% if subscription_order['Plan Interval Count'] != "1" %}
      {{subscription_order['Plan Interval Count']}}
      {{subscription_order['Plan Interval']}}
    {% else %}
      {{subscription_order['Plan Interval'] | pluralize: 1}}
    {% endif %}
    for {{discount.number_of_months_to_discount}} 
    {% if discount.number_of_months_to_discount == 1 %}
      month
    {% else %}
      months
    {% endif %}
    until {{subscription_order['Plan Discount Ends At'] | date: "%d/%m/%y"}} 
  </p>
  <p>Total Due: {{this.price.currency_symbol}}
    {%- include 'modules/siteglide_ecommerce/ecommerce/price_formatter'
                 price_data: discount.total_remaining -%}
                 </p>
{%- endif -%}
{% endraw %}
```

## 5b - Displaying the Minimum Spend

The following code can be used to display the minimum spend needed to keep using the discount:

### On Cart and Checkout Layouts:

```liquid
{% raw %}
{%- if discount_code != blank and discount_minimum -%}
<p class="mt-4">
    This code will only be valid on Cart orders worth over: 
    {{context.exports.cart_currency.data}}
    {%- include 'modules/siteglide_ecommerce/ecommerce/price_formatter'
                 price_data: discount_minimum -%}</p>
{%- endif -%}
{% endraw %}
```

### On Basic Payment Layouts:

The following code can be used to display the minimum spend needed to keep using the discount:

```liquid
{% raw %}
{%- if discount_code != blank and discount_minimum -%}
<p class="mt-4">
    This code will only be valid on orders over: 
    {% include 'ecommerce/basic_payment_currency'
                format: 'symbol' %}
                {%- include 'modules/siteglide_ecommerce/ecommerce/price_formatter'
                             price_data: discount_minimum -%}
                             </p>
{%- endif -%}
{% endraw %}
```

### On Subscription Layouts

&#x20;It's probably only really necessary to display the minimum spend before the Subscription Order is created and the Discount redeemed. Once the discount is redeemed, the amount spent will be fixed.&#x20;

```liquid
{% raw %}
{%- if discount_code != blank and discount_minimum -%}
  <p class="mt-4">
    This code will only be valid on orders over: 
    {{this.price.currency_symbol}}
    {%- include 'modules/siteglide_ecommerce/ecommerce/price_formatter'
                 price_data: discount_minimum -%}
                 </p>
{%- endif -%}
{% endraw %}
```

## 5c - Displaying a Message when the Discount Maximum is Reached on Basic Payment Forms, Cart and Checkout

This code will display a message if the minimum spend is not set strictly enough and the resulting payment total is below that allowed by the Payment Gateway.

```liquid
{% raw %}
{%- if discount_saving_maximum_reached == true -%}
<!-- Message here -->
<p class="mt-4">
    Minimum transaction value reached. 
    To make the most of your discount, try adding another item to your Cart.</p>
{%- endif -%}
{% endraw %}
```

`discount_saving_maximum_reached` will always return false for Subscriptions and these allow any size of Discount (controlled only by the Partner and Client setting Minimum Spend values on each Discount Code in the Admin.) Therefore, it's not necessary to add this code to a Discount Code Layout for a Subscription.

Read more about the [Discount Maximum requirement](https://help.siteglide.com/article/168-faq-ecommerce-discount-codes-what-if-the-discount-is-100-or-more-of-the-total-order-price)

## Summary of Available fields when building your Discount Code Layout:

*   `discount_code` is a variable which contains the Discount Code successfully applied after page refresh

*   `discount_minimum` is a variable which contains the minimum spend needed for this Discount Code to be valid.

*   `discount_amount` is a variable which stores the calculated saving on the current Cart value.

*   `{{context.exports.cart_currency.data}}` will output the currency symbol on Cart and Checkout Layouts

*   `{% include 'ecommerce/basic_payment_currency', format: 'symbol' %}` will output the currency symbol on Basic Payment Layouts

*   `{%- include 'modules/siteglide_ecommerce/ecommerce/price_formatter', price_data: discount_minimum -%}` You can use this Liquid tag to format any Liquid price variable with the correct decimalisation. To use, set the `price_data` parameter to the variable you wish to format.

*   `discount_saving_maximum_reached` - if `true`, the Minimum Amount for the Discount Code has not been set strictly enough and the total Payment Due is below that allowed by the Payment Gateway. You can use this to display a warning message that it has not been possible to apply the full discount.

*   For Subscriptions, your Layout will inherit the variables of the Layouts it's nested within- meaning it will inherit variables from the Subscription Detail Page, then the Subscription Form. See details of these objects [here](https://developers.siteglide.com/detail-layout#jo-step-5-available-fields). e.g. {{this.price.currency\_symbol}}

# Step 6 - Optional - Add JavaScript to handle errors

There are lots of reasons why the customer may enter a code but be refused a discount. For example, the code may have expired, or the Cart's value may not be above the minimum spend.

![](https://downloads.intercomcdn.com/i/o/200379256/5e95bdc674c1504fae6edbfb/image.png)

You can start with the JavaScript function below and make your own changes to decide how these errors are displayed to the customer:

```javascript
<script>
function s_e_discount_error(error) {
console.log(error.type); 
/* an error code which you can use in your logic. */
console.log(error.message); /* A ready-drafted error message */
alert(error.message);
}
</script>
```

As the comments in the example mention, each error returned from a failed discount code will give both a code and a default message. You can choose which one you will use.

Here are the full list:

| **error.type**                | **error.message**                                                                                           | **Notes**                                                                                                                                                                     |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| no\_code                      | Error: This Discount Code does not exist.                                                                   | &#x20;                                                                                                                                                                        |
| expired                       | Error: This Discount Code has expired.                                                                      | &#x20;                                                                                                                                                                        |
| below\_min\_spend={min-spend} | Error: This Discount Code has a minimum spend of {min-spend}                                                | &#x20;                                                                                                                                                                        |
| used\_up                      | This Discount Code has already been used the maximum number of times.                                       | &#x20;                                                                                                                                                                        |
| incorrect\_type               | Error: This Discount Code does not apply to this kind of payment. It may apply in another area of the Site. | By default, Discount Codes are only redeemable on Cart / Checkout flow. You can change this for an individual code in the Admin using the "Valid on Payment Form Type" field. |

If you want to change the message, you can use logic to display different messages using the error code:

```javascript
<script>
function myErrorFunction(error) {
if (error.type == 'no_code' ) {
alert('Better luck next time. Discount Code not found!');
} elsif (error.type.indexOf('below_min_spend=') != -1 ) {
//As the below min_spend code can vary depending on the value, this code checks for the substring.
alert('You'll need to spend more before using this code.');
}

</script>
```

Once you've created your function, use the `error_cb` option in step 3) b) and pass it your function name. e.g. `error_cb: myErrorFunction`

# Step 7 - Optional - Customise the JavaScript behaviour when a code is successfully added

Setting `reload` to either `true` or `false` in the `s_e_cart_discount_code` function will both effectively refresh your Discount Code Layout and the Liquid will update with new values, so most use-cases will not need a custom success function. However, if you do need to make changes, you can use the function below as a starting point:

```javascript
function mySuccessFunction(reload = true, discount, payment_type, refreshed_discount_layout) {
if(reload == true) {
window.location.reload();
} else if (refreshed_discount_layout) {
var slot = document.querySelector('[data-s-e-refresh-layout-discount-code]');
slot.innerHTML = refreshed_discount_layout;
if(payment_type == 'Checkout') {
s_e_cart_update_prices();
}
}
}
```

## Available arguments:

| **Argument**                  | **Example**                                                                     | **Purpose**                                                                                             |
| ----------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| reload&#xA;&#xA;default: true | &#x20;                                                                          | The value of the reload setting passed into the function. Defaults to true for backwards compatibility. |
| discount                      | &#x20;                                                                          | An object containing details of the newly applied discount code.                                        |
| payment\_type                 | 'Checkout' or 'Basic Payment'                                                   | Can be used in logic                                                                                    |
| refreshed\_discount\_layout   | A DOMstring containing the HTML generated by the refreshed Discount Code Layout | This can be used to refresh only the Discount Code Layout, if you choose.                               |

Once you've created your function, use the `success_cb` option in step 3) b) and pass it your function name. e.g. `success_cb: mySuccessFunction`

# Step 8 - Optional - Customise the JavaScript behaviour when a code is successfully removed

Setting `reload` to either `true` or `false` in the `s_e_cart_discount_code` function will both effectively refresh your Discount Code Layout and the Liquid will update with new values, so most use-cases will not need a custom success function. However, if you do need to make changes, you can use the function below as a starting point:

```javascript
function mySuccessFunction(reload = true, payment_type = 'Checkout', refreshed_discount_layout) { 
if(reload == true) { 
window.location.reload(); 
} else if (refreshed_discount_layout) { 
var slot = document.querySelector('[data-s-e-refresh-layout-discount-code]'); 
slot.innerHTML = refreshed_discount_layout; 
if(payment_type == 'Checkout') { 
s_e_cart_update_prices(); 
} 
} 
}
```

## Available arguments:

| **Argument**                  | **Example**                                                                     | **Purpose**                                                                                             |
| ----------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| reload&#xA;&#xA;default: true | &#x20;                                                                          | The value of the reload setting passed into the function. Defaults to true for backwards compatibility. |
| payment\_type                 | 'Checkout' or 'Basic Payment'                                                   | Can be used in logic                                                                                    |
| refreshed\_discount\_layout   | A DOMstring containing the HTML generated by the refreshed Discount Code Layout | This can be used to refresh only the Discount Code Layout, if you choose.                               |

Once you've created your function, use the `success_cb` option in step 3) b) and pass it your function name. e.g. `success_cb: mySuccessFunction`

# Specific Instructions for Subscriptions

{% hint style="success" %}
## Note

We recommend for Subscriptions to add some logic checking whether a Subscription Order has already been created and if so, to hide the apply button. This is because once the Subscription Order is created- any Discount Code already applied will be redeemed.&#x20;
{% endhint %}

At this point it's not possible to apply or change the Discount Code, only display details of the Order that's active. The purpose of the Form at this point is actually to allow Users to edit their payment details only.&#x20;

```liquid
{% raw %}
{% if subscription_discount_already_redeemed == true %}

<!-- Insert code here - the Discount has already been redeemed against the Subscription Order-->
{% endif %}
{% endraw %}
```

You could add this logic around the whole Layout (as in the default Layout), or just around individual components. For the sake of clarity, in the "subscription/default" Layout, we've opted to wrap the logic around the whole Layout, creating two distinctly separate blocks of Liquid for before and after redemption.&#x20;

You can also add the statement to check if the Discount will apply to the next invoice or if the Discounted period of months is over.

```liquid
{% raw %}
{% if rate_still_discounted == true %}
{% endif %}
{% endraw %}
```

## Related Articles

*   [eCommerce - Discount Codes](https://help.siteglide.com/article/177-ecommerce-discount-codes) - Adding and editing Discount Codes in the Siteglide Admin

*   [eCommerce - Discount Codes - How to avoid low prices which cost Payment Gateway Charges](https://help.siteglide.com/article/168-faq-ecommerce-discount-codes-what-if-the-discount-is-100-or-more-of-the-total-order-price)




