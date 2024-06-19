# 👀 SiteBuilder JavaScript

### Introduction <a href="#introduction" id="introduction"></a>

SiteBuilder includes JavaScript files to add in interactive functionality which may not exist in the original design system or library.

#### Performance <a href="#performance" id="performance"></a>

We always load our module JavaScript asynchronously. This means it should not block page render and features will be initiated only when the JavaScript is ready. For example, if there is a button for sharing via Facebook, the button element will load straight away, but clicking it in the first second after page load will do nothing, but a seoncd or two later the functionality will be added.

Even with asynchronous loading, you don't want to load a script if it's not being used. Depending on the library, we'll load some scripts in the Page Template if they are used commonly across the library, whereas more specialised scripts will be included within layouts. Some scripts will not be included at all by default itf they're not generally needed. Feel free to add and remove scripts from your templates and pages if you're happy with the resulting functionality changes.

#### Data Attributes and Constructors <a href="#data-attributes-and-constructors" id="data-attributes-and-constructors"></a>

To start with, most of our JavaScript functions are initiated with data-attributes on particular elements which need functionality added.

As the module grows, we will start to make constructors more easily available so that functions can also be initiated with a new keyword and an options parameter.

See the specific documentation to learn more.

#### Extending or Callbacks <a href="#extending-or-callbacks" id="extending-or-callbacks"></a>

If you want to extend our JavaScript, we recommend waiting for the DOM to finish loading and the required scripts to finish loading first. Normally our scripts have an ID which can be targeted and given a "load" eventListener.

We recommend not using html event attributes to run our JavaScript e.g. `onClick=""` as these will probably attempt to find functions before they are defined.
