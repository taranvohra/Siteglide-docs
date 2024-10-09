# 🛳️ Module - Secure Zones - Changelog

### 1.3.2 - 25th June 2024

* Updated security as outlined in [System Files update v2.8.2.4](https://help.siteglide.com/en/article/245-module-system-files-changelog)

***

### 1.3.1 - 23rd January 2024

* Added Form ID to password reset Form to better handle error messages

***

### 1.3.0 - 3rd October 2022

* Support for Automations structure

***

### 1.2.11 - 11th March 2022

* Patch for slug on User Orders output

***

### 1.2.10 - 7th December 2021

* Add support for new eCommerce Order structure on User Orders output via `order_products_flat` - [Docs](https://developers.siteglide.com/how-to-sell-digital-products#pi-output-the-media-download-link-within-your-user-orders-layout)

***

### 1.2.9 - 13th July 2021

* Fix for Password Reset on previously deleted users

***

### 1.2.8 - 2nd June 2021

* Access to CRM Company data on User Details output

***

### 1.2.7 - 17th May 2021

* Wording update on 'Add to Favourites' alert boxes
* Access to CRM User Address data on User Details output

***

### 1.2.6 - 14th April 2021

* Add support to `user_orders` for sorting and pagination

***

### 1.2.5 - 11th February 2021

* Updated default layouts to use [Siteglide Studio](https://help.siteglide.com/article/135-studio-by-siteglide-introduction) (this won't overwrite existing installed layouts)

***

### 1.2.4 - 7th January 2021

* Updates to User Orders query to fetch Ordered Products

***

### 1.2.3 - 10th December 2020

* Made CRM Custom Field output easier by giving you access to field names (e.g. `this['User Field XYZ']`)

***

### 1.2.2 - 5th November 2020

* Minor field changes ready for upcoming Module Custom Field updates

***

### 1.2.1 - 30th October 2020

_Important: Security update for Secure Zones_

Our latest Secure Zone Module update fixes a security vulnerability in Sign Up Forms and is a recommended update for all Sites.

**For most of our partners, no change in your code will be needed. Simply install the updated Module version 1.2.1.** However, if your Site uses custom code to add Secure Zones not currently attached to the Form, you will now need to attach them to the Form.

_Further Details:_

It has been possible to use Front End code to change which Secure Zone a Sign Up Form will give Users access to. There were legitimate uses for this, however, if a malicious User with knowledge of JavaScript was able to guess a Secure Zones ID, they would have been able to sign themselves up to that Secure Zone.

After this update, only Secure Zones attached to a specific Form in Admin will be allowed when Front End code changes the active Secure Zone of a Form. Any other Secure Zones will be rejected by the server.

We have worked quickly to close this vulnerability after discovering it internally and thank you for your understanding.

This documentation sets out clearly the new safer procedure for changing the Secure Zone using front-end code: - [docs](https://developers.siteglide.com/in-a-form-layout-dynamically-select-a-secure-zone-from-an-approved-list-in-admin)

_Further Documentation Updates:_

We've also updated our Secure Zones documentation with new content, see especially:

* [Secure Zones Introduction](https://help.siteglide.com/article/139-secure-zones-getting-started)

***

### 1.2.1 - 28th October 2020

* _Favourites_ - You can now add a button to WebApp/ Module layouts to allow logged in users to store items as 'favourite' - [Docs](https://developers.siteglide.com/storing-users-favourite-webapp-module-items)
* _Email/Password edit_ - Users can now edit their Email Address and Password - [Docs](https://developers.siteglide.com/how-users-edit-their-email-and-password-front-end)
* _User Secure Zones_ - This data array can now be accessed in Templates as well as Pages

***

### 1.1.0 - 4th September 2020

* Structural changes to improve performance and usage costs.

CRM Secure Zone data is now stored as User Properties rather than as User Profiles. Any custom extensions of this database will require you to change to the new field before updating your Module. All data is migrated to the new field on update.

Accessing data before: `session.current_user._user_.properties.secure_zones`\
Now: `session.current_user.properties.secure_zones`

If you apply this update, then your eCommerce Module should be updated to at least v1.0.4 in order to fully support this change.

***

### 1.0.0 - 14th August 2020

* Support for Secure WebApp items - [Docs](https://help.siteglide.com/article/139-secure-zones-getting-started)

***

### 0.10.0 - 29th July 2020

* User Subscriptions View updated to include new Subscriptions functionality: [User Subscriptions](https://developers.siteglide.com/user-subscriptions-list-the-logged-in-users-subscription-orders)

***

### 0.9.6 - 7th July 2020

* CRM - You can output Custom Field Set data with the rest of User Details
* Forms - Slight improvement to performance on Secure Zone signup forms, by combining 2 system level calls into 1

***

### 0.9.4 - 25th March 2020

* Fix for missing name in Password Reset emails
* Fix for Password Reset emails not sending if user was previously deleted

***

### 0.9.3 - 14th February 2020

* [Browser Support updates](https://help.siteglide.com/article/254-browser-support-updates-release-notes)
* Bug fix - Secure Zones blocked signup -

Initial report here -> [https://roadmap.siteglide.com/bugs/p/secure-zones-second-signup-with-same-email](https://roadmap.siteglide.com/bugs/p/secure-zones-second-signup-with-same-email)

If someone submitted a basic contact form, and then a Secure Zone signup form with the same email address, they'd see a "Invalid email or password" error, even though they'd never set a password before.

***

### 0.9.2 - 19th November 2019

* Allow custom redirects after a Password Reset request has been submitted

***

### 0.9.1 - 4th September 2019

* Added support for older browsers
