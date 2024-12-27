# Storing User's Favourite WebApp / Module Items

Users can "add" or "remove" their favourite WebApp and Module items. You can display them to the User in Lists.

<!-- ![](https://downloads.intercomcdn.com/i/o/255725150/fbf51e897d5cab0a9284ec7b/image.png) -->

## Prerequisites

* You have installed the [Secure Zones Module](/crm/quickstart-crm.md)
* You have added a User Sign Up Form
* A User has logged in

## Introduction

We've added the ability for User's to store their favourite Module items within a "favourite\_items" array, they'll be able to "add" and "remove" items from the list which will be stored alongside the rest of the CRM data available to that User in [user\_details](/crm/users/user-details.md).

Possible Use Cases for this feature include:

* A wishlist of Products
* Bookmarks of favourite Pages
* Giving feedback on parts of a Site the User found helpful.

## Syntax - Including the User Favourites Toggle Button Layout

This Layout will allow the User to add or remove an Item from their favourites.

{% hint style="info" %}
The User Favourites Toggle Layout will only work within an item.liquid file (for Modules) or a WebApp Layout file that has access to \{{this.id\}}.
{% endhint %}

Use this Liquid to include your User Favourites Layout, the only parameter that'll differ for this is the "layout", here you can specify a custom layout: 

```liquid
{% raw %}
{% include 'user_favourites_toggle', layout: 'default' -%}
{% endraw %}
```

`is_favourite` - you can use this within `user_favourites_toggle` layouts to determine if the Module/ Webapp item is already added to the Users favourites like so:

```liquid
{% raw %}
{% if is_favourite != true  %}
  <!-- output add to favourites button -->
{% else %}
  <!--  output remove from favourites button -->
{% endif %}
{% endraw %}


```

### Arguments

Our default Layout contains two buttons which we'd recommend you use for reference when setting this up. Let's have a look at these buttons and what they're doing:

#### Add to Favourites Button

```javascript
<button class="btn btn-success"
 onClick="user_add_to_favourites({{this.favourite_item}},added_success,favourite_toggle_failed)">
 Add to favourites
 </button>
```

#### Remove from Favourites Button

```javascript
<button class="btn btn-danger" 
onClick="user_remove_from_favourites({{this.favourite_item}},removed_success,favourite_toggle_failed)">
Remove from favourites
</button>
```

### Required Arguments for both Buttons

To keep things simple, we've bundled the arguments you need to pass into the function into a single Liquid variable containing a JavaScript array \{{this.favourite\_item\}}.

#### Advanced- modifying the arguments

If you need to modify them, you can split this into following the 4 items in the JavaScript array:

```javascript
[
  "{{this.id}}",  //contains the ID of the Module item being added/ removed.
  "{{this.name}}", //contains the name of Module item being added/ removed.
  "{{context.current_user.id}}", // ID of the User adding/ remove the Favourite item.
  "{{context.authenticity_token}}" // token given to the User, this is required.
]
```

{% hint style="warning" %}
#### A note on security

Even if a malicious User submits a fraudulent User ID argument, we will double check on the server-side, so it won't be possible for them to change the favourites of other Users.
{% endhint %}

### Custom Callback Functions

You can also pass success/ failure functions to the add/ remove buttons.

#### Step 1) Define your functions

```javascript
<script>
  function custom_success_function(type, name, button_element) {
   typeWord = type == 'add' ? "added" : "removed";
   alert('Success! You have ' + typeWord + ' ' + name + 'to favourites'  );
  }
  function custom_error_function(error) {
    alert('error');
  }
</script>
```

_Available arguments for success callback functions:_

* `type - add/ remove` - whether item was added or removed from favourites
* `name` - name of item added/ removed
*   `button_element` - element that fired toggle function

    \*Available arguments for error callback functions: \*
* `error` - error message detailing why function failed

#### Step 2) Add the name of your success function as the second argument to the toggle button's function, and your error function as the third.

If you add an error function, you must add a custom success function.

Note it's important to only add the names of functions at this step- this means without the usual round brackets which would contain arguments- that's because we only want to store the functions now and call them later.

```javascript
<button class="btn btn-success" 
onClick="user_add_to_favourites({{this.favourite_item}},custom_success_function,custom_error_function)">
Add to favourites
</button>
```

### Hiding add/ remove buttons if User isn't logged into Secure Zone

You may want to hide the add/ remove buttons from the User if they aren't logged into a Secure Zone you could do so by wrapping your user\_favourites Layout within this IF statement:

```liquid
{% raw %}
{% if context.current_user %} {% endif %}
{% endraw %}
```

## Syntax - Outputting User's Favourite Module/ Webapp items

Now let's look at how we can output all of the User's Favourite items. The favourite\_items object is stored within the [User Details Layout.](/crm/users/user-details.md)

You can include the user\_details Layout like so:

```liquid
{% raw %}
{% include 'user_details', layout: 'my_layout' -%}
{% endraw %}
```

Layouts for user\_details are stored under the following path: `site Manager/code Editor/layouts/modules>module_5/user_details/my_layout.liquid`

Next within the "user\_details" Layout, you can use the following Liquid variables:

* `favourite_items` - an array of IDs of favourite WebApp and Module Items you can loop over. This is mostly for use in your logic.
* `favourite_items_string` - a comma-separated String of favourite WebApp and Module Items. This is formatted ready to be passed into an item\_ids parameter for filtering WebApp and Module List views. See below.

#### Outputting Webapp favourite items

```liquid
{% raw %}
{%- include 'webapp', id: '1', layout: 'my_layout', item_ids: favourite_items_string -%}
{% endraw %}
```

#### Outputting favourite Products

```liquid
{% raw %}
{%- include 'ecommerce/products', layout: 'default', item_ids: favourite_items_string -%}
{% endraw %}
```

#### Outputting favourite Blog Posts (Modules)

```liquid
{% raw %}
{%- include 'module', id: '3', layout: 'my_layout', item_ids: favourite_items_string -%}
{% endraw %}
```
