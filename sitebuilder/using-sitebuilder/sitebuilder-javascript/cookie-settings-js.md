# ℹ️ Cookie Settings JS

### Introduction <a href="#introduction" id="introduction"></a>

The cookie settings JavaScript is a lightweight script designed to support SiteBuilder Layouts which modify a cookie in order to store the user's cookie preferences.

Here we'll explain how you can use the features of this script while modifying a layout.

### How it works <a href="#how-it-works" id="how-it-works"></a>

After the user first sets their preferences, these preferences will be stored in a cookie with the name: `sg-cookie-policy-settings` which will expire after a year.

### Loading the script asynchronously <a href="#loading-the-script-asynchronously" id="loading-the-script-asynchronously"></a>

```liquid
{% raw %}
<script async src="https://uploads.prod01.london.platform-os.com/instances/668/assets/modules/module_86/js/v1/sitegurus_cookie_settings.js?updated=1695044532"></script>
{% endraw %}
```

The Liquid will ensure the script is only loaded once on the page.

### Creating Controls to set the preferences <a href="#creating-controls-to-set-the-preferences" id="creating-controls-to-set-the-preferences"></a>

Use the `data-sg-cookie` data attribute to set an element as a control that will modify the settings. The value of the data-attribute will be the value of the preferences cookie when set. Theoretically you can set it to any string, but normally you'll want to differentiate between a simple set of choices.

Since the script is loaded asynchronously, the controls won't have event listeners attached immediately. Meanwhile the user may be eager to access the rest of the site and may try to dismiss the popup as soon as possible. Therefore, we recommend you start the controls with styling which indicates that they are disabled. You can then use the `data-sg-cookie-btn-enabled` data-attribute to store classes which you would like to use to style the button once it is enabled. The script will replace the value of the class attribute with the value of the data-attribute when the script is ready.

#### Using Buttons <a href="#using-buttons" id="using-buttons"></a>

```liquid
{% raw %}
<button disabled data-sg-cookie="all" type="button" class="text-white bg-blue-400 dark:bg-blue-500 cursor-not-allowed font-medium rounded-lg text-sm px-5 py-2.5 text-center" data-sg-cookie-btn-enabled="text-white bg-primary-700 hover:bg-primary-800 focus:ring-4 focus:outline-none focus:ring-primary-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-primary-600 dark:hover:bg-primary-700 dark:focus:ring-primary-800" >Accept all</button>
<button disabled data-sg-cookie="essential-only" type="button" class="text-white bg-blue-400 dark:bg-blue-500 cursor-not-allowed font-medium rounded-lg text-sm px-5 py-2.5 text-center" data-sg-cookie-btn-enabled="text-gray-500 bg-white hover:bg-gray-100 focus:ring-4 focus:outline-none focus:ring-primary-300 rounded-lg border border-gray-200 text-sm font-medium px-5 py-2.5 hover:text-gray-900 focus:z-10 dark:bg-gray-700 dark:text-gray-300 dark:border-gray-500 dark:hover:text-white dark:hover:bg-gray-600 dark:focus:ring-gray-600">Accept essential cookies only</button>
{% endraw %}
```

#### Using form elements <a href="#using-form-elements" id="using-form-elements"></a>

```liquid
{% raw %}
<div class="p-6 border-t border-gray-200 rounded-b dark:border-gray-600">
  <div class="flex items-center mb-4">
    <input  disabled data-sg-cookie="all" id="cookie-preference-1" type="radio" value="" name="cookie-preference" class="ml-2 text-sm font-medium text-gray-400 dark:text-gray-500" data-sg-cookie-btn-enabled="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">
    <label for="cookie-preference-1" class="ml-2 text-sm font-medium text-gray-900 dark:text-gray-300">Accept all</label>
  </div>
  <div class="flex items-center mb-4">
    <input  disabled data-sg-cookie="essential-only" id="cookie-preference-2" type="radio" value="" name="cookie-preference" class="ml-2 text-sm font-medium text-gray-400 dark:text-gray-500" data-sg-cookie-btn-enabled="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">
    <label for="cookie-preference-2" class="ml-2 text-sm font-medium text-gray-900 dark:text-gray-300">Accept essential cookies only</label>
  </div>
</div>
{% endraw %}
```

#### Accessing the current settings value <a href="#accessing-the-current-settings-value" id="accessing-the-current-settings-value"></a>

Note in this example above, we also use Liquid `context.cookies.sg-cookie-policy-settings` to set a default checked value to the radio currently active on page load.

### Success event <a href="#success-event" id="success-event"></a>

Since this uses data-attributes, we don't have a callback function on success. Instead we set a custom event on the document:

```javascript
document.addEventListener('sgCookiePreferencesAfterUpdate', success);
function success(event) {
  console.log(event.details)
}
```

Accessing `event.details` will let you know the current state of the preferences, however, you could of course use JS to check the cookies directly.

The script _does not_ actually remove google analytics cookies which are already set. Layouts will disable any analytics script wrapped inside their Liquid logic. If you do wish to delete analytics cookies directly, we recommend you do this in a function called after the success event.
