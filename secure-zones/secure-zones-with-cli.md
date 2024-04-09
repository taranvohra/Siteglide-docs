---
title: Secure Zones with CLI
slug: NnRm-
createdAt: 2021-02-18T11:04:18.000Z
updatedAt: 2023-03-03T08:09:58.000Z
---

How to create a Secure Zone using GraphQL via the CLI

Secure Zones are simply a Model object within Siteglide, with this in mind, we can very easily create Secure Zones via the CLI using GraphQL.

## Prerequisites

*   You have installed the Secure Zone module on the instance

*   You have [setup CLI and connected to your Site](https://developers.siteglide.com/introducing-siteglide-cli)

*   You know how to use the GraphiQL editor

## Example

Below is the GraphQL mutation that is used to create a Secure Zone from Siteglide Admin.&#x20;

We simply pass it the name for the Secure Zone within the query variables.&#x20;

```graphql
mutation(
	$name: String #The name of your Secure Zone
	){
  result: customization_create(
    customization: {
      custom_model_type_name:"modules/siteglide_secure_zones/secure_zones"
      properties: [
        {name: "name", value: $name}
      ]
    }
    form_configuration_name:"modules/siteglide_secure_zones/secure_zones"
  ){
    id
  }
}
```

After running the mutation, you will see an ID returned in the output window of the GraphiQL editor.  The ID returning means that the mutation was successful and your new Secure Zone can now be used.

![](https://downloads.intercomcdn.com/i/o/253866153/ddefa467bdf9f6fd434eba6e/Screen+Shot+2020-10-08+at+16.12.25.png)

{% hint style="warning" %}
## Note

If you already have Admin open you will need to refresh it to see the new Secure Zone.
{% endhint %}




