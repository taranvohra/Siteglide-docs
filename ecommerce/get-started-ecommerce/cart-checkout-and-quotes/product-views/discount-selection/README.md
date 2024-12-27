# 📂 Discount Selection

# Introduction

We're introducing Discount Codes to our eCommerce Module.

Your Client will be able to define and manage codes in the Admin- and manage their offers by setting the release and expiry dates, as well as the maximum number of uses in advance.

You'll be able to implement options in the Cart and Checkout for entering discount codes and the Module will work out the discounted costs for you.

# Managing Codes in the Admin

You can see a list of all Discount Codes under the eCommerce Menu.

![Discount Codes List](/.gitbook/assets/getgist/migrating-assets/products/discounts1.png)

## Available Fields

You can set the following fields when you create or edit a Discount Code:

- Item Name - Gives the discount a name
- Weighting - (optional) - Used in sorting
- Release Date - When should the discount code start being valid?
- Expiry Date - When should the discount code stop being valid?
- Enabled - Should the discount code be enabled or disabled?
- Code - A String of characters for the code a customer will need to enter for - the discount to be valid.
- Type - Should the discount be a percentage of the total Cart value, or a fixed - amount?
- Discount Value - How much of a discount should be given when this code is - entered? Choose a value appropriate to the type you selected e.g. 20 for 20% - or 20.00 for $20.00
- Minimum Spend - Often your Client will want to use the offer to up-sell to the - customer. By setting a minimum spend, the customer will need to spend this - amount before the offer can be used. The offer will apply to the entire value - of the Cart still, not the difference between the minimum spend and the Cart - value.
- Uses Remaining - This sets a total number of uses before the offer - automatically expires. This does not measure the number of times an individual customer uses the offer, rather it measures the number of times the offer has - been used globally. If your Client does not want to set a limit, you can set a - very large number- or your Client can increase the number when it runs low.
- Valid on Payment Form Type - Choose 'Checkout' (default), 'Basic Payment' or 'Subscription'. The discount code will only be applicable to the specified - Form type. This is useful when you have both Checkout Forms and Basic Payment Forms on your Site with different purposes.

# Special Fields for Subscriptions Discount Codes

When "Valid on Payment Form Type" is set to "Subscription", a "Coupon" will be created on the connected Stripe account. Therefore, extra fields are needed for this type:

- Number of Months to Discount - Even if your Subscription's Interval is days or weeks, this field must be measured in whole months. The discount will apply to - every invoice until the months are finished, after which the price will revert - to the price defined in the Subscription's plan.
- Stripe Coupon ID - This field will be filled automatically. You can use it to look up the associated Coupon in the Stripe Dashboard.

# Create a New Discount Code

From the List View, you can create a new Discount Code.

![Discount Codes List](/.gitbook/assets/getgist/migrating-assets/products/discounts2.png)

# Edit an Existing Discount Code

Find your code in the List, and use the pencil icon to edit.

![Discount Codes List](/.gitbook/assets/getgist/migrating-assets/products/discounts3.png)

# Delete a Discount Code

From the Edit screen, you can delete a Discount Code.

![Discount Codes List](/.gitbook/assets/getgist/migrating-assets/products/discounts4.png)

# Orders

If customers have used a Discount Code to make a purchase, you'll be able to see this against their Order. You can see customers' Orders under the eCommerce Menu in Admin.

# Adding an Input Field for Codes in the Cart Layout

In the next Article, we'll show you how to add and develop a Discount Codes Layout.

This will allow Users to type in and apply a Code, or remove a Code if it no longer applies and is preventing them from checking out:

![Discount Codes List](/.gitbook/assets/getgist/migrating-assets/products/discounts5.png)