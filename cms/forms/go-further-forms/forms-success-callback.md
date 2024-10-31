# ℹ️ Forms Success Callback

By default, Siteglide Forms will reload the page after submission.

If you would like to run some alternative JavaScript on the Front-End instead, you can do so by passing in a callback function to the 4th argument:

```liquid
{% raw %}
<button onClick="s_form_submit_v2(this,'form_12',undefined,success_cb);">
<script>
  function success_cb(redirect) {
    //Do something.
  }
</script>
{% endraw %}
```

Here we set the 3rd argument to undefined to "skip" it, but you can use this to set a custom callback function to call when the form submission process encounters an error- see Custom JavaScript Validation for Forms .

Your callback function will receive one parameter redirect which will contain the URL which the Form would normally redirect to. You can choose to use this in your function if you need it. We don't include the data submitted in these arguments, but you can of course use JavaScript to access the data directly from the DOM.

If you wish to run code on the server side after a successful form submission, you have the option of adding Automations instead.
