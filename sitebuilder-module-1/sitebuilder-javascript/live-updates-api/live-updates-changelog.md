# 🗓️ Live Updates Changelog

### Version 1.5 - Released 17th May 2024 <a href="#version-15-released-17th-may-2024" id="version-15-released-17th-may-2024"></a>

* Added option to specify onlyUpdateComponent array of strings in `.liveUpdate()` and `.changeStateTrailingDebounce()` methods.

These specify which components should re-render in the DOM after the update, for example if you pass `.update({onlyUpdateComponent: ['mainResults']});` only the element with data-sg-live-update-component="mainResults" will re-render, not data-sg-live-update-component="filters".

The re-render will still take the same amount of time on the server-side, but this may be helpful to improve UX by supressing any DOM replacements which are annoying to the user.

### Version 1.4 - Hotfix - Released 20th March 2024 <a href="#version-14-hotfix-released-20th-march-2024" id="version-14-hotfix-released-20th-march-2024"></a>

* Regression Bug found where since adding default params option, some types of control element were being ignored. This update should fix this.

### Version 1.4 - Released 21st December 2023 <a href="#version-14-released-21st-december-2023" id="version-14-released-21st-december-2023"></a>

* Added new method `.mergeDefaultParams()` - this is to be preferred in most cases over .setDefaultParams() as the passed object will be merged with existing defaultParams rather than completely overwriting it. Any common params will still be overwritten. This will avoid overwriting module defined internal defaultParams including those that send the original URL over to the endpoint.
* Added new data-attribute `data-sg-live-update-default-param`. This attribute should be given to an HTML form element within a `data-sg-live-update-controls` element. As usual, the element must also have a name to define which parameter it will set. This element will now set a defaultParams property instead of directly setting a parameter. This is useful because you can use the new default elements to set a default then use ordinary elements to override that default when the user makes a change. See reference docs for examples.

### Version 1.3 <a href="#version-13" id="version-13"></a>

* Fixed bug in data-attribute initiated Live Updates where `<select>` form controls would trigger both the `input` and `change` events, creating a duplicate update and small associated delay. Now form controls are either assigned an `input` or `change` event listener depending on the most appropriate one for their type. Please let us know any feedback if you think an input type could be improved by switching to a different event in future.
* Improved reliability: New Custom Event and global variable added to make it easier to execute a function after the asynchronous Live Updates JS is ready, or after any data-attributes have been passed (if using). A new event `live_update_constructor_ready` will fire on the document element when the `new SitegurusLiveUpdate()` constructor is ready to use. We've also added a new global variable `window.sgLiveUpdateInitiated` which tells you when the data-attributes have been read and instances of liveUpdates automatically constructed. Putting these together, you can now use the following code when waiting to use the constructor:

```js
if(SitegurusLiveUpdate) {
  myFunction();
} else {
  document.addEventListener('live_update_constructor_ready', myFunction);
}
```

Copy

You can also use this code if you want to wait for each instance of Live Updates initiated by data-attributes to be ready; Useful if you are using methods to modify them:

```js
if(window.sgLiveUpdateInitiated === true) {
  myFunction();
} else {
  document.addEventListener('live_update_script_ready', myFunction);
}
function myFunction() {
  //Target an instance of SitegurusLiveUpdate and use a method.
  window.sgLiveUpdateConfig['1'].setSuspenseCSSClassList('my-class');
}
```

Copy

This code is more reliable than previous patterns when your own script is running asynchronously, as it should work whether your script or the Live Updates script is executed first.

* Improved reliability - `live_update_end` event used to fire after all synchronous code related to the update had run; it now fires after all synchronous and asynchronous code has run.
* Improved console error messaging for a few scenarios where Live Updates code is incorrectly set up.

### Version 1.2 - Released 9th August 2023 <a href="#version-12-released-9th-august-2023" id="version-12-released-9th-august-2023"></a>

* Only form elements with names will now be automatically initiated as Live Updates filters. This helps avoid unwanted re-renders when typing in elements which are not intended to be used as filters. This helps compatibility with the search function of plugins like [https://github.com/Choices-js/Choices](https://github.com/Choices-js/Choices)

### Version 1.1 - Released <a href="#version-11-released" id="version-11-released"></a>

* New functionality added for modifyHistory, including a method and data-attribute for setting it. When turned on, any changes to live update form elements will push those same changes to the [history API](https://developer.mozilla.org/en-US/docs/Web/API/History\_API). This causes the URL in the browser's address bar to change without reloading the page. It is useful if you want the URL to your live-updates-powered page to be shareable.
* If any of the live-updates filters have an HTML value attribute (with a truthy value) on page load, a live update will run immediately as soon as the JavaScript is ready. This allows you to take a shareable link provided by the above `modifyHistory` feature, or a link from a non-live-updates layout, like a Blog Detail page, load that link and instantly have it apply those filters.
* The combination of these two features is powerful, but we recommend only one live-updates layout has this feature turned on on each page, otherwise you can end up in a loop where one layout's filters update the filters of another.
