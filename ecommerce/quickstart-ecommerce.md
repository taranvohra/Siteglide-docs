# 🚀 Quickstart: eCommerce

{% hint style="info" %}
This Quickstart guide covers the basics of setting up an eCommerce store using SiteBuilder. To build your layouts from scratch (not using SiteBuilder) you would just create your own Layouts either in Code Editor or via CLI.
{% endhint %}

We strongly recommend starting from the template if you're not familiar with Siteglide or the eCommerce module in particular:

{% content-ref url="../sitebuilder/setup-sitebuilder/create-site-from-template.md" %}
[create-site-from-template.md](../sitebuilder/setup-sitebuilder/create-site-from-template.md)
{% endcontent-ref %}

Most of these steps will be already done for you if you use the Template, you can simply customise each section to suit your store.

## Step 1: Install the eCommerce Module

Ensure the eCommerce Module is installed:

<figure><img src="../.gitbook/assets/Siteglide-Modules-eCommerce-Install.png" alt=""><figcaption></figcaption></figure>

For more help managing Modules follow the dedicated guide:

{% content-ref url="../portal/sites/install-and-manage-modules.md" %}
[install-and-manage-modules.md](../portal/sites/install-and-manage-modules.md)
{% endcontent-ref %}

## Step 2: Create and Manage Products

You can create and edit items as well as manage them via CSV using the Import/Export features:

<figure><img src="../.gitbook/assets/Siteglide-eCommerce-Products-List.png" alt=""><figcaption></figcaption></figure>

## Step 3: Product List Layout

To display the Products on the website you will need to setup the Product List Layout.&#x20;

{% hint style="info" %}
This will already be done for you if you use our eCommerce Template.
{% endhint %}

You can install a Layout via SiteBuilder:

<figure><img src="../.gitbook/assets/Siteglide-eCommerce-Product-List-SiteBuilder-Layout.png" alt=""><figcaption></figcaption></figure>

You then need to choose where to output the list of Products, in this example (the eCommerce Template) we are listing all products on the Shop page using the pl-1 layout from SiteBuilder:

<figure><img src="../.gitbook/assets/Siteglide-eCommerce-Product-List-Page-Include.png" alt=""><figcaption></figcaption></figure>

Once done you can preview the page and see the items:

<figure><img src="../.gitbook/assets/Siteglide-eCommerce-Product-List-Page-View.png" alt=""><figcaption></figcaption></figure>

## Step 4: Product Detail Layout

To be able to click into a product and view more details than shown on the list view you will need to setup a Product Detail Layout.

We recommend doing this via SiteBuilder but you can code one from scratch too:

<figure><img src="../.gitbook/assets/Siteglide-eCommerce-Product-Detail-SiteBuilder-Layout.png" alt=""><figcaption></figcaption></figure>

You then need to set the Detail Layout in the Product Table settings by clicking blue 'View Table' button:

<figure><img src="../.gitbook/assets/Siteglide-eCommerce-Products-List.png" alt=""><figcaption></figcaption></figure>

Then select the Detail Layout, you should see the Layout you've just installed via SiteBuilder:

<figure><img src="../.gitbook/assets/Siteglide-eCommerce-Product-Table-Settings.png" alt=""><figcaption></figcaption></figure>

## Step 5: Cart Page Layout

Next we'll setup the Cart. Again we'll install a SiteBuilder layout:

<figure><img src="../.gitbook/assets/Siteglide-eCommerce-Cart-SiteBuilder-Layout.png" alt=""><figcaption></figcaption></figure>

Then output the cart onto a page using the new layout:

<figure><img src="../.gitbook/assets/Siteglide-eCommerce-Cart-Page-Include.png" alt=""><figcaption></figcaption></figure>

You can then view the Cart Page:

<figure><img src="../.gitbook/assets/Siteglide-eCommerce-Cart-View.png" alt=""><figcaption></figcaption></figure>

## Step 6: Checkout Page Layout

The Checkout works in a very similar way to the Cart but the Checkout Layouts in SiteBuilder can be found under Forms not eCommerce:

<figure><img src="../.gitbook/assets/Siteglide-eCommerce-Checkout-SiteBuilder-Layout.png" alt=""><figcaption></figcaption></figure>

Then insert the Checkout onto a page using the new Layout:

<figure><img src="../.gitbook/assets/Siteglide-eCommerce-Checkout-Page-Include.png" alt=""><figcaption></figcaption></figure>

Finally you can view the Checkout page to check it's all working correctly:

<figure><img src="../.gitbook/assets/Siteglide-eCommerce-Checkout-View.png" alt=""><figcaption></figcaption></figure>

## Step 7: Setup your Payment Gateway

You can run multiple payment gateways on Siteglide but we strongly recommend using Stripe. Here's an example of how to get setup with Stripe very easily as it's fully integrated:

<figure><img src="../.gitbook/assets/Siteglide-eCommerce-Payment-Gateways-List.png" alt=""><figcaption></figcaption></figure>

You simply need to add your Live and Test Public Keys/Secret Keys. We recommend using the Test Keys first until you're ready to make a real payment:

<figure><img src="../.gitbook/assets/Siteglide-eCommerce-Payment-Gateways-Stripe.png" alt=""><figcaption></figcaption></figure>

## Next Steps

You can totally customise how your eCommerce store works in Siteglide. Here are a few features you might want to look at next:
/ecommerce/get-started-ecommerce/cart-checkout-and-quotes/product-views/shipping-selection/shipping-options
{% content-ref url="../ecommerce/get-started-ecommerce/cart-checkout-and-quotes/product-views/shipping-selection/shipping-options.md" %}
[shipping-options.md](../ecommerce/get-started-ecommerce/cart-checkout-and-quotes/product-views/shipping-selection/shipping-options.md)
{% endcontent-ref %}

{% content-ref url="../ecommerce/get-started-ecommerce/cart-checkout-and-quotes/product-views/discount-selection/discount-codes.md" %}
[discount-codes.md](../ecommerce/get-started-ecommerce/cart-checkout-and-quotes/product-views/discount-selection/discount-codes.md)
{% endcontent-ref %}

{% content-ref url="../ecommerce/get-started-ecommerce/about-the-ecommerce-module.md" %}
[about-the-ecommerce-module.md](../eCommerce/get-started-ecommerce/about-the-ecommerce-module.md)
{% endcontent-ref %}
