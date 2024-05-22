# 📋 Steps to Changing Form Styling on Submission Using CSS

When a Form submits, it can take a moment to make the requests it needs. Here's how you can use CSS to show submission progress.

## Introduction

When a [Form](https://help.siteglide.com/article/99-forms-getting-started) submits, it can take a moment to make the requests it needs. This is especially true with eCommerce Forms which need to make multiple requests for security reasons.

This Article will explain how you can use CSS to show submission progress and let the User know your Form is still submitting without errors.

You may also be interested to read about how you can use a custom validation function to change the way the Form behaves when validation errors are found: [Custom JavaScript Validation for Forms](https://developers.siteglide.com/custom-javascript-validation-for-forms)

## Step 1) Inspect The CSS Class

Firstly, follow the steps in your browser to open up the inspect tool.

When you submit a Form, the HTML Form element has two class names added to it:

* `form_submitting`
* `form_x_submitting` where x represents the ID of the Form in Admin

These classes should be removed if the Form is interrupted by a valid error, e.g. validation errors, so targeting one of these classes should tell you that the Form is busy submitting and the User should wait for completion.

## Step 2) Optional - Add a CSS rule to Restyle the Form Itself During Submission

In this example, we'll use CSS to select all Forms that are busy submitting globally. You may choose to select particular Forms differently.

```html
<style>
  form.form_submitting {
    opacity: 0.3;
  }
</style>
```

## Step 3) Optional - Add a CSS rule to Restyle a Form Child Element During Submission E.g. Adding a Spinner

In this example, a spinner icon has been added to the Form Layout.

The CSS demonstrates how Front-End CSS is used to achieve a different effect:

{% tabs %}
{% tab title="HTML" %}
```html
<i class="fas fa-spinner fa-5x"></i>
```
{% endtab %}

{% tab title="CSS" %}
```css
.fa-spinner {
  display: none;
}
form.form_submitting {
  opacity: 0.3;
}
form.form_submitting .fa-spinner {
  display: block;
  animation: spin 5s infinite;
}
@keyframes spin {
  from {transform: rotate(0deg);}
  to {transform: rotate(359deg);}
}
```
{% endtab %}
{% endtabs %}
