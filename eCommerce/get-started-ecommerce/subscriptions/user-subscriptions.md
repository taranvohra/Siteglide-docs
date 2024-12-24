This Article shows you how to use the Secure Zones Layout user\_subscriptions to List Subscription Orders belonging to a User.

# Introduction

This article shows you how to use the Secure Zones Layout user\_subscriptions to List Subscription Orders belonging to a User. As this is a Secure user-specific List, the Layout is found in the Secure Zones Module.

This is slightly different from a Subscriptions List view, as this lists all available Subscription products- you can [learn more here](/ecommerce/get-started-ecommerce/subscriptions/subscriptions-list.md).

# Outputting the user\_subscriptions List

The following Liquid can be outputted on any Page protected by a Secure Zone:

```liquid
{% raw %}
{%- include 'user_subscriptions', layout: 'default' -%}
{% endraw %}
```

Parameters:

- `layout` - Select a Layout for this view.&#x20;

# The user\_subscriptions Layout

## File Structure

You can find these Layouts at the path: `layouts/modules/module_5/user_subscriptions/`

## Development

### Looping over Subscription Orders

To loop over available Subscription Orders, you can use the following Liquid:

```liquid
{% raw %}
{% for this in subscription_orders %}

{% endfor %} 
{% endraw %}
```

Inside the loop, you can use the available fields shown below under the `this` namespace. Outside of the loop Liquid, you can build the HTML structure which will wrap your Layout.

### Setting a Subscription to Cancel at the end of the Billing Period

You can use the following Liquid to include a button to either cancel a Subscription or stop a pending cancellation. Read more here.

```liquid
{% raw %}
{%- if and this.cancel_at_period_end != 'true' -%}         
  {%- include 'ecommerce/subscription_cancel', orderID: this.id -%}
{% elsif this.cancel_at_period_end == 'true' %}
  {%- include 'ecommerce/subscription_reactivate_cancelled', orderID: this.id -%}
{%- endif -%}
{% endraw %}
```

## Available Fields

*Subscription Order*

- `{{this}}` - Output all available fields as JSON
- `{{this.created_at}}` - Outputs the time when this Subscription Order was originally created. Use the date filter with Ruby date format to format.
- `{{this.last_edit_date}}` - outputs the last time this Subscription Order was updated either via the Admin, user-action, or via Stripe Webhook. Use the date filter with Ruby date format to format.&#x20;
- `{{this.user_id}}` - The ID of the customer in Siteglide.
- `{{this.id}}` - The ID of the Subscription Order in Siteglide.
- `{{this.status}}` - The previous status of the Subscription Order before the update that triggered this Email.
- `{{this.cancel_at_period_end}}` - Either 'true', false, or empty. If set to 'true' the Subscription will be cancelled at the end of the current billing period.&#x20;
- `{{this.stripe_subscription_id}}` - The ID of the Subscription in the Stripe Dashboard.
- `{{this.stripe_plan_id}}` - The Stripe ID for the Plan this Subscription Order is using. This may be an older plan than the current plan used by the Subscription product.
- `{{this.plan_chargeable_price}}` - A snapshot of the Price of this Subscription Order's plan. This may be an older plan than the current plan used by the Subscription product
- `{{this.plan_display_only_price}}` - A snapshot of the Display Only Price of this Subscription Order's plan. This may be an older plan than the current plan used by the Subscription product.
- `{{this.plan_chargeable_price_formatted}}` - A snapshot of the Price of this Subscription Order's plan. This may be an older plan than the current plan used by the Subscription product. Formatted as a decimal (e.g. 1.00).
- `{{this.plan_display_only_price_formatted}}` - A snapshot of the Display Only Price of this Subscription Order's plan. This may be an older plan than the current plan used by the Subscription product. Formatted as a decimal. (e.g. 1.00)
- `{{this.plan_interval}}` -  A snapshot of the Interval of this Subscription Order's plan. This may be an older plan than the current plan used by the Subscription product.
- `{{this.plan_interval_count}}` -  A snapshot of the Interval Count of this Subscription Order's plan. This may be an older plan than the current plan used by the Subscription product.

*Subscription*

- `{{this.subscription}}` - Output all available fields as JSON
- `{{this.subscription.name}}` - The name of the Subscription Product
- `{{this.subscription['Description']}}`
- `{{this.subscription['Image']}}`
- `{{this.subscription['Interval']}}`
- `{{this.subscription['Interval Count']}}`
- `{{this.subscription['Product Code (SKU)']}}`
- `{{this.subscription['Stripe Product ID (Live)']}}` - The ID of the product in Stripe Live Mode
- `{{this.subscription['Stripe Product ID (Test)']}}`- The ID of the product in Stripe Test Mode

- The price of the Subscription Product per billing period:

```liquid
{% raw %}
{{context.exports.currency_map.data[this.subscription.price.properties
['module_field_14/price_2']]}}
{% include 'modules/siteglide_ecommerce/ecommerce/price_formatter' price_data: this.subscription.price.properties['module_field_14/price_3'] %}
{% endraw %}
```

*Price*

- `{{this.subscription.price.currency}}` - the currency
- `{{this.subscription.price.currency_symbol}}` - the currency symbol
- `{{this.subscription.price.price_charge}}` - the price charged per Interval as an integer.&#x20;
- `{{this.subscription.price.price_charge_formatted}}` - the price charged per Interval as a decimal currency format.
- `{{this.subscription.price.price_display}}` - a display-only price per interval as an integer e.g. recommended retail price
- `{{this.subscription.price.price_display_formatted}}` - a display-only price per interval as a decimal currency format e.g. recommended retail price.&#x20;

*Tip: Changes in the Pricing Plan*
It's possible to change the price and billing interval of a Subscription. This change will only affect new subscribers and existing customers will continue on the plan they signed up for originally. You can read more about this here: <a href="https://help.siteglide.com/en/article/ecommerce-subscriptions-changing-the-price-and-billing-interval-egzyvo/" target="_blank">eCommerce Subscriptions - Changing the Price and Billing Interval</a>

When outputting fields in the `user_subscriptions` view, Subscription Order fields beginning with the word "Plan" will normally be the appropriate choice. These will show the price that these Users will be paying- the original plan when they signed up.&#x20;

The other Price and Interval fields stored against the Subscription, could be used to show how much the User is saving on their current plan compared to the current price. In the different context of the [Subscription Detail Page](/ecommerce/get-started-ecommerce/subscriptions/subscriptions-detail.md)- we give a different recommendation as here it may not always be possible to identify immediately if the User is subscribed to a different plan.&#x20;

*Tip: Working with the Interval Fields*
As you can see below, there are multiple fields involved in storing the Interval of charges, which you can use to display the Interval in a user-friendly way. Here's one example of using Liquid to programmatically decide the format to display the Interval:

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

If the Interval Count is greater than 1, it will use formatting like "every 2 days".&#x20;

Check out all the available Liquid filters over on the <a href="https://documentation.platformos.com/api-reference/liquid/introduction" target="_blank">platformOS Liquid docs</a>.