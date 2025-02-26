# 🛳️ Module - System Files - Changelog

### 2.8.3.1 - 26th February 2025

* Patch to fix Front-End Rollout Automations

***

### 2.8.3.0 - 20th December 2024

* Added support for Rollout front-end Automations (Form submissions, and WebApp item create/update/delete)

***

### 2.8.2.6 - 11th December 2024

* Add more logging to Form Submissions to support debugging
* Add an alert box warning when a user tries to navigate off the page during a Form Submission

***

### 2.8.2.5 - 10th July 2024

* WebApps/Modules - Added a new sort type for list output - 'item\_ids'. This can be used to output items in order of IDs provided to the 'item\_ids' parameter. This is especially useful for outputting DataSource Multi fields in the same order the items were selected/ordered in Admin - [Docs](/webapps/layouts/webapp-list-layout.md) - [Roadmap](https://roadmap.siteglide.com/core-platform/p/webapps-multi-data-source-output-order)

***

### 2.8.2.4 - 25th June 2024

* Security - In order to improve security of the platform, we have removed some scripts that were in place to support Internet Explorer 11. As ever, we recommend using the latest version of your chosen web browser, as this will ensure you have up to date security features. We understand however that you cannot control what browser people use to navigate to your websites, but Internet Explorer accounts for only 0.5% of web traffic now so we have elected for security over support in this case. We have updated our 'Browser Support' document to reflect this change here - [Front-end Browser Support](../../get-started/support-and-faqs/front-end-browser-support.md)

***

### 2.8.2.3 - 19th June 2024

* Config - Added a default site config for new sites, to ensure the right platformOS features remain active
* Marketplace authorisation - Fixed an issue in the authorisation process used by Marketplace Modules
* Forms - Fixed an issue where the wrong field could be highlighted as an error
* Site Search - Fixed an issue where you couldn't have multiple different Site Search inputs on a page

***

### 2.8.2.2 - 5th March 2024

* Forms - Fixed an issue with malformed filenames on file upload fields when some special characters are used
* Forms - Fixed an issue where Billing and Shipping address weren't being handled correctly for eCommerce Orders

***

### 2.8.2.1 - 20th February 2024

* Forms - Fixed an issue when uploading multiple images

***

### 2.8.2.0 - 23rd January 2024

* Module Forms - Added support for Marketplace Modules
* Allow constants such as Company Information to be used in email notifications - [Docs on how to use this feature](../../site-manager/code-snippets-includes/constants\_json.md)
* Added support for custom success functions to be used with Forms. Default action will remain as a redirect to your chosen URL - [Docs](../../cms/forms/go-further-forms/forms-success-callback.md)
* Added consistency to error message format on Form submissions

***

### 2.8.1.19 - 1st November 2023

* WebApp/Module forms - secure\_zone\_array is now correctly set a 'empty' for filtering.

***

### 2.8.1.18 - 18th October 2023

* WebApp/Module forms - Before this change 'slug' value was always auto-generated when creating a WebApp/Module item using a front-end form. Now, if you set a value yourself, it won't be replaced by the auto-generated version by the system.

***

### 2.8.1.17 - 10th October 2023

* Patch to fix pagination on Category output - 'category\_items'

***

### 2.8.1.16 - 6th October 2023

* Patch to fix front-end Module edit forms when using the 'Anyone can edit' option

***

### 2.8.1.15 - 10th May 2023

* Swap the order of 404 response and include for WebApp/Module list views - [Roadmap](https://roadmap.siteglide.com/core-platform/p/change-order-of-liquid-logic-on-404-partial)

***

### 2.8.1.13 - 21st March 2023

* Fix an issue on forms with boolean fields that blocked them from submitting correctly

***

### 2.8.1.11 - 14th March 2023

* Fix an issue where you couldn't unset checkbox fields for front-end WebApp items on Forms
* Added 'use\_wrapper' param on WebApps to allow them to follow a similar output structure to Modules

***

### 2.8.1.10 - 19th January 2023

* Added 'module_is_in\_admin' authorisation check as an include, where it was previously only an Authorisation Policy. This allows for more control over what shows on a page in Custom UI for Modules.

***

### 2.8.1.8 - 30th December 2022

* Sitemap XML - Update lastmod to use same 'Last Edited' value as shown in Siteglide Admin. Before this change the value only changed on page content update, and not on change of metadata or page URL

***

### 2.8.1.7 - 21st December 2022

* WebApps/Modules - Better 404 responses for search engines

***

### 2.8.1.6 - 9th December 2022

* Forms - Add better error handling on hCaptcha validation. Automatically highlight the box in red, like other fields.

***

### 2.8.1.4 - 6th December 2022

* WebApp Forms - Support for "Anyone can edit" option

***

### 2.8.1.3 - 1st December 2022

* Forms - Fix to make custom JS form validation work seamlessly with hCaptcha spam protection

***

### 2.8.1.2 - 7th November 2022

* Automations - Support for 'enabled' option

***

### 2.8.1.1 - 28th October 2022

* Added hCaptcha as a Spam Protection option (default) on Forms

***

### 2.8.0.4 - 25th October 2022

* Added support for Google Auth in Integrations

***

### 2.8.0.2 - 10th October 2022

* Fix an issue with number fields in site search

***

### 2.8.0.0 - 3rd October 2022

* Support for Automations structure

***

### 2.7.2.6 - 7th September 2022

* Fix an issue with hyphens (-) in site search keyword

***

### 2.7.2.4 - 3rd August 2022

* Fix an issue where some WebApp/Module items would show in Sitemap even when they have the detail view turned off
* Fix an issue where you couldn't unset checkbox fields for CRM fields on Forms

***

### 2.7.2.3 - 23rd May 2022

Security patch for Form submissions

***

### 2.7.2.1 - 7th April 2022

* Fix for Marketplace Module data output
* Fix for og:url field output on WebApp/Modules

***

### 2.7.2.0 - 28th February 2022

Support for new Marketplace Module file paths

***

### 2.7.1.0 - 12th January 2022

New 'match\_type' option on WebApp/Module filtering. [Docs](../../webapps/layouts/searching-advanced-filtering.md)

***

### 2.7.0.4 - 20th December 2021

Minor patch to support new field types

* Image (Array)
* Folder
* Number (Integer)
* Number (Float)
* Boolean

***

### 2.7.0.3 - 6th December 2021

Minor patch to fix output of Module collections

***

### 2.7.0.2 - 1st December 2021

Minor patch to add support for Module caching

***

### 2.7.0.1 - 23rd November 2021

Minor patch to add support for [eCommerce v1.10.0](/developer-tools/release-notes/module-ecommerce-changelog.md)

***

### 2.7.0.0 - 15th November 2021

**Modules - Front-end item submission**

You can now insert Module Item Forms from Toolbox in Siteglide, and have users submit items (Blog, Events, Products, etc.) themselves.If an old version of a Module is missing the necessary layout for this, then you can reinstall the Module to set this up. Alternatively, edit the Module structure and simply 'Save' what is already there.

* [Docs](../../modules/go-further-modules/front-end-submit-modules.md)
* [Roadmap](https://roadmap.siteglide.com/siteglide-roadmap/p/front-end-forms-for-modules)

### 2.6.6.0 - 9th November 2021

* Site Search - Updated query to now search slug and metadata as well as the rendered content
* Sitemap XML - Updated homepage to use root URL, rather than the page slug (e.g. /home) - [Roadmap](https://roadmap.siteglide.com/feature-requests/p/sitemap-xml-update-home-page-to-root-url)
* WebApps - Cache - Added support for URL parameters so this feature now works with search
* WebApps - Category item output - When asking for items in a category you can now make sure it only looks in that category, and not any sub-categories. To do this, use `show_all_sub_items: 'false'`

***

### 2.6.5.8 - 2nd September 2021

* Patch to fix a conflict in CRM custom fields and Address fields on some Forms

***

### 2.6.5.7 - 25th August 2021

* Patch for Category detail views still showing when Category is disabled

***

### 2.6.5.5 - 5th August 2021

* Patch for pagination issue on Blog list views

***

### 2.6.5.4 - 15th July 2021

* Fix for compatibility between eCommerce and Custom Field Sets

***

### 2.6.5.3 - 8th July 2021

* Added support for `s_redirect` on standard Forms and front-end WebApp item Forms, to allow for custom redirects after submission
* Fixed an issue where reCaptcha failures weren't reported correctly
* Fixed an issue where Categories were still showing even after being deleted

***

### 2.6.5.2 - 3rd June 2021

* Support for the latest version of Bootstrap (5.0.1) for Studio

***

### 2.6.5.1 - 2nd June 2021

* Support for CRM Company data on Forms

***

### 2.6.5.0 - 17th May 2021

* Support for CRM User Address data on Forms

***

### 2.6.4.4 - 13th May 2021

* Patch for custom CRM field data not updating on Form submission

***

### 2.6.4.3 - 5th May 2021

* Patch to stop blank SEO fields outputting on WebApp/Module items

***

### 2.6.4.2 - 27th April 2021

* Patch for eCommerce Products used as a DataSource
* Output eCommerce Products in Sitemap XML

***

### 2.6.4.1 - 22nd April 2021

* Patch for WebApp search for compatibility with the previous update to `records`

***

### 2.6.4.0 - 20th April 2021

* An upgrade for all WebApp and Module data output to improve performance and stability (`customizations` -> `records`)

***

### 2.6.3.7 - 14th April 2021

* Bug - Fix to allow `"` in all form field values

***

### 2.6.3.6 - 9th April 2021

* Bug - Add support for Products and Subscriptions to Site Search

***

### 2.6.3.5 - 1st April 2021

* Forms - Bug fix to support '=' in form field values

***

### 2.6.3.4 - 22nd March 2021

* Improve page load speed by adding caching to Category fetching (most effective on sites with large amount of Categories).

***

### 2.6.3.3 - 21st March 2021

* Minor restructuring of Categories to support Import/Export

***

### 2.6.3.2 - 16th March 2021

* Support for Studio with Bootstrap 5

***

### 2.6.3.1 - 16th February 2021

* Added filtering/sorting support for eCommerce

***

### 2.6.3.0 - 18th January 2021

* Added a new flag to the `category_items` include as an option to fetch Categories differently - `show_all_sub_items` - When set to 'true' all items from within sub-Categories will be output, as well as the items within the specified Category

***

### 2.6.2.0 - 30th December 2020

* Added another layer of Form validation, to remove reliance on the `.required` class. If this class is missing, submissions will be validated server-side, and any errors fed back to the front-end before further progressing the submission.

***

### 2.6.1.0 - 10th December 2020

* Support for the new 'Custom Array' field type
* Fix for WebApp location searching
* Made CRM Custom Field output easier by giving you access to field names (e.g. `this['User Field XYZ']`)

***

### 2.6.0.0 - 26th November 2020

* Support for CRM Custom Fields on front-end Forms
* Image fields on Categories
* Location filtering on Modules
* Secure Module items
* Fixed a bug where checkboxes and multi select boxes weren't working on Forms

***

### 2.5.0.2 - 5th November 2020

* Minor field changes ready for upcoming Module Custom Field updates

***

### 2.5.0.1 - 2nd November 2020

* Patched an issue with Form Submission when fields were used which submit multiple values e.g. Checkboxes

***

### 2.5.0.0 - 28th October 2020

* _Forms_ - Updated the submission process to reduce site usage costs\
  **Note: This is includes a change to all FormConfiguration files for Forms and WebApps. Any use of CLI without first pulling the latest file could revert the change back to a broken state. To manually fix, change `resource: Customization` to `resource: form_1` (that is an example; it should match the FormConfiguration name)**
* _WebApps_ - You can now add a button so front-end submitted items can be deleted by the person that submitted them

***

### 2.4.11.0 - 7th October 2020

* Track the steps of a Form Submission so you can add a progress bar
* Added a new helper function to make it easier to write custom error functions for Form submissions. The helper function will format all errors to Strings, helping you focus on displaying them to your Users. We've also added a new example here
* Support for upcoming Siteglide Studio release

***

### 2.4.10.2 - 1st October 2020

WebApp location coordinates - There was a mistake in our release that caused the coordinate values to be flipped (latlong instead of longlat). This has now been fixed.

All docs have been updated accordingly, so please re-read and update your layouts:

* [WebApps - Searching by location](../../webapps/layouts/searching-by-location.md)

You will need to update all WebApp items to this new format. Simply re-search for the location, and select again from the dropdown, or you can swap the coordinate values manually. If you have a large amount of data to migrate to this new format please get in touch with support, and we can handle the conversion.

***

### 2.4.10.1 - 24th September 2020

* WebApp location searching
* Fix to allow multiple site searches on a page - [Roadmap](https://roadmap.siteglide.com/feature-requests/p/allow-multiple-site-search-forms-on-a-page-on-the-same-page)

***

### 2.4.9.2 - 4th September 2020

* Support for structural changes introduced in [Secure Zones 1.1.0](/developer-tools/release-notes/module-secure-zones-changelog.md)

***

### 2.4.9.0 - 14th August 2020

* Support for Secure WebApp items

***

### 2.4.8.4 - 11th August 2020

* Verify response of reCAPTCHA v2

***

### 2.4.8.3 - 9th July 2020

* Fix Category slug output for some sites
* [Reduce whitespace in code source](https://roadmap.siteglide.com/bugs/p/whitespace-in-page-source)

***

### 2.4.8.1 - 7th July 2020

* Minor fix for including a list of WebApp items on an eCommerce Product page

***

### 2.4.8.0 - 21st May 2020

* WebApp Edit Forms - [Roadmap](https://roadmap.siteglide.com/feature-requests/p/webapps-front-end-editing)
* Form confirmation Pages - [Roadmap](https://roadmap.siteglide.com/feature-requests/p/ecommerce-make-more-data-available-about-a-users-order-on-confirmation-page-afte)
* Official release of an update to support forms on shared devices. This has been in place for some time as a trial - [Roadmap](https://roadmap.siteglide.com/bugs/p/forms-overwriting-crm-records)
* Fix for og:image on Module detail pages
* Performance upgrade for sites with a large amount of categories
* Fix to allow multiple File Upload fields in a Form
* Added feature for previewing Images when a file is uploaded front end

***

### 2.4.7.0 - 7th May 2020

* [Support for eCommerce Update 0.12.0](/developer-tools/release-notes/module-secure-zones-changelog)
* Sitemap generation

***

### 2.4.5.0 - 27th April 2020

* [Support for eCommerce Update 0.11.0](/developer-tools/release-notes/module-secure-zones-changelog)

***

### 2.4.4.0 - 22nd April 2020

* [Support for Events Module](/developer-tools/release-notes/module-events-changelog.md)
* Fix for multiple reCAPTCHA Forms on a Page

***

### 2.4.3.0 - 15th April 2020

* Further performance updates for [DataSource fields on WebApps](../../ecommerce/get-started-ecommerce/cart-checkout-and-quotes/product-views/related-products.md)
* Bug fix for WebApps showing more than 1 item on their detail view
* Pagination update to support upcoming Modules (Events, Media Downloads)

***

### 2.4.2.8 - 30th March 2020

* Performance improvements on Categories. Mainly noticeable on sites with a very large amount of Categories.
* Fixed a bug with multiple Custom Field Sets on a form

***

### 2.4.2.5 - 25th March 2020

* Set a default layout (of 'default.liquid') for custom pagination that's included outside the scope of a WebApp list view
* Front-end file upload is now direct-to-S3

***

### 2.4.2.4 - 23rd March 2020

* Fix for CFS updating on form submissions
* Stop overwriting sitemap.xml and robots.txt on each update
* Update FontAwesome to v5 in locations missed in v2.4.2.1
* Site Search - Allow WebApp items with no detail view to show in results.
* Categories - Big performance upgrade, with no action required by users to take advantage of this.

***

### 2.4.2.3 - 13th March 2020

* Fix for recaptcha after unpublished changes from Google

***

### 2.4.2.2 - 6th March 2020

* **Custom Pagination layouts** - You can now define the layout for pagination. [Find more information, and usage docs here](../../sitebuilder/using-sitebuilder/sitebuilder-liquid-includes/pagination.md)
* **Datasource performance updates** - We've greatly improved performance of Datasource output. [Find more information, and usage docs here](../../ecommerce/get-started-ecommerce/cart-checkout-and-quotes/product-views/related-products.md)

***

### 2.4.2.1 - 17th February 2020

* Updated FontAwesome to version 5
* Auto-inserted a meta viewport tag which is required for our layouts

***

### 2.4.2.0 - 14th February 2020

* Browser Support updates

***

### 2.4.1.3 - 10th February 2020

* Minor patch on previous update

***

### 2.4.1.2 - 6th February 2020

* **Forms** - Fix an issue with some form submissions in Microsoft's Edge browser
* **Site Search** - Added support for buttons to submit the search, rather than relying on keyboard controls - [https://roadmap.siteglide.com/bugs/p/site-search-on-smaller-devices-a-search-button-will-reduce-reliance-on-keyboard](https://roadmap.siteglide.com/bugs/p/site-search-on-smaller-devices-a-search-button-will-reduce-reliance-on-keyboard)
* **Site Search** - Fixed an issue where Pages were showing in search results, even though 'Visible to search' was turned off - [https://roadmap.siteglide.com/bugs/p/pages-searchable-toggle-bug](https://roadmap.siteglide.com/bugs/p/pages-searchable-toggle-bug)

***

### 2.4.1.1 - 11th December 2019

* **reCAPTCHA Security upgrade**

#### Introduction

This week, we are releasing updates to the following:

A more secure reCAPTCHA validation for Forms.
Site Search now allows you to specify a combination of Pages, WebApp and Module Detail Pages to search.
We've also made brand new features available for Beta testing:

eCommerce Quotes- eCommerce customers select items in their Cart and submit a Form to request a Quote for those items without making a Payment.
White-labelling Phase One - Allow Clients to see your Agency Logo in the top-left hand corner of Admin.

#### Improvements

CMS Improvements

reCAPTCHA Security upgrade

Thanks to the Community for feedback on our reCAPTCHA integration , we've made a range of improvements this week.

What's changing?

All Forms now use XHR requests for submitting their data. This allows us to do extra checks on Forms which use reCAPTCHA.

XHR submission is a requirement for forms with reCAPTCHA
Bots which try to submit Forms directly via JavaScript with the .submit() method will fail at the first hurdle regardless of reCAPTCHA.
If you're not using reCAPTCHA, then you can manually alter our code to stop using XHR.
How to get the update?

Update System Files to version 2.4.1.1

To see this update on your form you'll need to simply hit 'Save' on the Form in Siteglide. It will work with both default and custom Layouts.
Site Search- More control over the scope of what is searched

#### What's Changing?

You can now choose any combination of Pages, WebApp Detail Pages and Module Detail Pages to include in your Site Search Results. Use the type parameter.

If you include WebApps in the parameter, Toolbox will also prompt you to select which WebApps you'd like to search.

Also, for searches which include WebApps, you can include the parameter single_field, to only search for WebApp Detail Pages with that specific field e.g. properties.webapp_field_2_1 matching the keyword terms. Note- this will be the real database name of the field- not the user-friendly field name.

How to get this Update?

Visit Admin for your Site and System Files will be updated.
You will then find the Toolbox updated with the new Parameters you can use.
Learn more:

New Features
Admin Features
Whitelabelling - (Beta)

We want to give Partners the ability to show their Clients a white-labelled version of Admin. The first step allows you to replace the logo your Clients see in the Admin with your own. We will release full documentation for this soon when the next feature is ready.

How to use?

In Portal, click your Agency name in left side menu
Upload your logo there, and toggle the 'Whitelabel logo?' switch to on.
Save, and refresh to see your logo in the top left.
This feature is in Beta, so Clients using admin.siteglide.com will not see your agency logo. You can view your agency logo from beta.siteglide.com.
Module Features

eCommerce Quotes- (Beta)

This community-requested feature allows Users to use the Cart as Normal, but complete a Quote Form instead of a Checkout Form.

Features

A new kind of eCommerce Form is now available: Quote Only.
When the Form is completed, it generates an Order using the items in the User's Cart- but does not prompt them to complete any Payment information. The Order appears in the Admin with the status: "Quote Only".
Generating a "Quote Only" order does not decrease the number of items in the Product's Inventory. However, a Product will need to be in stock before it is added to a Cart.

***

### 2.4.1.0 - 3rd December 2019

* **Support for Blog Archive feature**
