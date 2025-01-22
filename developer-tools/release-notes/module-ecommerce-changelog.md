# 🛳️ Module - eCommerce - Changelog

### 1.15.0 - 22nd January 2024

* Allow Discounts to apply to specific Products and Categories - [Roadmap](https://feedback.siteglide.com/p/apply-discount-codes-to-specific-products)
* Added a flag to turn off the success alert box on Discounts - [Roadmap](https://feedback.siteglide.com/p/ecommerce-module-discount-code-added-alert)
* Fix for re-order feature when multiple items are in the Order
* Added forloop object to product output

***

### 1.14.5 - 11th December 2024

* Add more logging to Form Submissions to support debugging
* Fix for sessions not tracking correctly on first time visit to a site
* Fix for an issue with inventory not calculating correctly in some rare cases
* Turn off PayPal item breakdown if it throws an error, and just send over the total price, rather than blocking payment entirely
* Improved process of Discount Code checker on Cart pages

***

### 1.14.4 - 16th July 2024

* Discounts - New option to choose when a percentage discount is applied - before, or after tax calculations - Default is 'after'

***

### 1.14.3 - 28th June 2024

* Cart - Remove items that are expired or not yet released

***

### 1.14.2 - 25th June 2024

* Updated security as outlined in [System Files update v2.8.2.4](https://docs.siteglide.com/en/developer-tools/changelogs/module-system-files-changelog#id-2.8.2.4-25th-june-2024)
* Settings - Added a 'Pricing Accuracy' setting to allow you to switch between 2 decimal places and 4 decimal places on pricing for Products, Attributes, and Shipping (as well as showing those values in Order views)

***

### 1.14.1 - 15th March 2024

* Multiple Tax Rates - Can now set multiple tax codes against a currency
* Tax Rounding - Can now change how the tax system rounds prices. System default is 'Round on item', and you can change this to 'Round on row' or 'Round on total' - [Roadmap](https://roadmap.siteglide.com/core-platform/p/vat-calculation-on-ecommerce)
* Order Details - This view in Siteglide has been updated for any new Orders to show more data
* Settings - Fix for eCommerce Settings not loading correctly

***

### 1.13.4 - 6th February 2024

* Add custom callback support for [s\_e\_cart\_update](https://roadmap.siteglide.com/core-platform/p/add-callback-function-to-secartupdate) and [s\_e\_cart\_remove](https://roadmap.siteglide.com/core-platform/p/add-callback-parameter-to-secartremove) - [Docs](https://docs.siteglide.com/en/ecommerce/get-started-ecommerce/cart-checkout-and-quotes/cart/updating-quantity-in-cart#the-s\_e\_cart\_update\_quantity-function)

***

### 1.13.3 - 23rd January 2024

* Now checks if a custom empty cart layout exists, and if it doesn't we fallback to the default layout, rather than displaying an error message - [Docs on how empty cart layouts work](../../ecommerce/get-started-ecommerce/cart-checkout-and-quotes/how-to-set-up-a-shopping-cart-and-guest-checkout-tutorial.md)

***

### 1.13.2 - 22nd December 2023

* Settings - Allow you to set a pre-defined list of Order Status Options that will then appear as a dropdown on the Order Edit view. If no options are set, the field will continue to be free-text

***

### 1.13.1 - 20th December 2023

* Attribute Options - Add Image Array field

***

### 1.12.9 - 16th November 2023

* PayPal - Fixed an issue where products with \`"\` in the name would crash the order create process
* Product Feed - Fixed an issue where HTML entities would break XML generation

***

### 1.12.8 - 17th October 2023

* Stripe - Improve payment flow to accommodate for recent updates to Stripe payment handling and 3D Secure
* Basic Payments - Allow setting of Payment Gateway using include parameters - [Docs](../../ecommerce/get-started-ecommerce/basic-payment-forms/ecommerce-basic\_payment.md)

***

### 1.12.7 - 6th October 2023

* Fixed an issue where owner data wasn't being fetched correctly for Products

***

### 1.12.6 - 17th August 2023

* Patch to fix Payment Methods not being stored correctly

***

### 1.12.5 - 17th July 2023

* Patch to fix rounding issue with Volume Pricing

***

### 1.12.3 - 28th March 2023

* Patch to better handle special characters in Form Names when sending to Stripe

***

### 1.12.2 - 23rd March 2023

* Show Form name in transaction description in Stripe. For example:
  * "Payment Form" -> "Example-Form-Name (Basic Payment Form)"
  * "Checkout Order ID: 123" -> "Example-Form-Name (Checkout - Order ID: 123)"
* Fix for quote forms where no price is set against the product

***

### 1.12.1 - 17th January 2023

* Fix for hCaptcha with PayPal Checkouts

***

### 1.12.0 - 28th October 2022

* Added hCaptcha as a Spam Protection option (default) on Forms

***

### 1.11.0 - 3rd October 2022

Support for Automations structure

***

### 1.10.14 - 18th July 2022

Fixed an issue where products can remain hidden in a user's cart after the product has been disabled.

***

### 1.10.13 - 12th May 2022

Patch for price rounding issue on Product Attributes where decimal tax percentages are in place (introduced in v1.10.11).

***

### 1.10.12 - 22nd April 2022

Patch for Subscriptions where no specific Payment Gateway ID is provided.

***

### 1.10.11 - 13th April 2022

Support for decimal tax percentages - [Roadmap](https://roadmap.siteglide.com/core-platform/p/tax-codes-allow-decimals-in-the-amount). It is a good idea to test this update using your own Siteglide Demo Site in order to make sure calculations are working as you would expect for your project.

***

### 1.10.10 - 12th April 2022

Patch to fix issue when Product Inventory quantity is set as '0' when type isn't 'Global'.

***

### 1.10.9 - 2nd March 2022

Patch to fix edge-case issue when changing Product Inventory type.

***

### 1.10.8 - 15th February 2022

Patch to fix issue with Product Inventory not hiding/showing Products correctly.

***

### 1.10.7 - 27th January 2022

Patch to fix issue with Order Detail view when multiple Products in the Order.

***

### 1.10.6 - 24th January 2022

Patch to fix a recursion issue on Order Detail fetching.

***

### 1.10.5 - 14th January 2022

Patch to improve the consistency of price output in some rare situations on Subscriptions.

***

### 1.10.4 - 4th January 2022

Patch to fix Product and Attribute data not capturing correctly in Orders.

***

### 1.10.3 - 20th December 2021

Minor patch to support new field types - [Docs](../configuration/field-types.md)

* Image (Array)
* Folder
* Number (Integer)
* Number (Float)
* Boolean

***

### 1.10.2 - 7th December 2021

* Allow defined Payment Gateway on Subscriptions, rather than just using the most recently update Payment Gateway
* Patched order\_details output to fix Product+Attribute price calculation (only affected output, not capture or charges)

***

### 1.10.1 - 1st December 2021

Added `remove_default_css` option to Cart output, which allows you to remove the `siteglide_example.css` file from output

***

### 1.10.0 - 23rd November 2021

Structural changes to the Orders database to improve performance and reduce usage.

This change is safe to apply unless you have custom code reliant on the old structure being in place that used the `module_14/order_product` or `module_14/order_product_attribute` tables.

***

### 1.9.2 - 18th November 2021

Patch to fix checkout timeouts on sites with large amount of Product Attributes

***

### 1.9.1 - 5th November 2021

Added support for output of more tax breakdowns:

* Final Item Price - price_total_item\_cost - The total of all Products in the Cart, with any applicable Tax added
* Final Total Tax Amount - price_total_tax\_amount - The total Tax amount applied to any Products or Shipping Option
* Final Total Price Before Tax - price_total_before\_tax - The total price of Products and the selected Shipping Option, before any Tax has been applied

Find the full list [here](/ecommerce/get-started-ecommerce/cart-checkout-and-quotes/cart/cart-layouts.md)

***

### 1.9.0 - 3rd November 2021

You can now add multiple payment method options to a checkout layout -> [Roadmap](https://roadmap.siteglide.com/siteglide-roadmap/p/ecommerce-allow-multiple-payment-gateways-at-once)

***

### 1.8.1 - 13th October 2021

Patch to support inventory checking against Attributes on Cart.

***

### 1.8.0 - 12th October 2021

[Shipping Option Tax](https://roadmap.siteglide.com/siteglide-roadmap/p/ecommerce-add-shipping-tax) - This allows you to set which Tax Codes apply to a Shipping Option, and display prices inc/ex Tax on Cart and Invoice layouts.

***

### 1.7.0 - 16th September 2021

* Product Attributes - Added Inventory control
* Product Attributes - Pricing of Product Attributes is now controlled per currency, rather than 1 charge for all currencies
* Product Attributes - CSV Import/Export is now available from the Product List view
* Added the ability to use custom parameters with PayPal
* We've opened up our eCommerce Order flow, so you can add custom functions before and after payment is successfully taken. More information to follow...

***

### 1.6.6 - 21st June 2021

* Patch to support 'Custom Array' field types in eCommerce

***

### 1.6.5 - 1st June 2021

* Patch for Subscription Stripe Webhooks to fix an issue where they would always return as 'Failed'

***

### 1.6.4 - 17th May 2021

* Support for CRM User Addresses to be used as Shipping & Billing data

***

### 1.6.2 - 27th April 2021

* Patch for Products used as a DataSource

***

### 1.6.1 - 21st April 2021

* Patch to support HTML and special characters in Product Descriptions stored against Quotes.

***

### 1.6.0 - 20th April 2021

* An upgrade to Product output in line with [System Files update v2.6.4.0](https://docs.siteglide.com/en/developer-tools/changelogs/module-system-files-changelog#id-2.6.4.0-20th-april-2021)

***

### 1.5.1 - 14th April 2021

* Bug - Fix to allow `"` in Attribute/Option name
* Added a snapshot of Product Description to Order Products model

***

### 1.5.0 - 16th March 2021

* Tax Code system - [Docs](../../ecommerce2/tax-codes.md)

***

### 1.4.2 - 8th March 2021

* Fix unhandled PayPal error

***

### 1.4.1 - 2nd March 2021

* Patch for spam protection bug (due to platform cookie name change) which was causing an 'Unauthorised' error on payment forms.

***

### 1.4.0 - 16th February 2021

* Volume Pricing - You can now set prices to change depending on how many items are purchased by the user. For example, you might say "buy 1 for $10, or 3 for $8 each" - [Docs](/ecommerce/get-started-ecommerce/cart-checkout-and-quotes/volume-pricing.md)
* Discount Codes on Subscriptions - You can now set up Discount Codes to be used with Subscriptions. For example, you can say "50% off for 3 months" or even use it as a free-trial type code of "100% off for 1 month"
* XML Product Feed - A new System Page that outputs Product data in XML format for RSS feeds
* Sorting and Filtering by Price
* Shipping Options - Added 'display only' price.

***

### 1.3.5 - 11th February 2021

* Updated default layouts to use Siteglide Studio (this won't overwrite existing installed layouts)

***

### 1.3.4 - 18th January 2021

* Allow Shipping Option changes on Checkout Forms
* Minor fix for some applications of Discount Codes with 'live reload'
* Minor fix to get rid of a console warning when updating Pricing in a Cart

***

### 1.3.3 - 8th January 2021

* Fix for Add to Cart buttons

***

### 1.3.2 - 7th January 2021

* Fix for when Order value is equal to a Discount Code's minimum spend
* Added console warnings on some Discount Code implementation to help developers debug issues. Warnings only appear when a potential issue has occurred.

***

### 1.3.1 - 6th January 2021

* Fix for some further issues when displaying Cart and Checkout layouts on the same Page
* Fix for empty Discount Codes on Basic Payment Forms

***

### 1.3.0 - 30th December 2020

#### New

* Basic Payment Forms - Added the ability to use Discount Codes on Basic Payment Forms
* Orders - Added the ability to add a previous Order to your Cart
* Cart - Added a validation function to check that the contents of a Cart are valid before passing the data to the Checkout. Note that this validation was performed server-side before payment, but this now allows for more Cart layout feedback/customisation. For example, checking that there enough inventory to cover the Order

#### Improvements

* Shipping Options - The page refresh upon option selection is now optional
* Product Attributes - Provide more readable property naming on output (e.g. `.image` rather than `.properties['module_field_14/product_attribute_option_5']`)

#### Bug fixes

* Fix to block Discount Codes attempting to force an Order to a negative value
* Fix for a bug where PayPal Discount Codes would be have their 'uses' value reduced even when the payment errors
* Fix for a bug where a random Discount Code could be applied when entering an empty string
* Blocked disabled Attributes from showing on Product list/detail views
* Fix for displaying Cart and Checkout layouts on the same Page

***

### 1.2.0 - 26th November 2020

* Support for eCommerce Product location filtering and Custom Fields
* Image and Display-only Price fields on Attributes

***

### 1.1.6 - 19th November 2020

* Patch for PayPal live mode issues

***

### 1.1.5 - 5th November 2020

* Minor field changes ready for upcoming Module Custom Field updates

***

### 1.1.4 - 29th October 2020

* _Basic Payment Forms_ - Allow access to the Payment amount in autoresponder and workflow emails
* _Basic Payment Forms_ - Allow access to the 'minimum payment' value on Page
* _Cart_ - The 'update quantity' field can now apply updates on change, rather than needing to press an 'update cart' button
* _Buy now_ - Support for sending the user straight to a payment from, rather than simply adding the item to the basket
* _Discount Codes_ - Invalid codes (expired or no uses remaining) can now be removed from your cart

***

### 1.1.3 - 16th October 2020

* Minor patch to cover Pricing field type change from text to integer

***

### 1.1.1 - 14th October 2020

* Fix for issue where setting Product Inventory to "none" prevented Orders being created for that Product.
* Fix for conflict between recent database changes and PayPal Checkout
* Fix for bug in Stripe Subscription Cancellation

***

### 1.1.0 - 8th October 2020

* PayPal Payment Gateway
* Stripe - Store the Siteglide Order ID against the order in Stripe as metadata
* Structural changes to Pricing and Inventory databases in order to improve performance, lower usage costs, and allow for easier filtering/sorting on this data.

All Pricing and Inventory data is now stored directly against the Product, rather than in separate database tables.

Any custom extensions of the existing database structure will require you to change to the new structure before updating your Module. All data will be migrated to these new fields when you update your Module.

***

### 1.0.5 - 23rd September 2020

* Added support for the s_e_update\_price() function on Product List View Pages.\
  Roadmap: [https://roadmap.siteglide.com/bugs/p/ecommerce-selecting-attributes-on-a-product-in-the-list-view](https://roadmap.siteglide.com/bugs/p/ecommerce-selecting-attributes-on-a-product-in-the-list-view)
* Stripe Basic Payment Form Submissions now display the associated Stripe Charge ID next to the Payment Intent ID in the Admin.
* Fixed a bug where the Add to Cart button would sometimes add extra items to the Cart that were previously added and removed.

***

### 1.0.4 - 4th September 2020

* Support for structural changes introduced in Secure Zones 1.1.0

***

### 1.0.2 - 17th August 2020

* Fixed a bug with Discount Codes where some combinations of Products would cause the preview of the discounted amount to be incorrect (there was no problem with the actual discount applied) .

***

### 1.0.1 - 6th August 2020

* Fixed a bug with Quote generation Forms.

***

### 1.0.0 - 29th July 2020

*   With the addition of Subscriptions, we complete the first release of Siteglide eCommerce.

    You can learn more about the new features and how to implement Subscriptions on your sites here: [Subscriptions Overview](/eCommerce/get-started-ecommerce/subscriptions/README.md)

**Upgrading from 0.14.1 for Sites which use Subscriptions**

If you were using the Beta version of eCommerce Subscriptions (versions 0.14.1 and lower) and you have not yet upgraded your eCommerce Module, your Sites will continue to work as normal.

However, after upgrading to the eCommerce Module 1.0.0, Stripe webhooks must be set up.

You should also make sure that your Secure Zones Module is up to date.

***

### 0.14.1 - 20th July 2020

* Bug fix for Checkout sometimes displaying logs.

***

### 0.14.0 - 9th July 2020

* [Custom 'add to cart' button text](https://roadmap.siteglide.com/feature-requests/p/ecommerce-allow-changing-text-on-add-to-cart-button)
* [Custom 'add to cart' callbacks](https://roadmap.siteglide.com/feature-requests/p/ecommerce-custom-callback-function-for-successful-add-to-cart)
* Output CFS data on Order Detail views (and in emails)
* Show Cart total price on Checkout views

***

### 0.13.0 - 24th June 2020

* Spam protection for Stripe endpoints

***

### 0.12.0 - 7th May 2020

* Support for 'Add to cart' button on Product list views
* Order details in Workflow and Autoresponder emails

***

### 0.11.0 - 27th April 2020

* Performance updates for Product output - You should find list views loading far quicker than before this update

***

### 0.10.0 - 22nd April 2020

* Discount Codes
* Cart Live Updating

***

### 0.9.8 - 25th March 2020

* Fix for Custom Field Set output on Product layouts

***

### 0.9.7 - 24th February 2020

* Store Shipping Method name against Order rather that just the ID and cost

***

### 0.9.6 - 14th February 2020

* Browser Support updates

***

### 0.9.5 - 22nd January 2020

* Allow '+' in email addresses used on payment forms

***

### 0.9.4 - 31st December 2019

* Stripe - Check if stored customer exists before processing them

***

### 0.9.3 - 23rd December 2019

* Shipping Options

***

### 0.9.2 - 26th November 2019

* Quotes

\
