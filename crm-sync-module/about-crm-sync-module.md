# 💡 About CRM Sync Module

The Sendgrid CRM Sync Module aims to integrate the Siteglide CRM with an Email Marketing Platform, starting with Sendgrid.

The module can carry out the following actions taking the data _from_ the Siteglide Admin and using it _to_ update the e-marketing platform's data:

* Creating custom fields automatically
* Renaming custom fields if the name has been changed in Siteglide
* Creating a Contact with CRM data
* Updating a Contact
* Adding a Contact to Lists
* Removing a Contact from Lists
* Deleting a Contact

It's also possible to use Liquid logic and parameters to modify which of these actions is taken at any one time.

At the present time, the module does not make use of webhooks to update Siteglide when something changes on the e-marketing provider. Any checks on the current state of data on the e-marketing provider are done when the module code is run by Siteglide.

The module is not intended at the current time to allow design and triggering of bulk emails from the Siteglide Admin itself. Instead, by syncing data to an e-marketing platform, it allows you to make the most of the no-code and low-code tools on that platform, powered by automated, up-to-date, data. Sendgrid for example allows automations to be triggered a certain amount of time after a contact is added to a specific list. The module's job is to add that contact to the list, Sendgrid then has everything it needs to run a wide range of automations.
