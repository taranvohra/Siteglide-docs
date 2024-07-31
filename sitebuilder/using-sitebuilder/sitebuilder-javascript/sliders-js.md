# ℹ️ Sliders JS

### Introduction <a href="#introduction" id="introduction"></a>

The sitegurus\_sliders\_javascript\_api is a script which allows multiple layouts on the same page to run fully responsive sliders powered by Swiper.js.

We chose Swiper.js because it's a well maintained library, which has a very wide range of configuration options, allowing all sorts of slider effects.

SiteBuilder layouts can use any front-end JS library, so using this API is completely optional. However, for those layouts which do use it, this article aims to help you make the most of the benefits.

Read more about the Slider Module here]\(/documentation/sitebuilder/modules\_and\_more/sliders).

### How Swiper.js is initiated <a href="#how-swiperjs-is-initiated" id="how-swiperjs-is-initiated"></a>

Each of the layouts which uses this script will include the following code for loading the script and setting up the configuration for the slider:

```liquid
<script>
  if(!window.sitebuilderSwiperConfig ) {
    window.sitebuilderSwiperConfig  = {};
  }
  window.sitebuilderSwiperConfig[''] = {
    initiated: false,
    //Choose any configuration from the docs here: https://swiperjs.com/swiper-api
    config: {
      slidesPerView: 1
    }
  }
  if(typeof window.sitebuilderSwiperInit == 'function') {
    //In case script is loaded already. Run initiation again. Sliders in the config will only be initiated if initiated property is set to false.
    window.sitebuilderSwiperInit();
  }
</script>

  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/swiper@8/swiper-bundle.min.css"/>
  <script async src="https://uploads.prod01.london.platform-os.com/instances/668/assets/modules/module_86/js/sitegurus_sliders_javascript_api.1.js?updated=1695044531"></script>
```

This code is included inside the layout in order to allow some level of configuration by developers, while maximising performance:

1. It loads asynchronously along with its dependencies, and includes Liquid logic to ensure it only runs once.
2. It allows multiple slider layouts to be initialised on the same page, each with different settings, without conflicts.
3. It allows the developer to configure the settings and write JS which manipulates the sliders after initialisation, should they wish.

This is achieved mainly through creating a globally-scoped variable `window.sitebuilderSwiperConfig`. Each inidivudal slider is added to this object with a unique name and important properties are stored against it. Once the JavaScript is loaded, it reads this variable and initialises the sliders.

#### How to update the configuration <a href="#how-to-update-the-configuration" id="how-to-update-the-configuration"></a>

You will see inside the layout a `config` object:

```js
window.sitebuilderSwiperConfig[''] = {
  initiated: false,
  config: {
    slidesPerView: 1
  }
}
```

This contains the configuration settings required to acheive the Swiper.js effects the layout has out of the box, but it can be edited as per the [parameters](https://swiperjs.com/swiper-api#parameters) in the Swiper.js docs.

For example, changing `slidesPerView` to `2` would show 2 slides on the page at a time.

Note that some properties, for example pagination, may require you to add [markup](https://swiperjs.com/swiper-api#swiper-full-html-layout) to the HTML alongside your changes to the JS object.

Only the config property directly maps to the Swiper.js documentation, the initiated and onInit properties are used by Sitegurus behind the scenes.

#### How to programatically update the Slider <a href="#how-to-programatically-update-the-slider" id="how-to-programatically-update-the-slider"></a>

Under the configuration, you can define a callback function in the `onInit` property. This will allow you to run your own JavaScript when you can be confident that the Slider has initiated. The function will provide you a reference to the initiated slider which you can use to run any [methods](https://swiperjs.com/swiper-api#methods-and-properties) from the documentation:

In the example below, we show you how to add a button to manipulate the slider once it is ready.

```liquid
<button id="reset">Back to start</button>
<script>
  window.sitebuilderSwiperConfig[''] = {
    initiated: false,
    config: {

    },
    onInit: callbackFn
  }
  function callbackFn(instance) {
    //When the slider (stored in instance parameter) is ready, initialise the custom reset button.
    var btn = document.querySelector('#reset');
    btn.addEventListener('click', function() {
      instance.slideTo(0, 0.3, true);
    });
  }

</script>
```

The references to each initialised slider are also stored inside the window.sitebuilderSwiperConfig object.
