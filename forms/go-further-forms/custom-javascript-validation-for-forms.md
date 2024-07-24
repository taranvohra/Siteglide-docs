# 🔹 Forms Error Callback and Validation

This article gives some examples for different ways to validate Siteglide forms on the Front End using JavaScript.

## Introduction

When a User submits a [Form](https://help.siteglide.com/article/99-forms-getting-started), we'll check:

* That the User has filled in the fields correctly
* That additional processes like reCaptcha, payment and Secure Zone sign up were successful

For most errors, we'll provide a single error message which can be displayed. For validation errors, we'll provide both the error message and additional messages for each missing field.

## Marking a Field as Required

Fields must be marked as "required" in the Admin, and in the HTML of your Form Layout, in order for them to trigger the validation process.

```liquid
<input 
  class="form-control required" 
  id="{{ form_builder.fields.properties.form_field_4_1.name }}" 
  name="{{ form_builder.fields.properties.form_field_4_1.name }}"  
  type="text"
>

```

For most fields, we will validate only whether or not a field has been submitted- but for emails we take the extra step of checking whether or not the format of the email is valid.

You can either use Siteglide's default validation message, or write your own custom JavaScript. We'll also provide examples of how you can customise the error messages each provide to your users.

## Default

For most error messages, the default behaviour will be to display an alert.

You can also use the following line of HTML in your form Form Layout file to output the default JS validation error message at the end of your Form- but by default this will only display for validation type error: `<div class="form-error"></div>`

A class of `.input-error` gets added to fields if they fail to validate, which you can select with Custom CSS if you wish to show the User that they should be amended.

```css
.input-error {
    border: 1px solid red !important;
}
```

![](https://downloads.intercomcdn.com/i/o/253713156/c017c7f36c95b360e72aa1e8/image.png)

## Passing your Custom Function in as an Argument

You can write your own custom validation by changing:

`<button onClick="s_form_submit_v2(this,'form_12');">` to be: `<button onClick="s_form_submit_v2(this,'form_12',error);">`

where `error` is the name of your function. e.g.

```javascript
<button onClick="s_form_submit_v2(this,'form_12',error);">

<script> 
  function error(error) { 
    //Sanitize the error message 
    error = s_error_formatter(error);    
    //Display the error message 
    alert(error);   
  }
</script>
```

## Formatting your error message

As in the example above, a custom error function will always be passed the main error as its argument. In the past, some of the integrations we worked with passed errors in different formats, which made writing error functions tricky. We've improved this by adding a newfunction: `s_error_formatter(error);` to sanitize the error message and return the message itself as a String.

This means if you include this helper function, you'll always know to expect the message in a String format.

## Example Function

### Custom Error Messages for Fields

The example below demonstrates the following:

* Displays all kinds of main error messages on the Page
* Does not use alert messages
* Allows you to change the field validation message on a field by field basis in the HTML

\*\*\*Step 1) Add HTML before closing tag \*\*\*`<div id="errorSummary" class="alert alert-danger d-none"></div>`

_**Step 2) Add custom error messages to fields in HTML**_ In our custom code for this example, let's invent a data-attribute `data-custom-msg` to store custom error messages against the field we want to display them for:

```liquid
<input 
  data-custom-msg="You forgot the question field!!!" 
  class="form-control required" 
  id="{{ form_builder.fields.properties.form_field_4_1.name }}" 
  name="{{ form_builder.fields.properties.form_field_4_1.name }}"  
  type="text"
>
```

\*\*\* Step 3) Add CSS\*\*\* The CSS plays a visual role here, but also a functional one- as the boxes displaying the errors should be hidden when the Form is submitting and the Siteglide class can be used to select for this.

```css
  #errorSummary {
    max-height: 100%;
    opacity: 100; 
  }  
  [class*="_submitting"] #errorSummary {
    max-height: 0;
    opacity: 0; 
  } 
  [class*="_submitting"] #errorSummary * {
    display: none;
    opacity: none;  
  }
```

\*\*\*Step 4) Add JavaScript \*\*\*The first part of the function:

1. Formats the main error message
2. Selects the Form elements it needs
3. Deletes old error messages

Next the function loops over the fields with input errors and displays validation messages- after adjusting for any custom messages you've added.

Finally, the function uses a "switch" statement to change the main error message, should you wish (useful for translations) before displaying at the bottom of Page.

See the comments in the code for more explanatory details.

```javascript
function error(error) {
  //Format the error message
  error = s_error_formatter(error);
  //Select the key DOM elements
  var standard_errors = document.querySelectorAll(".input-error:not([data-custom-msg])");
  var custom_errors = document.querySelectorAll(".input-error[data-custom-msg]");
  var old_errors = document.querySelectorAll(".my-input-error");
  var standard_error_message = "<div class=\"my-input-error alert alert-warning\">This field is required.</div>";
  //Delete old error messages
  for (e=0;e<old_errors.length;e++) {
    old_errors[e].parentNode.removeChild(old_errors[e]);
  }
  //Add standard field validation messages
  for (e=0;e<standard_errors.length;e++) {
    var this_error = standard_errors[e];
    this_error.insertAdjacentHTML("afterend", standard_error_message);
  }
  //Add custom field validation messages
  for (e=0;e<custom_errors.length;e++) {
    var this_error = custom_errors[e];
    var custom_message = "<div class=\"my-input-error alert alert-warning\">"+this_error.getAttribute("data-custom-msg")+"</div>";
    this_error.insertAdjacentHTML("afterend", custom_message);
  }
  //Add main error summary from function argument- this includes non-validation errors.
  if(error){
    //Add JavaScript logic here to replace specific error messages with your own text.
    switch(error){
      case "Form submission error: Please fill in all required fields":
        //Example of renaming a specific error- add more cases for each error you wish to change
        error = "Please fill in all required fields";
        break;
    }
    //Output the main error
    errorSummary.classList.remove('d-none');
    errorSummary.textContent = error;
  }
}
```

## Related Articles

* [Forms](https://help.siteglide.com/article/99-forms-getting-started)
* [reCAPTCHA](https://help.siteglide.com/article/99-forms-getting-started#2-spam-protection)
