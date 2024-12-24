{% hint style="info" %}
The newer and similarly named [Live Updates API](/sitebuilder/using-sitebuilder/live-updates-api.md) from the SiteBuilder module provides a comprensive way to update or re-render layouts after a change.
{% endhint %}

A JavaScript function runs each time the cart is updated and refreshes the quantity of items in the cart for any element with the data attribute data-s-e-live-cart-quantity.

For example:

```liquid
{% raw %}
<span data-s-e-live-cart-quantity>{{items_in_cart}}</span> 
{% endraw %}
```

Here, on page load, the span will contain the amount of items in the cart. The data attribute attached will ensure that this number is kept updated by user interactions (empty cart, add products, etc.)

You can also use the function s_e_live_cart_update()  to simply return the amount of items in the cart. This is useful if you have any custom JavaScript processes you'd like to run that rely on the latest cart quantity value.