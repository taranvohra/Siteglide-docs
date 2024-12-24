These features allow users to change the key information that identifies them on your site.

<!-- ![](https://downloads.intercomcdn.com/i/o/258038314/977e8edb09dd8197a452d6d8/image.png) -->

# Prerequisites

*   Install the [Secure Zones Module](/crm/quickstart-crm.md)

*   Users must remember their existing password

*   Users must be already logged in

# Introduction

This Article shows how Users who remember their Email address and Password can change these using a Form. If you need a feature for Users who have forgotten their password, try the [Password Reset](/crm/quickstart-crm.md#2-adding-a-password-recovery-page) feature.&#x20;

# Step 1 - Set up a Form&#x20;

Create a Form which will be used to update Users' email address or password.&#x20;

<!-- ![](https://downloads.intercomcdn.com/i/o/258319499/5f68c4e7d61e63062ad8c247/image.png) -->

This Form should have a Secure Zone attached- but this can be an existing Secure Zone that you use for Accounts e.g. "My Account" or an equivalent.&#x20;

You do not need to add any custom fields in the Siteglide Admin in order to use this feature. Instead, the feature will be added solely in the Form Layout.

You may wish to use one Form for updating an email and a separate Form for updating password. This is fine- just adjust these instructions accordingly.&#x20;

# Step 2 - Create a Custom Form Layout

We'll need to modify the Form Layout, so head to Code Editor and create a new Form Layout liquid file. This should be in the same folder as the Form you created in step 1.

<!-- ![](https://downloads.intercomcdn.com/i/o/258320889/1dc7f7aa68ef97197c627c62/image.png) -->

# Step 3 - Add your Form to a Page

You can add your Form to any Page.

<!-- ![](https://downloads.intercomcdn.com/i/o/258319926/fb64165aa155854d73c9e3b3/image.png) -->

Select your Custom Form Layout you made in step 2.

# Step 4 - Add a Secure Zone to that Page

Editing email and password will only work if the User is already logged in. We recommend adding a Secure Zone to your Page to ensure this is the case.

# Step 5 - Add new fields to the Form Layout

In this step we'll be adding fields to the Form Layout which will allow the User to submit new email and password values.

&#x20;Pay close attention to the IDs of these elements, as this is what Siteglide will use to identify them.

```html
<label for="s_email_edit">New Email Address</label>
<input class="form-control" id="s_email_edit" type="email" >
```

*Purpose* - In this field the User will submit a new value for their email address.

```html
<label for="s_password_edit">New Password</label>
<input class="form-control" id="s_password_edit" type="password" >
```

*Purpose* - In this field the User will submit a new value for their password.

On most Siteglide Forms you'll see an email address and password fields with the HTML ID `s_email` and `s_password`. These fields are specifically used for Users to enter their current email address and password.&#x20;

Notice that the fields below we use for Users to provide new values for their email and password use different IDs `s_email_edit` and `s_password_edit`.&#x20;

Remember, you do not need to use a single Form to edit both email and password. You can include these on separate Forms if you wish.&#x20;

You can use custom JavaScript to show or hide the fields when needed. Only when a value is given to the fields will they validate and throw an error if there is a mistake.

*Things to check at the end of this step:*

*   The ID attribute of each field will need to be exactly the same as that used in the documentation in order to work.

*   The fields should not have an HTML `name` attribute. This is because we don't wish the information to be stored in the Case along with other custom fields.&#x20;

# Step 6 - Reveal the Current Password Field to Logged in Users

In order to use this feature the User must:

*   be already logged in

*   enter their existing password again

In this step then, we make sure we are giving the User the opportunity to re-enter their password:

```html
<div class="row mt-4">
  <div class="col">
    <label for="s_password">Current Password</label>
    <input class="form-control required" id="s_password" type="password">
  </div>
</div>
```

The Form Default Layout already includes this Field- however it is hidden from Users who are logged in.&#x20;
The simplest way to complete the step is to remove the logic:

```liquid
{% raw %}
{% unless context.exports.is_logged_in.data -%}
  
{% endif %}
{% endraw %}
```

*Things to Check*

*   Make sure any \<label> tags clearly show which field should be used for current password and which should be used for the new password.&#x20;

*   Make sure the current password field is only included once in the Form Layout

# Step 7 - Optional - Add a confirmation field for additional validation

The last thing the User wishes to do is to reset their password to the wrong value.&#x20;

To provide extra validation, you can add confirmation fields:

```html
<!-- New Email -->
<label for="s_email_edit">New Email Address</label>
<input class="form-control" id="s_email_edit" type="email" >

<!-- New Email Confirmation -->
<label for="s_email_edit_confirm">Confirm New Email Address</label>
<input class="form-control" id="s_email_edit_confirm" type="email" >

<!-- New Password -->
<label for="s_password_edit">New Password</label>
<input class="form-control" id="s_password_edit" type="password" >

<!-- New Password Confirmation -->
<label for="s_password_edit_confirm">Confirm New Password</label>
<input class="form-control" id="s_password_edit_confirm" type="password" >
```

Once you've added a confirmation field, our validation will make sure the email fields match and that the password fields match.&#x20;

If you choose not to add a confirmation field, it will not be required.&#x20;

# Step 8 - Optional - Add autocomplete fields

To help the User's browser to understand the difference between current and new password fields, you could add values to the autocomplete attribute:

*   `autocomplete="current-password"`

*   `autocomplete="new-password"`

```html
<label for="s_password">Current Password</label>
<input class="form-control" id="s_password" type="password" autocomplete="current-password">

<!-- New Password -->
<label for="s_password_edit">New Password</label>
<input class="form-control" id="s_password_edit" type="password" autocomplete="new-password">

<!-- New Password Confirmation -->
<label for="s_password_edit_confirm">Confirm New Password</label>
<input class="form-control" id="s_password_edit_confirm" type="password" autocomplete="new-password">
```

# Next

And you're done!&#x20;

You can use this feature along with our other Front-End CRM features to give Users control over their Data and Credentials on your Site.
