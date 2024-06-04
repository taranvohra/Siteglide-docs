# 🔹 Siteglide's Module Update Policy

## How to Update a Module

When an update is available for a module that you have installed on one of your sites, you will see a notification icon along the top bar of the sites' Admin.

To install an update, head on over to the Site Settings page, and click the Update button for the relevant modules. **Note: Updating a module may affect the live site, please follow the below guidance and check the module release notes to determine if and when to update each module.**

{% hint style="info" %}
For sensitive sites, where extra caution is expected from your clients, you can create a Site Copy of your Site to a staging environment, install the update to the copied Site and test for any issues in the affected Module's implementation. This allows you to develop a fix in advance if needed, giving you time to ask for advice, and deploy that fix at the same time as you update the module.
{% endhint %}

### How does this affect your layouts?

Layouts provided in Modules are ignored on update. This is done so we don't overwrite your changes every time we release a new version of a Module. The same applies to some other file types such as Email Notifications (Password Reset in Secure Zones) and System Pages (401 in Secure Zones)

***

## Deprecation notices

Sometimes we will release updates to existing features that mean the old method is now unsupported and deprecated. The old method will continue to be usable for a time period specified in the changelog - typically 1 year.

### How do you switch to the new method?

Unless you're writing custom code, in most cases the feature will be seamlessly switched to using the new method where input and output remain the same. However, if you have custom code that is extending the old method, then this will remain. We will release notes on what has changed, and you will then see what you need to change in your custom code.

### What if you don't want to update your custom code, and want to continue with the deprecated version?

Module updates are optional, so simply don't update the Module. Obviously you would then miss out on any future features and upgrades for that specific Module. Currently there is no way to downgrade a Module, so please check the release notes before upgrading.
