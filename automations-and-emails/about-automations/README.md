# 💡 About Automations

#### What are Automations?

Automations are a set of Triggers and Actions, which can be applied to Forms, Modules, and WebApps.

For example:

* **Trigger** - When a WebApp item is edited in Admin
* **Action** - Send an email to the content approval team

#### What Triggers and Actions are available?

**Triggers**

* Admin item create - Modules (excluding eCommerce Orders), WebApps
* Admin item update - Modules, WebApps
* Admin item delete - Forms, Modules, WebApps
* Front-end item create - Forms, WebApps
* Front-end item update - WebApps
* Front-end item delete - WebApps

**Actions**

* API Call (limited to 1 per trigger)
* Custom (limited to 1 per trigger)
* Email

#### How do I add an Automation?

In the Table Builder view click the 'Automations' tab.From here you select the Trigger and Action to use, and then enter the relevant details for that Action.

In all Automations, you can access the data of an item using both `{{data}}` or `{{form}}` in your code editor.

Once you save your changes, the Automation will then be in place. For example, next time someone creates a WebApp item, your selected Action will be performed.

Note: From this view you can also edit or delete any existing Automations.

![Select a Trigger](https://d258lu9myqkejp.cloudfront.net/attachment\_images/9b9f0b6af72e75c44739eeaf48710178716f911a065df65d8930613d16a39ba6screenshot-2022-10-07-124810\_1rpm0c5.png)

![Select an Action](https://d258lu9myqkejp.cloudfront.net/attachment\_images/244a348b10909709dc374a1657d247850092b0b51bab5b69677106cb1ece721ascreenshot-2022-10-07-124814\_yw31s5.png)

&#x20;
