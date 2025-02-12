# Discount Codes Layout

This Article explains how to output a Discount Codes Layout in either Basic Payment Form, Cart, Checkout or Subscription Layouts

## Introduction

Discount Codes allow your Client to provide special offers to their customers.

You can learn how to [set up Discount Codes in the Admin](/ecommerce/get-started-ecommerce/cart-checkout-and-quotes/managing-products/managing-attributes.md) here.

The role of a Discount Code Layout is to give the customer an opportunity to enter and apply a Discount Code on your Site. Additionally, once a code is applied, the Layout will give the customer information about how their code has been applied along with any terms and conditions, and the opportunity to remove the code.

This Article will explain how you can include a Discount Codes Layout in either your:

* Cart wrapper.liquid file
* Checkout Form Layout (Discount Code Layouts for the Cart and Checkout will have the same syntax).
* Basic Payment Form Layout - This will have slightly different syntax due to the unique properties of Basic Payment Forms, but we'll cover this below.
* Subscription Form Layout - This will have slightly special considerations because the discount has the potential to be applied to all invoices for a specified number of months. It's also possible to use Subscription Discount Codes to take 100% off the price giving a free trial.

Once a customer uses the button in the Layout to successfully add a Discount Code, this will be stored in their session alongside any Cart Data. We'll store one code at a time for each payment type, with Basic Payment Forms storing their codes in `{{context.session.basic_payment_discount}}`, Cart saving its codes in `{{context.session.cart_discount}}` and Subscriptions saving their codes in `{{context.session.subscription_discount}}`.

When a customer completes a Payment Form, the Server-side checks will apply the code and reduce the amount they are charged. This means your Site will be secure and safe against malicious users choosing their own discounts.

## Step 1 - Including the Layout inside the Cart, Checkout, Basic Payment Form or Subscription Form Layout

The screenshot below shows how the Discount Code Layout can be nested inside the Cart. However, step 1 also applies in all kinds of Layout.

### 1a - Add your Layout

The following Liquid will add the Layout:

```liquid
{% raw %}
{% include 'ecommerce/discount_code'
   layout: "cart/default" 
%}
{% endraw %}
```

The only parameter you'll need will be `layout` which refers to the file name of the Layout. We'll look at where to create the Layout files in Step 2.

### 1b - Optional - Adding Support for Refreshing Layout instead of whole Page

In order to better support adding Discount Code Layouts on Forms, we've added the option to reload just the Layout, instead of the whole Page. The main benefit of this is that Users will not have to refill their form data after adding a Discount Code. We'll discuss this more in Step 3) b)

For now, you can add the data-attribute `data-s-e-refresh-layout-discount-code` to the element which serves as a wrapper for your Layout e.g.

```liquid
<div data-s-e-refresh-layout-discount-code>
{% raw %}
{% include 'ecommerce/discount_code', layout: "cart/default" %}
{% endraw %}
</div>

```

In a Cart Layout, you may also wish to set prices to automatically update when the discount code is added.

You can add the following data-attributes:

* `data-s-e-live-cart-currency` - the element will be filled dynamically with the Cart currency when the Layout refreshes
* `data-s-e-live-cart-total` - the element will be filled dynamically with the updated Cart Total Price.

e.g.

```liquid
<p class="text-uppercase"><strong>TOTAL PRICE:</strong> 
<span data-s-e-live-cart-currency></span>
<span data-s-e-live-cart-total>
{% include 'ecommerce/price_total'
            format_type: 'formatted' -%}</span></p>


```

### Related Layout Development Docs

* [Developing Cart Layouts](/ecommerce/get-started-ecommerce/cart-checkout-and-quotes/cart/cart-layouts.md)
* [Checkout Tutorial](/eCommerce/get-started-ecommerce/cart-checkout-and-quotes/steps-to-implement-a-guest-checkout-flow.md)
* [Basic Payment Form Tutorial](/eCommerce/get-started-ecommerce/basic-payment-forms/basic-payments.md)

## Step 2 - Create Layout Files or Choose the Discount Code Layout

A Discount Code Layout will typically contain:

* An input field for the customer to enter a discount code
* A button which allows them to submit the code
* A button which allows them to remove a code (if perhaps the code is no longer valid and blocking payment).
* Feedback to the user regarding successful and unsuccessful attempts to apply their discount code.
* Essential HTML, JavaScript and Liquid which controls functionality

### File Structure

Discount Code Layouts will be stored here, inside: `layouts/modules/module_14/discount_code`

You'll just need a single Liquid file with the same name as your Layout. Optionally, you can use folders to organise Layouts of different types.

If you haven't already, make sure your layout parameter in the Liquid tag matches the name of your Layout File. Any custom folders like 'cart/' should also be added to the layout parameter path.

As there are subtle differences in implementation depending on the type of payment, we've created three different default layouts to help you get started:

* "basic\_payment/default"
* "cart/default"
* "subscription/default"

For steps 3 and onwards, you may find it easier to copy and edit the code from the default Layout, but we'll break this down into steps here so you can see all the elements you'll need.

## Step 3 - Add HTML and Liquid to allow a Customer to enter a Discount Code

### 3a - Add an \<input> element and \<label>

```liquid
<label class="mb-3" for="s_e_discount_code">Discount Code</label>
<input class="form-control" 
       id="s_e_discount_code" 
       data-s-e-discount-code 

{% raw %}
{% if discount_code != blank %} 
       value="{{discount_code}}" 
       readonly="true"{%- endif -%}
{% endraw %}


```

_HTML Attributes Explained:_

| **Code**                             | **Purpose**                              | **Required** |
| ------------------------------------ | ---------------------------------------- | ------------ |
| data-s-e-discount-code               | Attribute should be added to input field | Yes          |
| value="{% raw %}{%- if discount_code != blank -%}{{discount_code}}{%- endif -%}{% endraw %}" <br> <br> or <br> <br> {%raw %}{% if discount_code != blank %}value="{{discount_code}}" readonly{% endif -%}{% endraw %} | If a code is already successfully added, it will be autofilled. <br> <br> or <br> <br> Any successful code is autofilled and the current field value is readonly until removed in step b) | One of these |


### 3b - Add an "Apply" button

When adding the 'Apply' button, you can customise how the JavaScript will behave on successful and unsuccessful attempts to add a Discount.

In the examples below, we'll show the basic options recommended for different types of Layout, then explain the full range of options you have for JavaScript behaviour.

#### Applying to a Cart Layout:

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

#### Applying to a Checkout Form Layout:

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

#### Applying to a Basic Payment Form Layout:

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

#### Applying to a Subscription Layout:

{% hint style="info" %}
**Note**

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

#### 3c - JavaScript Options Explained

At this stage, you have a choice about whether you'd like the whole Page to reload after a successful Discount Code is added, or whether you'd like to only reload the Discount Code Layout itself.

We'd strongly recommend that for Layouts on Forms that you set `reload: false` as this will prevent the User having to re-enter their Form data, and will preserve any custom amount chosen on the Basic Payment Form.

Note also that the value of `spend` will be different for Basic Payment Forms:
* Basic Payment Forms store the `spend` value in `document.querySelector('#s_e_amount').value` - as this can be dynamically changed by JavaScript, there is no Liquid value for it.
* Cart and Checkout Forms can use the Liquid value: `'{{context.exports.cart_base_price.data | json}}'`
* Subscriptions store the spend in `{{spend}}`

| **Option**                                              | **Required / Default** | **Notes** |
| ------------------------------------------------------- | ---------------------- | --------- |
| spend: <br> - `document.querySelector('#s\_e\_amount').value` <br> - `{% raw %}{{context.exports.cart_base_price.data \| json}}{% endraw %}` <br> - `{% raw %}{{spend}}{% endraw %}`  | Required - no default  | Basic Payment Forms use spend: `document.querySelector('#s_e_amount').value` <br> - as this can be dynamically changed by JavaScript, there is no Liquid value for it. <br> <br> Cart and Checkout Forms can use the Liquid value: <br> <br> spend: `{% raw %}{{context.exports.cart_base_price.data \| json}}{% endraw %}` |
| reload: <br> - true <br> - false | default: true | Setting true will refresh the entire Page. <br> <br> Setting false will refresh the Discount Code Layout only. <br> <br> We'd strongly recommend that for Layouts on Forms that you set reload: false as this will prevent the User having to re-enter their Form data, and will preserve any custom amount chosen on the Basic Payment Form. <br> <br> If you select `false`, you must add the data-attribute `data-s-e-refresh-layout-discount-code` to the element which wraps around the Layout <br> see Step 1) b) |
| error_cb: <br> - custom JavaScript function name (don't call the function yet!) <br> - success_cb: mySuccessFunction | default: <br> <br> - Depending on the reload option, will reload the Page or Layout <br> - If reload is false and the Payment Type is Checkout, will update the total Price by running the `s_e_cart_update_prices()`; | For arguments and how to customise your own function, head to step 7. |

## Step 4 - Add HTML and Liquid to allow a Customer to Remove a Discount Code

You can optionally add a button to the Layout which will allow the customer to remove a Discount Code that has already been applied.

```liquid
{% raw %}
{%- if discount_code != blank -%}
  <button class="btn btn-danger" id="s_e_discount_remove" onclick="s_e_cart_discount_code_remove(
    {
      reload: false
    }
  )">
    Remove Code
  </button>
{% endif %}
{% endraw %}
```

The Liquid IF statement helps make sure the button is only displayed if there is a code present to be removed.

The JavaScript function will make the button functional.

| **Option**      | **Required / Default** | **Notes** |
| --------------- | ---------------------- | --------- |
| reload: <br> - true <br> - false | default: true | Setting true will refresh the entire Page. <br> <br> Setting false will refresh the Discount Code Layout only. <br> <br> We'd strongly recommend that for Layouts on Forms that you set reload: false as this will prevent the User having to re-enter their Form data, and will preserve any custom amount chosen on the Basic Payment Form. <br> <br> If you select `false`, you must add the data-attribute `data-s-e-refresh-layout-discount-code` to the element which wraps around the Layout <br> see Step 1) b) |
| success_cb: | Default: <br> <br> Depending on how you set the refresh setting, will refresh the Page or the Layout. | For arguments and how to customise your own function, head to step 8. |


_Why is this helpful?_ Although we check Discount Codes are valid when they are added, there are cases where the code is no longer valid by the time the customer reaches the Checkout, for example:

* The User may have adjusted the quantity of items in the Cart, causing the spending amount to drop lower than the minimum payment allowed by the Discount Code.
* The Code may have been close to expiry.

Adding a "remove" button gives the User a clear way to solve any problems stopping them from completing their purchase.

{% hint style="info" %}
**Note**

You cannot remove a Subscription Discount Code after the Subscription Order has been created and the Discount redeemed. See Subscription Specific Instructions.
{% endhint %}

## Step 5 - Add HTML and Liquid to give the customer feedback

### 5a - Displaying the Discount Amount

On Page refresh (or if you've chosen `reload: false` on Layout refresh), after a successful Code is applied, the following Liquid will explain the minimum spend needed and the discount available.

Depending on where your Layout is, different syntax may be needed to fetch the currency to display.

#### On Cart and Checkout Layouts:

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

#### On Basic Payment Layouts:

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

#### On Subscription Layouts:

On Subscription Layouts it is important to know whether or not the Subscription Order has been created, if it has, then the Discount will already be redeemed. The difference in display needs to account for the fact that a redeemed discount is time-limited.

For both situations, we can use the fields inside the discount variable to access details on the Discount.

_Before the Subscription Order is Created_  
At this stage, we can use general details of the discount which is applied, but not yet redeemed, from the `this` object.

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

_After the Subscription Order is Created and the Discount Redeemed_  
At this stage, we can use details of the actual discount code stored against the Subscription Order. As this is time limited, we may also wish to give details of how much longer the Discount will be active for and the specific Subscription Order will provide these details.

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

### 5b - Displaying the Minimum Spend

The following code can be used to display the minimum spend needed to keep using the discount:

#### On Cart and Checkout Layouts:

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

#### On Basic Payment Layouts:

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

#### On Subscription Layouts

It's probably only really necessary to display the minimum spend before the Subscription Order is created and the Discount redeemed. Once the discount is redeemed, the amount spent will be fixed.

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

### 5c - Displaying a Message when the Discount Maximum is Reached on Basic Payment Forms, Cart and Checkout

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

Read more about the [Discount Maximum requirement](/eCommerce/get-started-ecommerce/cart-checkout-and-quotes/product-views/discount-selection/minimum-payments.md)

### Summary of Available fields when building your Discount Code Layout:

* `discount_code` is a variable which contains the Discount Code successfully applied after page refresh
* `discount_minimum` is a variable which contains the minimum spend needed for this Discount Code to be valid.
* `discount_amount` is a variable which stores the calculated saving on the current Cart value.
* `{{context.exports.cart_currency.data}}` will output the currency symbol on Cart and Checkout Layouts
* `{% raw %}{% include 'ecommerce/basic_payment_currency', format: 'symbol' %}{% endraw %}` will output the currency symbol on Basic Payment Layouts
* `{% raw %}{%- include 'modules/siteglide_ecommerce/ecommerce/price_formatter', price_data: discount_minimum -%}{% endraw %}` You can use this Liquid tag to format any Liquid price variable with the correct decimalisation. To use, set the `price_data` parameter to the variable you wish to format.
* `discount_saving_maximum_reached` - if `true`, the Minimum Amount for the Discount Code has not been set strictly enough and the total Payment Due is below that allowed by the Payment Gateway. You can use this to display a warning message that it has not been possible to apply the full discount.
* For Subscriptions, your Layout will inherit the variables of the Layouts it's nested within- meaning it will inherit variables from the Subscription Detail Page, then the Subscription Form. See details of these objects [here](/eCommerce/get-started-ecommerce/subscriptions/subscriptions-detail.md#step-5-available-fields). e.g. `{{this.price.currency_symbol}}`

## Step 6 - Optional - Add JavaScript to handle errors

There are lots of reasons why the customer may enter a code but be refused a discount. For example, the code may have expired, or the Cart's value may not be above the minimum spend.

You can start with the JavaScript function below and make your own changes to decide how these errors are displayed to the customer:

```javascript
function s_e_discount_error(error) {
console.log(error.type); 
/* an error code which you can use in your logic. */
console.log(error.message); /* A ready-drafted error message */
alert(error.message);
}
```

As the comments in the example mention, each error returned from a failed discount code will give both a code and a default message. You can choose which one you will use.

Here are the full list:

| **error.type**                | **error.message**                                                                                           | **Notes**                                                                                                                                                                     |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| no\_code                      | Error: This Discount Code does not exist.                                                                   |                                                                                                                                                                               |
| expired                       | Error: This Discount Code has expired.                                                                      |                                                                                                                                                                               |
| below\_min\_spend={min-spend} | Error: This Discount Code has a minimum spend of {min-spend}                                                |                                                                                                                                                                               |
| used\_up                      | This Discount Code has already been used the maximum number of times.                                       |                                                                                                                                                                               |
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

## Step 7 - Optional - Customise the JavaScript behaviour when a code is successfully added

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

### Available arguments:

| **Argument**                | **Example**                                                                     | **Purpose**                                                                                             |
| --------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| reload default: true        |                                                                                 | The value of the reload setting passed into the function. Defaults to true for backwards compatibility. |
| discount                    |                                                                                 | An object containing details of the newly applied discount code.                                        |
| payment\_type               | 'Checkout' or 'Basic Payment'                                                   | Can be used in logic                                                                                    |
| refreshed\_discount\_layout | A DOMstring containing the HTML generated by the refreshed Discount Code Layout | This can be used to refresh only the Discount Code Layout, if you choose.                               |

Once you've created your function, use the `success_cb` option in step 3) b) and pass it your function name. e.g. `success_cb: mySuccessFunction`

## Step 8 - Optional - Customise the JavaScript behaviour when a code is successfully removed

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

### Available arguments:

| **Argument**                | **Example**                                                                     | **Purpose**                                                                                             |
| --------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| reload default: true        |                                                                                 | The value of the reload setting passed into the function. Defaults to true for backwards compatibility. |
| payment\_type               | 'Checkout' or 'Basic Payment'                                                   | Can be used in logic                                                                                    |
| refreshed\_discount\_layout | A DOMstring containing the HTML generated by the refreshed Discount Code Layout | This can be used to refresh only the Discount Code Layout, if you choose.                               |

Once you've created your function, use the `success_cb` option in step 3) b) and pass it your function name. e.g. `success_cb: mySuccessFunction`

## Specific Instructions for Subscriptions

{% hint style="success" %}
**Note**

We recommend for Subscriptions to add some logic checking whether a Subscription Order has already been created and if so, to hide the apply button. This is because once the Subscription Order is created- any Discount Code already applied will be redeemed.
{% endhint %}

At this point it's not possible to apply or change the Discount Code, only display details of the Order that's active. The purpose of the Form at this point is actually to allow Users to edit their payment details only.

```liquid
{% raw %}
{% if subscription_discount_already_redeemed == true %}

<!-- Insert code here - the Discount has already been redeemed against the Subscription Order-->
{% endif %}
{% endraw %}




```

You could add this logic around the whole Layout (as in the default Layout), or just around individual components. For the sake of clarity, in the "subscription/default" Layout, we've opted to wrap the logic around the whole Layout, creating two distinctly separate blocks of Liquid for before and after redemption.

You can also add the statement to check if the Discount will apply to the next invoice or if the Discounted period of months is over.

```liquid
{% raw %}
{% if rate_still_discounted == true %}
{% endif %}
{% endraw %}
```

