Customise the Email and Landing Page used to take updated payment methods and authorisation from Subscription customers.

# Introduction

When a Stripe subscription changes status, a customer may need to update their payment details or carry out 3D Secure authorisation.&#x20;

The email and landing page used in this flow can be customised and branded.&#x20;

# The Email

You can find the System Email under Site Manager > System Emails with the name `Subscription User Action Required`.&#x20;

The purpose of this Email is to inform the User that the Subscription Order needs action from them before it can continue to be processed.&#x20;

## Adding a Link to the Landing Page

You must add a link to the Landing Page where your customer can take action. You can use the Liquid below:

```liquid
{% raw %}
{% include 'ecommerce/subscriptions/subscription_system_page_link'
   button_text: "Authorise payment details"
   button_id: "authorisePayment" %}
{% endraw %}
```

Parameters:

*   `button_text` -  sets the text displayed on the button

*   `button_id` - optional - allows you to set the ID of the button

*   `button_class` - optional - allows you to set the class of the button

## Available Fields

*Subscription Order Fields*

*   `{{data.subscription_order}}` - Output all available fields as JSON (except the new\_subscription\_status - see below).

*   `{{data.subscription_order['User ID']}}` - The ID of the customer in Siteglide.

*   `{{data.subscription_order['Subscription ID']}}` - The ID of the Subscription Order in Siteglide.

*   `{{data.subscription_order['Status']}}` - The previous status of the Subscription Order before the update that triggered this Email

*   `{{data.new_subscription_status}}` - the new status of the Subscription Order. This is the Event which will have triggered the Email.

*   `{{data.subscription_order['Stripe Subscription ID']}}` - The ID of the Subscription in the Stripe Dashboard.

*   `{{data.subscription_order['Cancel At Period End']}}` - "true" or "false"- if true, this Subscription has been set by the User to be automatically Cancelled at the end of the current billing period. The User has a chance to change their minds until this date.

*   `{{data.subscription_order['Stripe Plan ID']}}` - The Stripe ID for the Plan this Subscription Order is using. This may be an older plan than the current plan used by the Subscription product.

*   `{{data.subscription_order['Plan Chargeable Price']}}` - A snapshot of the Price of this Subscription Order's plan. This may be an older plan than the current plan used by the Subscription product.

*   `{{data.subscription_order['Plan Display Only Price']}}` - A snapshot of the Display Only Price of this Subscription Order's plan. This may be an older plan than the current plan used by the Subscription product.

*   `{{data.subscription_order['Plan Chargeable Price Formatted']}}` - A snapshot of the Price of this Subscription Order's plan. This may be an older plan than the current plan used by the Subscription product. Formatted as a decimal (e.g. 1.00).

*   `{{data.subscription_order['Plan Display Only Price Formatted']}}` - A snapshot of the Display Only Price of this Subscription Order's plan. This may be an older plan than the current plan used by the Subscription product. Formatted as a decimal. (e.g. 1.00

*   `{{data.subscription_order['Plan Interval']}}` - A snapshot of the Interval of this Subscription Order's plan. This may be an older plan than the current plan used by the Subscription product.

*   `{{data.subscription_order['Plan Interval Count']}}` - A snapshot of the Interval Count of this Subscription Order's plan. This may be an older plan than the current plan used by the Subscription product.

*Subscription Fields*

*   `{{data.subscription_order.subscription}}` - Output all available fields as JSON

*   `{{data.subscription_order.subscription.name}}` - The name of the Subscription Product

*   `{{data.subscription_order.subscription['Description']}}`

*   `{{data.subscription_order.subscription['Image']}}`

*   `{{data.subscription_order.subscription['Interval Count']}}`

*   `{{data.subscription_order.subscription['Stripe Product ID (Live)']}}` - The ID of the product in Stripe Live Mode

*   `{{data.subscription_order.subscription['Stripe Product ID (Test)']}}`- The ID of the product in Stripe Test Mode

*Customer Fields*

*   `{{data.subscription_order.related_user}}` - Output all available fields as JSON

*   `{{data.subscription_order.related_user.id}}` - The ID of the User in Siteglide

*   `{{data.subscription_order.related_user.name}}`&#x20;

*   `{{data.subscription_order.related_user.first_name}}`

*   `{{data.subscription_order.related_user.last_name}}`

*   `{{data.subscription_order.related_user.email}}`

*Tip: Changes in the Pricing Plan
*It's possible to change the price and billing interval of a Subscription. This change will only affect new subscribers and existing customers will continue on the plan they signed up for originally. You can read more about this here: [eCommerce Subscriptions - Changing the Price and Billing Interval](/eCommerce/get-started-ecommerce/subscriptions/managing-subscriptions/changing-price-and-billing-interval.md)

When outputting fields in the email, Subscription Order fields beginning with the word "Plan" will normally be the appropriate choice. These will show the price that these Users will be paying- the original plan when they signed up.

The other Price and Interval fields stored against the Subscription, could be used to show how much the User is saving on their current plan compared to the current price. In the different context of the [Subscription Detail Page](/eCommerce/get-started-ecommerce/subscriptions/subscriptions-detail.md)- we give a different recommendation as here it may not always be possible to identify immediately if the User is subscribed to a different plan.

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

Check out all the available Liquid filters over on the [platformOS Liquid docs](https://documentation.platformos.com/api-reference/liquid/introduction).

# The Landing Page

You can find the System Page under `Site Manager > System Emails` with the name `Subscription User Action Required`.&#x20;

The purpose of this Page is to provide a reliable URL where the above email can send Users to update their Payment Method. We'll provide the URL parameters to let the Page know which Subscription and Subscription Order to load. We'll also provide security to check that the User owns that Subscription Order before continuing.&#x20;

This page may function very similarly to the standard Subscription Detail Page, however, you do have the option to use a different Layout or logic if you prefer.&#x20;

## Including the Subscription Detail Layout

The following Liquid will include a Subscription Detail Layout for the Subscription referenced in the link from the above Email. Note, this is different from the usual Liquid for including a Layout, because Siteglide will in this case be setting some of the parameters for you automatically.&#x20;

```liquid
{% raw %}
{% include "modules/siteglide_ecommerce/ecommerce/subscription_update_payment"
   subscription_detail_page_layout: 'default' 
%}
{% endraw %}
```

Parameters:

*   `subscription_detail_page_layout` - This allows you to choose which Detail Layout will be used for the Subscription Detail View. You can choose a different Layout than you use on your Subscription Detail Page.

If that Detail Layout contains a Form, we'll use the URL parameters to set the Form to edit the payment details for the correct Subscription Order referenced in the link from the Email.&#x20;

You can add any other static content you like to this Page, but we recommend you use the Subscription Detail Layout itself to add any dynamic content and you can see available fields there.
