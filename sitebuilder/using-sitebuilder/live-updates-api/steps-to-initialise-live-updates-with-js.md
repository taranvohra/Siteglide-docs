# 📋 Steps to Initialise Live Updates with JS

### Initialising Live Updates with the Object Constructor in JavaScript <a href="#initialising-live-updates-with-the-object-constructor-in-javascript" id="initialising-live-updates-with-the-object-constructor-in-javascript"></a>

Until this point, we have focussed on how to use our data-attributes to configure the Live Updates API. In this guide we'll show you how to initialise with JavaScript. This is intended for advanced users, who may wish to extend the functionality.

#### 1) Include the JS <a href="#id-1-include-the-js" id="id-1-include-the-js"></a>

Similar to the Getting Started Section, include the following Liquid to asyncronously load the JS only once per page.

```liquid
{% raw %}
{% if context.exports.sitebuilder.live_update_JS_loaded == blank %}
  <script async src="{{'modules/module_86/js/v1-6/sitegurus_live_update_javascript_api.min.js' | asset_url }}"></script>
  {% assign live_update_JS_loaded = true %}
  {% export live_update_JS_loaded, namespace: sitebuilder %}
{% endif %}
{% endraw %}
```

We'll skip this snippet of code in the next few examples, for brevity.

#### 2) Add an event-listener to watch for the Script to load <a href="#id-2-add-an-eventlistener-to-watch-for-the-script-to-load" id="id-2-add-an-eventlistener-to-watch-for-the-script-to-load"></a>

Since the JS runs asynchronously, the constructor function cannot be invoked immediately. We provide a custom event on the document which can be listened for so that we know when the script is ready.

```liquid
{% raw %}
<script>
  //The live-update module's script is loaded asynchronously, so you must wait for it to be ready before using its functions.
  document.addEventListener('live_update_script_ready', ready);
  function ready() {

  }
</script>
{% endraw %}
```

#### 3) Passing in the Public Key and Initialising <a href="#id-3-passing-in-the-public-key-and-initialising" id="id-3-passing-in-the-public-key-and-initialising"></a>

First, include the module JavaScript via CDN and generate the public\_key on the server-side as shown earlier in this article.

Next, you'll need to pass the public\_key to your JavaScript. You can either:

a) write the JS in an inline `<script></script>` tag and output the public\_key straight into the JS using Liquid\
b) or you can use Liquid to output the public\_key into a data-attribute and fetch it from the DOM when needed. Tip: You may not wish to use a different attribute other than `data-sg-live-update-key`, as this will trigger the default event-listeners in the module if present.\
c) Or you can use Liquid to output the public key as a global JS variable in an inline script tag.

Inline Script Tag example:

```liquid
{% raw %}
<script>
  //The live-update module's script is loaded asynchronously, so you must wait for it to be ready before using its functions.
  document.addEventListener('live_update_script_ready', ready);
  function ready() {
    //Initialise an HTML element to mark it as ready to live-update
    const section = new SitegurusLiveUpdate(
      {
        publicKey: "",
        element: document.querySelector('#mySectionID'),
        liveUpdateComponents: Array.from(document.querySelectorAll('[data-sg-live-update-component]')),
        defaultParams: {
          per_page: 2
        }
      }
    )
  }
</script>
{% endraw %}
```

Refer to the [API Reference](/sitebuilder/using-sitebuilder/live-updates-api/live-updates-reference.md) for the full range of available options which can be used while initialising with JS.

#### 4) Add an HTML control and attach an Event Listener <a href="#id-4-add-an-html-control-and-attach-an-event-listener" id="id-4-add-an-html-control-and-attach-an-event-listener"></a>

```liquid
{% raw %}
<script>
  //The live-update module's script is loaded asynchronously, so you must wait for it to be ready before using its functions.
  document.addEventListener('live_update_script_ready', ready);
  function ready() {
    //Initialise an HTML element to mark it as ready to live-update
    const section = new SitegurusLiveUpdate(
      {
        publicKey: "",
        element: document.querySelector('#mySectionID'),
        liveUpdateComponents: Array.from(document.querySelectorAll('[data-sg-live-update-component]')),
        defaultParams: {
          per_page: 2
        }
      }
    )
    var myControlElement = document.querySelector('#mySectionID').querySelectorAll('button');
    //Use the liveUpdate() method to live-update the component when something happens.
    myControlElement.addEventListener('change', function(button) {

    })
  }
</script>
{% endraw %}
```

#### 5) Trigger a Live Update when the Event Callback runs <a href="#id-5-trigger-a-live-update-when-the-event-callback-runs" id="id-5-trigger-a-live-update-when-the-event-callback-runs"></a>

Earlier we stored a reference to the Live Update instance in a variable called `section`. We can use this now to run the `liveUpdate` method inside the event callback function.

```liquid
{% raw %}
<script>
  //The live-update module's script is loaded asynchronously, so you must wait for it to be ready before using its functions.
  document.addEventListener('live_update_script_ready', ready);
  function ready() {
    //Initialise an HTML element to mark it as ready to live-update
    const section = new SitegurusLiveUpdate(
      {
        publicKey: "",
        element: document.querySelector('#mySectionID'),
        liveUpdateComponents: Array.from(document.querySelectorAll('[data-sg-live-update-component]')),
        defaultParams: {
          per_page: 2
        }
      }
    )
    var myControlElement = document.querySelector('#mySectionID').querySelectorAll('button');
    //Use the liveUpdate() method to live-update the component when something happens.
    myControlElement.addEventListener('change', function(button) {
      section.liveUpdate({
        page: button.dataset.page
      })
    })
  }
</script>
{% endraw %}
```

You can find the full reference for this method and others in the [API Reference](sitebuilder/using-sitebuilder/live-updates-api/live-updates-reference.md). Other methods can be run on the instance in the same way.

