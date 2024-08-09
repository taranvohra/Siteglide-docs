# ℹ️ A Custom Liquid Action Example

Once you've read how our [introduction to Automations](../), you're ready to start creating your own. Below is an example of a custom action in Automations.\
\
A custom action is a great place to run a [GraphQL mutation](../../../developer-tools/graphql/tutorials/tutorial-9-using-mutations-to-create-new-records.md) if you want to modify something in the site's database.

This example will log data if the WebApp item's name contains 'Hello'.

<figure><img src="https://d258lu9myqkejp.cloudfront.net/attachment_images/7f83ddff3cc84c4114dba78b9b695501b322737f21768325913fbd5a9b0bf0a41679653557245.png" alt=""><figcaption></figcaption></figure>

Learn more about the Log liquid tag here: [https://documentation.platformos.com/api-reference/liquid/platformos-tags#log](https://documentation.platformos.com/api-reference/liquid/platformos-tags#log) - one caveat, to read logs you won't usually be able to use pos-cli with a Siteglide site, use siteglide-cli instead:

{% content-ref url="../../../developer-tools/cli/reference.md" %}
[reference.md](../../../developer-tools/cli/reference.md)
{% endcontent-ref %}
