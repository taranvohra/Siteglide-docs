# Tax Codes

## Prerequisites

- You have the eCommerce Module installed at version 1.5.0 or higher

## Introduction

You can create Tax Codes in Siteglide and apply them to Products. The Tax Percentage is then applied to that Product if the same currency and Tax Code are applied to the Cart.

## Full Video Tutorial

{% embed url="https://www.youtube.com/watch?v=rmv8QqeAgNg" %}

## Managing Tax Codes

To create a Tax Code, go to eCommerce>Tax Codes and click 'Add new Tax Codes item'. Here you can set the following data:

- **Currency** - The currency this Tax Code can be applied to (e.g. USD)
- **Code** - A free-text field that you can display front-end to indicate what Tax Code is being applied
- **Percentage** - The percentage to add to the Product's Chargeable Price.

## Setting a default Tax Code

To set a default Tax Code for a currency go to eCommerce>Products>Edit Module Structure and in the 'Currencies' you will see a list of all currencies available on your site.

Your created Tax Code will appear in the dropdown of 'Default Tax Code' if it matches that currency's 'Letter Code'.

Setting a default means that when that currency is applied to the Cart, this Tax Code will automatically be activated for Products that use it. If no default is set, then no Tax will be applied until a Tax Code is set by the user front-end.

## Applying Tax Codes to a Product

To apply a Tax Code to a Product, go to eCommerce>Products and click to edit a Product. In the 'Pricing' tab you can select Tax Codes that can be applied to this Product. If that Tax Code is then active front-end, then this Product's price will change accordingly.

You can find out more information about [applying these to your layouts here](/ecommerce/get-started-ecommerce/cart-checkout-and-quotes/cart/cart-layouts.md)

## Applying Tax Codes to Shipping Options

To apply a Tax Code to a Shipping Option, go to eCommerce>Shipping Options and click to edit a Shipping Option. In the 'Pricing' tab you can select Tax Codes that can be applied to this Shipping Option. If that Tax Code is then active front-end, then this Shipping Option's price will change accordingly.

You can find out more information about [applying these to your layouts here](/ecommerce/get-started-ecommerce/cart-checkout-and-quotes/cart/cart-layouts.md)

## Changing Currency or Tax Code

If you want to change currency or Tax Code, rather than using the defaults in eCommerce Settings and Product Structure, then you can find details on how to do so here:

- [How to add a Currency Changer to your site](/ecommerce/get-started-ecommerce/introduction-2/currency-changer.md)
- [How to add a Tax Code Changer to your site](/ecommerce/get-started-ecommerce/introduction-2/tax-changer.md)

## Calculations

We take the 'Chargeable Price' value and calculate the Tax value to 4 decimal places before rounding up to just 2 decimal places.

## Potential Limitations

- If you want to use this Tax Code system then your 'Chargeable Price' values should be excluding Tax, and then Tax Codes set up to apply the correct percentages.
- The Cart value is a total of all Products and Attributes with any relevant Tax applied. Any Discounts are then applied to this 1 total, rather than per item. This can cause reported 'Tax Amount' values to appear inaccurate
- Tax Codes can only be applied to eCommerce Products; not Subscriptions, or WebApp/Module items
- Before [v1.14.1](/developer-tools/release-notes/module-ecommerce-changelog.md#id-1.14.1-15th-march-2024) - All Tax values are displayed and stored to 2 decimal places
- Before [v1.14.1](/developer-tools/release-notes/module-ecommerce-changelog.md#id-1.14.1-15th-march-2024) - You can only have 1 Tax Code active in a session, so if 2 Products have 2 different Tax Codes, then only 1 can be applied.
