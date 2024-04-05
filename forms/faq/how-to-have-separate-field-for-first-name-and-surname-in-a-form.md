---
description: >-
  Currently a form needs a value of "s_name" to submit properly. Lets take a
  look at how we can include two separate fields into "s_name".
---

# How to have separate field for first name and surname in a Form

Currently a form needs a value of "s\_name" to submit properly. Lets take a look at how we can include two separate fields into "s\_name".

## Introduction

When a [Form is created](https://help.siteglide.com/article/99-forms-getting-started) you'll notice two standard field that are always required; Name and Email. These two fields must have a value when a user submits the Form or it will fail (as the required fields haven't been given). If two separate fields are required for both first name and last name there is a way of getting round this!

### Separate Name Fields

Firstly we'll need to create/ locate the form we need to add custom fields to. Head over to your sites admin, from here click "CMS" and find "Forms" within there. From here you can choose to create or edit a Form (as seen in red highlights):

<figure><img src="../../.gitbook/assets/Screenshot 2024-03-26 153411.png" alt=""><figcaption></figcaption></figure>

Firstly we must create two separate form fields for First name and Last name, to do this click "Add Fields" and name them accordingly:

These must be set to 'required' as they're being inserted into the name field (which will prevent the Form from submitting without a value).

We will be building upon the "default" Form layout as it automatically creates all the correct fields the Form needs to submit. Go to code editor:

`layouts/forms/form_1/default.liquid` (replace form\_1 with the ID of your form).

Copy the code inside this file. Create a new file in Code Editor and paste the content inside:

`layouts/forms/form_1/first_and_last_name.liquid`

### Create a custom Layout:

Now we'll need to create a custom layout. Right click the Form we're working on and select "Create File".

Copy the code from the default layout into here (we'll be using this as a starting point). You'll notice that the full name field has a `type` of "text", this will need to be replaced with "hidden" (this field is just for the database- users don't need to see it!). Remove the label element as it will still display otherwise. Here's what it should look like:

```liquid
{% raw %}
{% comment %}<label for="s_name"></label>{% endcomment %}
<input
  class="form-control required"
  name="{{ form_builder.fields.properties.name.name }}"
  id="s_name"
  type="hidden"
/>
{% endraw %}
```

### Add IDs to custom fields:

Next we must add unique ids to our custom fields, we will use these to combine the two fields later on.

Update each field to include id="lastName" and id="firstName" after the name value. These aren't normally required but will be used to refer to our fields in the following Java Script. Here's what the custom fields should look like:

```liquid
{% raw %}
<label for="form_field_2_4">First Name</label>
<input
  class="form-control required"
  name="{{ form_builder.fields.properties.form_field_2_4.name }}"
  type="text"
  id="firstName"
/>
<label for="form_field_2_5">Last Name</label>
<input
  class="form-control required"
  name="{{ form_builder.fields.properties.form_field_2_5.name }}"
  type="text"
  id="lastName"
/>
{% endraw %}
```

### Include handleNames() function:

Next, we must look at the submit button. Normally it uses the onClick attribute to fire Siteglide's form submit function- but we want it to wait until we've handled the name fields.&#x20;

```html
<button
  type="button"
  class="btn buttonAccent"
  onClick="s_form_submit_v2(this,'form_2')"
>
  Submit
</button>
```

So we switch it to run my `handle_names(this)` function instead, we'll also need to remove 'form\_2' as this submits the form (we. The submit button should look like now:

```html
<button
  type="button" 
  class="btn buttonAccent" 
  onClick="handle_names(this)"
>
  Submit
</button>
```

### Add the handleNames() function:

Lastly we must combine both the fields by adding some Java Script below all of our form fields. This will run the user clicks the "Submit" button, it combines the firstName and lastName fields before submitting the form!

```javascript
<script>
  function handle_names(element) {
    //Store a variable for each field's value
    var firstName = document.querySelector("#firstName").value;
    var lastName = document.querySelector("#lastName").value;
    //The full name must go in this element
    var fullNameElement = document.querySelector("#s_name");
    //Build the full name by adding both names- with a space between
    var fullName = firstName+" "+lastName;
    //Place the full name in the correct field.
    fullNameElement.value = fullName;
    //Now submit the form.
    var contact_form_submit_element = document.querySelector("#contactFormSubmit");
    s_form_submit_v2(element,'form_1');
  }
</script>
```

That's everything!&#x20;

Your form will store the first name and last name within the appropriate fields, but it will also store full name in the required system field.&#x20;

## Related Articles:&#x20;

* [Creating Forms](https://help.siteglide.com/article/99-forms-getting-started#2-creating-and-editing-forms)
