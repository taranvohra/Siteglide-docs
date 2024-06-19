# 🔹 Case From Order ID

### Example <a href="#example" id="example"></a>

```liquid
{% raw %}
{% function case_details = "modules/module_86/front_end/functions/v1/case_from_order_id", order_id: this.id %}
{% endraw %}
```

### Purpose <a href="#purpose" id="purpose"></a>

This function can be fed an order ID, perhaps from a URL and returns the details of the form submission which was made as the order was created. This is useful in order confirmations and order detail layouts.
