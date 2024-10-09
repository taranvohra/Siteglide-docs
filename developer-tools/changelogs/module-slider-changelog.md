# 🛳️ Module - Slider - Changelog

### 1.1.1 - 24th March 2023

* Fix a broken layout (missing '{')

***

### 1.1.0 - 11th October 2022

* Support for Automations structure

***

### 1.0.1 - 12th July 2020

* Added easier support for multiple Sliders of the same Layout to be added to the same Page using the Liquid parameter: `uniq_slider_id` to provide each instance of a Layout with a unique ID that will be selected by the JavaScript. - [Docs](https://developers.siteglide.com/slider)
* Added logic to the Slider Layouts to make sure the Layout contents are not loaded when no Slider Items are available in the Module (after filters are applied). This fixes a bug where if there were no available items, the JavaScript would experience an unhandled error.

***

### 1.0.0 - 7th July 2020

* Slider Module is released. - Add images and content to your Slides in Admin and display on a Site either using our custom Layouts or creating your own. Learn more here: [Slider Module Documentation](https://developers.siteglide.com/slider)
* New Slider Layouts available on Layout Library: [https://layouts.siteglide.com/](https://layouts.siteglide.com/)
