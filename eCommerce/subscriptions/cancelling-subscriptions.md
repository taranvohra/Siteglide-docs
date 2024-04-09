---
title: Cancelling Subscriptions
slug: jkQN-
createdAt: 2021-02-19T12:03:28.000Z
updatedAt: 2023-03-03T08:09:58.000Z
---

The customer can schedule their Subscription to end, while continuing to use services until the end date.

# Introduction

Ending a Subscription is not as simple as deleting most database objects. The customer may wish to arrange for their Subscription to end, but they may wish to continue using the services they've paid for until the end of the billing period!&#x20;

# Front-end cancellation

When a User "cancels" a Subscription front-end, we send an API call to Stripe, instructing them to mark the Subscription to be cancelled at the end of the current billing period.&#x20;

Subscription Orders marked for cancellation will have the field "cancel\_at\_period\_end" ("module\_field\_14/subscription\_order\_9") marked as "true". This corresponds to the equivalent property on Stripe.

The following Liquid can be added within a `user_subscriptions` List Layout:`{%- include 'ecommerce/subscription_cancel', orderID: this.id -%}
`
You may wish to use logic to only show the button when it can be used.

```liquid
{% raw %}
{%- if this.cancel_at_period_end != 'true' -%}
  {%- include 'ecommerce/subscription_cancel', orderID: this.id -%}
{%- endif -%}
{% endraw %}
```

# Un-scheduling the Cancellation before it happens

Until that time, we'll allow Users to change their mind and choose not to cancel the Subscription after all. This removes the property from the Stripe subscription `cancel_at_period_end` and the Subscription will remain in its current state: `{%- include 'ecommerce/subscription_reactivate_cancelled', orderID: this.id -%}`

You may wish to use logic to only show the button when it can be used.

```liquid
{% raw %}
{% if this.cancel_at_period_end == 'true' %}
  {%- include 'ecommerce/subscription_reactivate_cancelled', orderID: this.id -%}
{%- endif -%}
{% endraw %}
```

Both buttons could be combined in the logic as follows:

```liquid
{% raw %}
{%- if this.cancel_at_period_end != 'true' -%}
  {%- include 'ecommerce/subscription_cancel', orderID: this.id -%}
{% elsif this.cancel_at_period_end == 'true' %}
  {%- include 'ecommerce/subscription_reactivate_cancelled', orderID: this.id -%}
{%- endif -%}
{% endraw %}
```

# Cancelling Immediately

The option to cancel a Subscription item immediately is available on the Stripe Dashboard.&#x20;

# Stripe's Webhook

When the actual change of status to `canceled` takes place on Stripe, either because of an action on the Dashboard, or because Siteglide queued it to happen at the end of the billing period, Stripe will send a `customer.subscription.deleted` event to Siteglide. We'll then also remove the database object from your Site, and stop provisioning the Secure Zone Access.&#x20;
