# 🔹 A Transactional Email Example

{% hint style="info" %}
We strongly recommend that you [authorize Sendgrid](../automations-and-emails/about-automations/guides-automations/steps-to-authenticating-sendgrid-emails-on-live-sites.md) to send emails from your domain to avoid them going to spam filters, or being rejected from sending by your DMARC policy.&#x20;
{% endhint %}

Once you've read how our [introduction to Automations](about-automations.md), you're ready to start creating your own.  Siteglide Automations can send transactional Emails powered by Sendgrid. By transactional emails, we mean an email sent to, or c.c.ed to one or a few relevant people when a trigger occurs. Below is an example of an email in Automations.

This example will send an email to 'site-admin@siteglide.com' with a link to the newly created item.

{% hint style="info" %}
Note, for forms, use the form variable for submitted data, for webapps and modules, use the data.data variable. See [dynamic-content-in-workflow-and-autoresponder-emails.md](../automations-and-emails/reference-automations/dynamic-content-in-workflow-and-autoresponder-emails.md "mention")
{% endhint %}

<figure><img src="https://d258lu9myqkejp.cloudfront.net/attachment_images/f0f073c5beb44a6a98d214a515f6fe53bcc369019c684cac689acb65ef91f41a1679653640212.png" alt=""><figcaption></figcaption></figure>
