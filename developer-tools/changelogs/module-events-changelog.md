# 🛳️ Module - Events - Changelog

### 1.1.0 - 3rd October 2022

* Support for Automations structure

***

### 1.0.4 - 11th February 2021

* Updated default layouts to use [Siteglide Studio](https://help.siteglide.com/article/135-studio-by-siteglide-introduction) (this won't overwrite existing installed layouts)

***

### 1.0.3 - 23rd September 2020

*   Fixed a bug where double quotes in Event names would cause invalid JSON when using default Calendar Layout. This fix will only apply to new Sites so as to not overwrite Layouts you may be using.

    To fix manually on existing Sites, replace the following line in your `item.liquid` file:

`"title": "{{this.name}}",`

...with:

`"title": {{this.name | json }},`

***

### 1.0.2 - 11th August 2020

*   UX improvements to Default Detail Event Layouts.

    New installs of the Events Module will have improved default Detail Layouts. Previously you had to click through to the Product Detail Page to buy tickets, but this can now be done straight from the Events Detail Page. This should mean a simpler UX experience.

    For existing Events and eCommerce Module users, you can easily add this functionality, should you wish to upgrade. Read the "Adding to Cart on the List View" section on the eCommerce docs: [https://developers.siteglide.com/list-layouts](https://developers.siteglide.com/list-layouts)

***

### 1.0.1 - 16th July 2020

* Add [keyword search](https://developers.siteglide.com/browse-events-by-keyword) to default Events List Layout

***

### 1.0.0 - 22nd April 2020

* [Initial release](https://help.siteglide.com/article/133-modules-getting-started)
