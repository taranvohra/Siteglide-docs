# 👀 Orders Reference

## Orders Detail Layout

Within the Orders Detail Layout you will have access to the orders array variable. To display a list of items in the single order, you should add a Liquid loop like this:

```
{% raw %}
{% for order in orders %}
  <!-- {{order.id}} etc. -->
{% endfor %}
{% endraw %}
```

Within the loop, you can use properties of the object within the loop iteration as detailed in the table:

| Field Name     | Liquid Tag            | Description                                           |
| -------------- | --------------------- | ----------------------------------------------------- |
| Order ID       | `{{order.id}}`        | The unique ID of the order                            |
| Order URL      | `{{order.slug}}`      | The unique slug of the order                          |
| Order Full URL | `{{order.full_slug}}` | The unique slug of the order including Order Slug     |
| User ID        | `{{order.user_id}}`   | The unique ID of the Current User                     |
| User Email     | `{{order.email}}`     | The email address of the User who completed the Order |
| Status         | `{{order.status}}`    | The status of the Order                               |
| Price          | `{{order.price}}`     | The Price paid for the Order as a decimal             |
| Currency       | `{{order.currency}}`  | The currency the Order was made in                    |
