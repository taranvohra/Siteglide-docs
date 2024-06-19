# 📋 Steps to Use Live Updates Methods

This guide will show you how to use methods after data-attributes initialisation. If you want to use the object constructor, look [here](https://www.sitegurus.io/documentation/sitebuilder/live\_updates/guide\_-\_initialising\_with\_js).

### What are Methods? <a href="#what-are-methods" id="what-are-methods"></a>

Methods are another name for functions which you can run on an object in JavaScript.

The Live Updates API builds an object we call an instance for each of the sections of code you add data-attributes to. You can access these and call methods to set advanced options, affecting how the API works.

### Available Methods <a href="#available-methods" id="available-methods"></a>

You can see the full list of available methods in the [API Reference](https://www.sitegurus.io/documentation/sitebuilder/live\_updates/API\_reference)

***

### How to use Methods <a href="#how-to-use-methods" id="how-to-use-methods"></a>

#### 1) Wait for the script to load <a href="#id-1-wait-for-the-script-to-load" id="id-1-wait-for-the-script-to-load"></a>

Since the Live Updates API JS loads asynchronously, you need to get your code to wait for it to finish loaded before accessing it.

We provide a custom event for this, so set an event listener to wrap all your code which will need to work with the Live Updates API (note the window.sgLiveUpdateInitiated variable was added in Live Updates v1-3, you'll need to update your scripts to use it):

```js
if(window.sgLiveUpdateInitiated === true) {
  myFunction();
} else {
  document.addEventListener('live_update_script_ready', myFunction);
}
function myFunction() {
  //Target an instance of SitegurusLiveUpdate and use a method.

}
```

Copy

#### 2) Optional: Add a `data-sg-live-update-section` data-attribute to the layout <a href="#id-2-optional-add-a-datasgliveupdatesection-dataattribute-to-the-layout" id="id-2-optional-add-a-datasgliveupdatesection-dataattribute-to-the-layout"></a>

Adding the `data-sg-live-update-section` with a unique value to the same element where you added `data-sg-live-update-key` allows you to reference it later.

This is useful if you want to use methods on a specific layout. If you want to instead apply the method to all instances of Live Update in a loop, you can skip this step.

#### 3) Access the instance for the layout you're working on <a href="#id-3-access-the-instance-for-the-layout-youre-working-on" id="id-3-access-the-instance-for-the-layout-youre-working-on"></a>

Since using data-attributes automatically initialises the `SitegurusLiveUpdate` object, we provide a global JavaScript variable `window.sgLiveUpdateConfig` (and a custom event on the document element `live_update_script_ready` to inform you when it's ready to access) to provide a list of all the initiated instances.

Each instance is stored within the object against a key which is derived from the `data-sg-live-update-section="your_key"` attribute on the main element, or a incrementally designated number by default.

You can access a specific instance via this key, or loop over them all and run your method on the instance. In the example, replace methodName with the method name from this documentation.

```liquid
<script>
  if(window.sgLiveUpdateInitiated === true) {
    ready();
  } else {
    document.addEventListener('live_update_script_ready', ready);
  }
  function ready() {
    //Access a specific instance with a known ID (see optional step 2.)
    var instance = window.sgLiveUpdateConfig['your_instance_id']
    //Loop over all instances, accessing each in turn
    for(key in window.sgLiveUpdateConfig) {
      var thisInstance = window.sgLiveUpdateConfig[key];
    }
  }
</script>
```

Copy

#### 4) Call the method on the instance <a href="#id-4-call-the-method-on-the-instance" id="id-4-call-the-method-on-the-instance"></a>

```liquid
<script>
  if(window.sgLiveUpdateInitiated === true) {
    ready();
  } else {
    document.addEventListener('live_update_script_ready', ready);
  }
  function ready() {
    //Access the first instance
    var instance = window.sgLiveUpdateConfig['your_instance_id']
    //Call method
    instance.setSuspenseHTML('<div>loading</div>');
  }
</script>
```

Copy

More methods can be found in the [API Reference](https://www.sitegurus.io/documentation/sitebuilder/live\_updates/API\_reference)
