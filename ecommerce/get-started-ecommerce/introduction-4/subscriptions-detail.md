---
title: Detail Layout
slug: 1fIp-
createdAt: 2021-02-19T13:41:30.000Z
updatedAt: 2023-03-03T08:09:58.000Z
---

# Subscriptions Detail Layout

The Detail Layout for Subscriptions displays details of the Subscription Product and also a Form for creating/editing Subscription Orders

## Introduction

A Subscription Detail Layout allows you to display detailed content about an individual Subscription product to a customer. It also is an important part of outputting a Subscription Sign Up Form, as these must be outputted within the Layout of the Subscription they will subscribe Users to.

## Outputting the Detail View

The most common place where Detail Views are displayed is on the automatically generated Detail Page, if you have enabled these. However, they can also be outputted within most Liquid files, including ordinary Pages.

### Setting up Detail Pages

Heading to ECOMMERCE > Settings will allow you to select the Subscriptions tab.

![](https://downloads.intercomcdn.com/i/o/223781939/f343dc96b5b8ec49d55ea67c/image.png)

Here you can set up Detail Pages by:

* Choosing the slug which will begin the URL to Subscription Detail Pages
* Choose a Page Template to use on Subscription Detail Pages
* Choose a Detail Layout to use on Subscription Detail Pages

### Outputting on a Standard Page (or in most Liquid files, including Emails)

You can use the `type` parameter to output a Detail Layout in most Liquid files:

```liquid
{% raw %}
{% include "module", id: "14/subscription"
   item_ids: subscription_id
   type: "detail", layout: 'my_layout'
%}

{% endraw %}
```

Parameters:

* `type` - give the value
* `'detail'`.
* `layout` - give the name of a Detail Layout for Subscriptions
* `item_ids` - this parameter is usually optional, but it's essential when you are outputting a Detail View as only one Item ID must be displayed.

Bear in mind that Forms will not work properly inside Emails, so if displaying a Detail Page inside an Email, it is best to provide an alternative Detail Page without the Sign Up Form.

### Outputting on the Subscription Action Required System Page

To output the Layout here, you need to add a Detail Layout name to the Liquid as a parameter. Read more [here](https://developers.siteglide.com/editing-the-subscription-user-action-required-system-page-and-email).

## File Structure

Subscription Layouts can be found at the path: `layouts/modules/module_14/subscription` Within this folder, you can create a folder for each Layout. Each Layout folder can contain a further "detail" folder containing the `wrapper` and `item` files it needs.

![](https://downloads.intercomcdn.com/i/o/223783980/3767a4b64dc4f4a28e327a37/image.png)

## Developing the Detail Layout

#### Step 1 - Optional - Add logic to inform the User of what the status of their Subscription is currently.

We provide an example of some logic you can use to explain to logged in Users what the Form will do:

```liquid
{% raw %}
{% if context.params.slug == "subscription-action-required" %} 
    
    {% comment %} Content to display when customer is responding to an email notification which asked them to update or authorise payment details. {% endcomment %} 

{%- elsif active_subscriptions contains this.id and context.current_user.id -%} 

    {% comment %} Content to display when customer has already signed up to this subscription and its status is active. {% endcomment %} 

{% elsif subscription_order_id and context.current_user.id %} 

    {% comment %} Content to display when customer has already signed up to this subscription and its status is not active. {% endcomment %} 

{%- else -%} 

    {% comment %} Content to display when the User is not logged in or has not yet signed up to this subscription. {% endcomment %} 
				
{%- endif -%}
{% endraw %}




```

In the case where the User is not currently logged in and is not responding to an email, the logic won't be able to determine the exact status straight away.

Instead, if a non-logged in User tries to Sign up for a Subscription, Siteglide will first log them in and check if they have an active Subscription already. If they do, we'll throw an error, but allow the User to try again if they wish to update their payment details.

#### Step 2 - Create your Form

Adding a Form to the Detail Layout allows users to Sign Up to this Subscription product. You can read more about creating this Form [here](https://help.siteglide.com/en/article/forms-getting-started-4i929m/#2-creating-and-editing-forms).

If you've already created your Form, you can skip this step.

#### Step 3 - Include the Form inside the Detail Layout

Once you've created a Form and made a note of its ID, you'll be able to add it to your Detail Layout.

As a guide, we've added a Liquid comment to remind you to add your Subscription Sign Up Form to this Layout: \`

\`

This is just a suggestion, you can actually include your Form anywhere you like in the Layout. Use the following Liquid: `<div data-gb-custom-block data-tag="include" data-0='form' data-1='1' data-2='1' data-3=', layout: '></div>`

Parameters:

* `id` - the ID of your Subscription Sign Up Form, you can check this in CMS > Forms. Remember you can use the same Form Layout for all Subscriptions. The this.id field controls which Subscription product is associated with the Form.
* `layout` - Choose a Form Layout

#### Step 4 - The Wrapper

The `wrapper.liquid` file could be used to add any HTML structure you may require around your layout.

You must include the following Liquid, which will output the `item.liquid` file for the Subscription Item. Most fields are specific to the Item and will only be available inside the `item.liquid` file.

```liquid
{% raw %}
{%- include 'modules/siteglide_ecommerce/ecommerce/get/get_subscriptions'
    item_layout: 'item' 
-%}

{% endraw %}
```

#### Step 5 - Available Fields

On the Subscription Detail View, we provide you with fields relating to the Subscription and also the Subscription Order for a logged in User.

_Subscription Fields_

* `{{this}}` - Output all fields as JSON
* `{{this.id}}`
* `{{this.weighting}}`
* `{{this.release_date}}`
* `{{this.expiry_date}}`
* `{{this['Description']}}`
* `{{this['Interval']}}`
* `{{this['Interval Count']}}`
* `{{this.full_slug}}` - URL for the Product Detail Page
* `{{this['Secure Zones']}}` - Array containing the IDs of Secure Zones associated with this Subscription.
* `{{this.price.id}}`
* `{{this.price.currency}}`
* `{{this.price.price_charge}}` - The chargeable price of this Subscription each Interval. Integer format.
* `{{this.price.price_display}}` - A field for displaying a secondary price of your choice, e.g. recommended retail price. This is not used by the integration. Integer format
* `{{this.price.currency_symbol}}`
* `{{this.price.price_charge_formatted}}` - The chargeable price of this Subscription each Interval. Currency format
* `{{this.price.price_display_formatted}}` - A field for displaying a secondary price of your choice, e.g. recommended retail price. This is not used by the integration. Currency format.

\*Subscription Order Fields \*If a User is logged in, Siteglide will establish if they have an existing Subscription Order for this Product. Using any of these fields should be done cautiously, as they will not be available if the User is logged out, or if they don't have an existing Subscription.

To determine this, you can use Liquid Logic to hide an entire block of code in which you use these fields:

```liquid
{% raw %}
{% if subscription_order != blank %}
  {% comment %}Content here can safely include subscription_order fields- 
  or will be hidden if none is available.{% endcomment %}
{% endif %}
{% endraw %}



```

Fields:

* `{{subscription_order}}`- Output all Subscription Order fields as JSON
* `{{active_subscriptions}}`- Array containing all Subscription IDs connected with one of the current User's Subscription Orders, where those orders have status Active
* `{{subscription_order['Status']}}` - These relate to the Subscription Status in Stripe and are the best way to understand the status of the Subscription Order at a glance. More information available below.
* `{{subscription_order['Stripe Subscription ID']}}` - This refers to a Subscription on Stripe and can be searched by the Client on the Stripe Dashboard to find out detailed information about this Subscription Order and the associated customer, invoices, payment\_intents and charges.
* `{{subscription_order['Cancel At Period End']}}` - "true" or "false"- if true, this Subscription has been set by the User to be automatically Cancelled at the end of the current billing period. The User has a chance to change their minds until this date.
* `{{subscription_order['Stripe Plan ID']}}` - The Stripe ID for the Plan this Subscription Order is using. This may be an older plan than the current plan used by the Subscription product.
* `{{subscription_order['Plan Chargeable Price']}}` - A snapshot of the Price of this Subscription Order's plan. This may be an older plan than the current plan used by the Subscription product.
* `{{subscription_order['Plan Display Only Price']}}`- A snapshot of the Display Only Price of this Subscription Order's plan. This may be an older plan than the current plan used by the Subscription product.
* `{{subscription_order['Plan Chargeable Price Formatted']}}` - A snapshot of the Price of this Subscription Order's plan. This may be an older plan than the current plan used by the Subscription product. Formatted as a decimal (e.g. 1.00).
* `{{subscription_order['Plan Display Only Price Formatted']}}` - A snapshot of the Display Only Price of this Subscription Order's plan. This may be an older plan than the current plan used by the Subscription product. Formatted as a decimal. (e.g. 1.00)
* `{{subscription_order['Plan Interval']}}` - A snapshot of the Interval of this Subscription Order's plan. This may be an older plan than the current plan used by the Subscription product.
* `{{subscription_order['Plan Interval Count']}}` - A snapshot of the Interval Count of this Subscription Order's plan. This may be an older plan than the current plan used by the Subscription product.

\*Tip: Changes in the Pricing Plan \*It's possible to change the price and billing interval of a Subscription. This change will only affect new subscribers and existing customers will continue on the plan they signed up for originally. You can read more about this here: [eCommerce Subscriptions - Changing the Price and Billing Interval](https://help.siteglide.com/en/article/ecommerce-subscriptions-changing-the-price-and-billing-interval-egzyvo/)

When outputting fields, be aware that the Price might have changed globally for a Subscription, while a User may already have an existing Subscription with a different price. When changing their payment Details on the Subscription Detail View, these Users may be reassured to see the price displayed they are paying currently.

For these Users (if they are logged in) there will be two sets of fields available. For example:

* `{{this.price.price_charge}}` - Shows the current price of the Subscription if a new User were to sign up now.
* `{{subscription_order['Plan Chargeable Price']}}` - This field, if it is available, shows the price of the older plan that this customer is currently paying. See Subscription Orders in the next section for more of these fields.

You can use logic to display a different price to Users in this situation.

```liquid
{% raw %}
{% if subscription_order['Plan Chargeable Price'] != blank %}
  <p>{{subscription_order['Plan Chargeable Price']}}</p>
{% else %}
  <p>{{this.price.price_charge}}</p>
{% endif %}
{% endraw %}



```

Or alternatively, you can use the default filter:

```liquid
{% raw %}
<p>{{subscription_order['Plan Chargeable Price'] | default: this.price.price_charge}}</p>

{% endraw %}
```

_Tip: Working with the interval_ As you can see above, there are multiple fields involved in storing the interval of charges, which you can use to display the interval in a user-friendly way. Here's one example of using Liquid to programmatically decide the format to display the Interval:

```liquid
{% raw %}
{% if this['Interval Count'] == "1" %}
  per {{this['Interval'] | pluralize: 1}}
{% else %}
  (every {{this['Interval Count']}} {{this['Interval']}})
{% endif %}
{% endraw %}
```

If the Interval Count is 1, it will use formatting like "per day".

If the Interval Count is greater than 1, it will use formatting like "every 2 days".

Check out all the available Liquid filters over on the [platformOS Liquid docs](https://documentation.platformos.com/api-reference/liquid/introduction).
