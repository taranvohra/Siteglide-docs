# 🗓️ SiteBuilder Changelog

## About SiteBuilder updates and backwards compatibility <a href="#about-sitebuilder-updates-and-backwards-compatibility" id="about-sitebuilder-updates-and-backwards-compatibility"></a>

### Summary <a href="#summary" id="summary"></a>

* Always install updates to the main SiteBuilder Module before any Themes
* SiteBuilder updates won't overwrite your site code
* Uninstalling the SiteBuilder module may cause some code to stop working.

### In Detail <a href="#in-detail" id="in-detail"></a>

We're always adding to SiteBuilder and its associated Theme Modules. However, it's important to us that changes to this module do not cause you problems on your site.

Therefore, we never change the layouts on your site during an update. We only update the "master copy" of the layout in the module. That means brand new layout installs from the module will have updates, while older layouts will continue to function as before.

There are exceptions to this rule, for example Liquid includes which power functionality like dynamic forms. In these cases, we will only modify these files with non-breaking changes. For breaking changes, a new version of the file will be created and linked to new layouts, leaving the old version continuing to function with existing layouts.

For the optimum compatibility, we recommend always making sure the main SiteBuilder module is up to date before updating any SiteBuilder Theme modules. Some Theme module updates may rely on the latest version of SiteBuilder.

## Releases <a href="#releases" id="releases"></a>

### 4.17.2 - Released October 25th 2024

\+ Flowbite Pro Version 1.9.4

* New Admin Table Layouts for Modules:
  * Blog List
  * FAQ List
  * Events List
* 2 New Blog Detail Layouts
* 2 New Form Layouts
* New Accordion WebApp Layout
* Original Blog Detail Layout updated with new features (will roll out to other Blog layouts soon):
  * Google Structured Data Support
  * Support for visiting URL with ?edit=true at end of URL to display edit form (after permission checks). This goes nicely with the Admin Tables which can link to it.
* Updated many modals to be "static" to prevent accidental closing

### 4.17.1 - Released October 2024&#x20;

* Support for new Pro layouts in Preview Mode
* Removed console errors for Live Updates which were unnecessary (logs not errors).
* Flowbite Pro Theme - Version 1.9.4
  * A new eCommerce themed menu layout containing a mini cart preview
    * Cart preview includes product thumbnails, names and prices
    * User can delete items from cart, with live-updates supported re-rendering for a smooth experience
  * A new Blog Detail layout alternative
  * More static layouts for Portfolio and Promotional Section

### 4.17.0 - Released 24th September 2024

* Tailwind build method can now be overridden on the Page Template level, either by setting when you create a Page Template, or by using the `template_build_method` parameter (can be set to either "cli" or "preview"):

```liquid
{% raw %}
{% include 'modules/module_86/tailwind/head', template_build_method: 'cli', template_build_me optional_path_to_cli_css: '' %}
{% endraw %}
```

* New Preview build method for Tailwind. This is a replacement for the now deprecated JIT option, which should provide faster development times.&#x20;
  * Preview mode is designed to load CSS fallbacks so that any Flowbite blocks added to the site will be supported out-of-the-box, using Flowbite default variables.
  * It can be used alongside a CLI build. The CLI build will override any classes you've used, with branded versions of the variables you've set in your Tailwind Config file, while continuing to fallback to Flowbite defaults when brand new blocks are added.
* New Static Layouts for Flowbite:
  * Portfolio
  * Promotional Section

### 4.16.3 - Released 19th September

* Small UX and styling improvements to navigation and scrolling

### 4.15.2 - 4.15.3 - Hotfixes - Released 10th September 2024

### 4.15.1 - Released 5th August 2024

* Patch to fix Flowbite WebApp Edit Form layout not installing properly in "static" mode.&#x20;

### 4.15.0 - Released 3rd August 2024

* New Layout type- Category List Views - these work as code snippets which can be added almost anywhere and either loop over all categories or children of a category ID you pass in in settings.
  * SiteBuilder 4.15.0
    * 2 new Category List Layouts
  * Flowbite Pro Theme 1.9.0
    * 5 new Category List Layouts

### 4.14.0 - Released 17th July 2024

* New Flowbite Form Confirmation Layout which will automatically display submitted custom fields with headings.
  * Each field type will be displayed appropriately, e.g. files can be downloaded and images will be displayed.
* Page Templates and Flowbite Cookie Popup Layouts will include code for Google Tag Manager- ID will need adding manually in order to work.
* Cleaned up some old files no longer used
* Renamed some eCommerce layouts for clarity

### 4.11.1 - 4.11.4 - Released 17th June 2024 <a href="#id-4111-4114-released-17th-june-2024" id="id-4111-4114-released-17th-june-2024"></a>

* Patches to manually-managed setting on files created with SiteBuilder
* Changes to Tailwind setup folder structure - for easier setup

### 4.11.0 - Released 14th June 2024 <a href="#id-4110-released-14th-june-2024" id="id-4110-released-14th-june-2024"></a>

* Changelog coming soon. Suggest holding off on update until ready.

### 4.10.0 - Released 17th May 2024 <a href="#id-4100-released-17th-may-2024" id="id-4100-released-17th-may-2024"></a>

* Updated Layouts generally to support latest version of Flowbite v.2.3.0 and Tailwind CSS 3.4.3. To get the benefit of newer Flowbite JS, you will need to update the `<script>` tag in any SiteBuilder-built Page Templates. When testing the Site Templates, we didn't find many compatibility issues- the main one was a change in syntax for Flowbite Modal components. Please report any you find which can be fixed on our end.
* Updated the Sitegurus Tailwind Template with these newer versions of Flowbite and Tailwind CSS. [https://github.com/SiteGurus/Siteglide-Tailwind-Template](https://github.com/SiteGurus/Siteglide-Tailwind-Template) You can update your existing CLI setups using NPM
* Released eCommerce Layouts
  * Product List View
  * Product Detail View
  * Cart
  * Form Confirmation with embedded Order Detail
  * Orders List View (requires login)
* Form Layouts
  * New Form Layout with embedded Cart Layout, designed to be used with Checkout/ Quote type forms
    * Added better support for Stripe Form elements in dark mode
  * Added better Flowbite dark mode support for spinners on buttons
* standard Blog list view layout
  * Fix for author snippets links
  * Improved displaying user-feedback on filtering
* A new Flowbite eCommerce Site Template will follow shortly, demoing many of these new layouts.

### 4.9.5 - Released 22nd March 2024 <a href="#id-495-released-22nd-march-2024" id="id-495-released-22nd-march-2024"></a>

* Fix for addresses in form layouts

### 4.9.4 - Released 21st March 2024 <a href="#id-494-released-21st-march-2024" id="id-494-released-21st-march-2024"></a>

* Hotfix for bug in previous update

### 4.9.3 - Released 21st March 2024 <a href="#id-493-released-21st-march-2024" id="id-493-released-21st-march-2024"></a>

* Form Layouts
  * Fix for eCommerce-themed Form type Layouts asking which Module you wish to use, instead of which CMS Form.
  * Module Add and Edit Layouts have been upgraded to better support Custom Modules from the Marketplace. This will work alongside an upcoming Siteglide release

### 4.9.2 - Released 20th March 2024 <a href="#id-492-released-20th-march-2024" id="id-492-released-20th-march-2024"></a>

* Live Updates 1-4 hotfix - [changelog](https://www.sitegurus.io/documentation/sitebuilder/live\_updates/changelog)

#### 4.9.1 - Released 15th February 2024 <a href="#id-491-released-15th-february-2024" id="id-491-released-15th-february-2024"></a>

* Hotfix for form layouts not working with the minified version of JavaScript files. This issue would only have affected more recent installs.

#### 4.9.0 - Released 21st December 2023 <a href="#id-490-released-21st-december-2023" id="id-490-released-21st-december-2023"></a>

* Support for upcoming eCommerce features- including new version of [Live Updates 1.4](https://www.sitegurus.io/documentation/sitebuilder/live\_updates/changelog).

#### 4.8.12 + 4.8.13 - Released 11th December 2023 <a href="#id-4812-4813-released-11th-december-2023" id="id-4812-4813-released-11th-december-2023"></a>

* Support for upcoming eCommerce features

#### 4.8.10 + 4.8.11 - Released 4th October 2023 <a href="#id-4810-4811-released-4th-october-2023" id="id-4810-4811-released-4th-october-2023"></a>

* Fix for broken links in the SiteBuilder UI

#### 4.8.9 - Released 27th September 2023 <a href="#id-489-released-27th-september-2023" id="id-489-released-27th-september-2023"></a>

* Fix for JIT Tailwind script not loading correctly after 4.8.8.

#### 4.8.8 - Released 14th September 2023 <a href="#id-488-released-14th-september-2023" id="id-488-released-14th-september-2023"></a>

* Live Updates v1-3
  * New version of [Live Updates 1.3](https://www.sitegurus.io/documentation/sitebuilder/live\_updates/changelog). Existing layouts can be updated by manually changing the `<script>`. New layouts will use the new version.
* Performance
  * All SiteBuilder JS, including Live Updates, now has a minified version of the same file in the same folder. Simply replace `.js` with `.min.js` extensions for a performance boost. This will be applied to new installs of layouts going forwards. If you're experiencing unhandled JS errors and want to report a bug, you may find it helpful to switch back to the unminified version temporarily.
  * Performance boost to the SiteBuilder module UI

#### 4.8.7 - Released 9th September 2023 <a href="#id-487-released-9th-september-2023" id="id-487-released-9th-september-2023"></a>

* Forms
  * Datasources in forms used to only show a maximum of 20 options. A lower value may have increased performance, but also reduced the user's choices arbitrarily. Now that limit has been increased to 2000 by default on both dynamic and static form layouts. You can change the default on dynamic layouts by setting a `datasource_limit` parameter to a string value e.g. `'1000'` on the `form_layout_fields` include. On static layouts, the `per_page` parameter can be edited on the nested `<div data-gb-custom-block data-tag="include"></div>` tags inside the layout which fetch the datasource options.
* Cookie Popup Layouts
  * Fixed bug preventing some layouts from hiding scripts when cookies rejected. Remember changes will only apply to freshly installed layouts. If you need to fix an existing layout manually, replace: `<div data-gb-custom-block data-tag="if" data-0='all' data-1='all' data-2='all' data-3='all' data-4='all' data-5='all' data-6='all' data-7='all' data-8='all' data-9='all' data-10='all' data-11='all' data-12='all' data-13='all' data-14='all' data-15='all' data-16='all' data-17='all' data-18='all' data-19='all' data-20='all' data-21='all' data-22='all'></div>` with `<div data-gb-custom-block data-tag="if" data-0='sg-cookie-policy-settings' data-1='sg-cookie-policy-settings' data-2='sg-cookie-policy-settings' data-3='sg-cookie-policy-settings' data-4='] == ' data-5='] == ' data-6='] == '></div>`
* Live Updates
  * Added support for using a code\_snippet or content\_section as your layout. A new parameter of `include_id` has been added to the `live_updates_params_encode` include to store the ID of the `code_snippet` or `content_section`. See: [Defining a Live Update Layout](https://www.sitegurus.io/documentation/sitebuilder/live\_updates/guide\_-\_getting\_started#2-defining-a-layout-which-will-liveupdate-and-automatically-generating-a-public-api-key)

#### 4.8.6 - Released 9th August 2023 <a href="#id-486-released-9th-august-2023" id="id-486-released-9th-august-2023"></a>

* New version of [Live Updates 1.2](https://www.sitegurus.io/documentation/sitebuilder/live\_updates/changelog)

#### 4.8.5 - Released 3rd August 2023 <a href="#id-485-released-3rd-august-2023" id="id-485-released-3rd-august-2023"></a>

* Fixed bug in Page Template install in Themes with no cookie popup option
* Fixed bug in Live Updates error handling

#### 4.8.4 - Released 25th July <a href="#id-484-released-25th-july" id="id-484-released-25th-july"></a>

* Improved PageBuilder Options. You can now set custom pagination layouts in PageBuilder in the options drawer.
* Improvement to WebApp table layout so that if a category filter is added, it's possible to choose a parent category in a Liquid variable at the top of the wrapper. This means you can organise relevant categories in a folder and only show those.
* Improvement to Blog layouts using a grid where if few results, the cards would stretch to fill the space. Now they stay at the correct unstretched size.
* Blog, Events, FAQ and other list layouts replaced with upgraded Live Updates versions of themselves, for better user experience. When using new list layouts alongside a details page, set `use_adv_search: 'true'` on the list view's tag to instantly apply detail page filters when linking back. (See below)
* Fixed missing parameter `range_field` for live Updates API
* Live Updates API now has a new version of its JavaScript file, with added functionality. This will be included in many new SiteBuilder layouts by default, or you can optionally upgrade your existing layouts with the tag:

```liquid
{% raw %}
<script async src="{{'modules/module_86/js/v1-1/sitegurus_live_update_javascript_api.js' | asset_url }}"></script>
{% endraw %}
```

* Live Updates API now adds a click listener to text input fields. This helps to cover an edge-case where a cancel button is nested inside the text area to clear the field. Non-breaking change.
* New feature modifyHistory changes te URL to match fitlers without page reload - useful for shareable links and single-page applications
* New feature automatically launches a live-update on page load if any of the live-update form elemtns has a value.
* Improvement to error message when a Liquid error is detected in updated HTML.

#### 4.8.3 - Released 21st June <a href="#id-483-released-21st-june" id="id-483-released-21st-june"></a>

* Fixed a rare bug relating to module API page templates conflicting with site page templates.

#### 4.8.2 - Released 15th June <a href="#id-482-released-15th-june" id="id-482-released-15th-june"></a>

* Fix for live-updates issue where radio button element's value is read incorrectly when filtering.

#### 4.8.1 - Released 25th May <a href="#id-481-released-25th-may" id="id-481-released-25th-may"></a>

* Fix for issue from 4.7.2

#### 4.8.0 - Released 25th May <a href="#id-480-released-25th-may" id="id-480-released-25th-may"></a>

* Added layouts to Flowbite and Bootstrap Themes for:
  * Cookie Policy Popups
  * Cookie Policy Settings Pages
* These are examples of a brand new type of layout for SiteBuilder, as installing them creates a Siteglide code\_snippet with a unique ID. More [code\_snippet layouts are now possible for SiteBuilder developers](https://www.sitegurus.io/documentation/sitebuilder/developers\_-\_adding\_SiteBuilder\_content/adding\_layouts#code-snippets). Currently, these are not supported in PageBuilder.
* Page Template creation now gives you an option to install a cookie popup layout directly into your new Page Template. If chosen, this replaces the Google Analytics script which would normally be entered by default. The cookie popup layout contains the same Google Analytics script, but wraps it in logic which allows it to be toggled on and off by the end-user. Cookies settings page layouts are not designed to be entered in the Page Template and must be installed via the layouts tab instead.

***

#### 4.7.3 - Fix to previous release <a href="#id-473-fix-to-previous-release" id="id-473-fix-to-previous-release"></a>

#### 4.7.2 - Released 18th May 2023 <a href="#id-472-released-18th-may-2023" id="id-472-released-18th-may-2023"></a>

* Added new setting in settings tab for TinyMCE API key. This allows layouts to dynamically fetch key from one place.

#### 4.7.1 - Released 17th May 2023 <a href="#id-471-released-17th-may-2023" id="id-471-released-17th-may-2023"></a>

* Flowbite table webapp layout now uses left-align for its table headers.

#### 4.7.0 - Released 16th May 2023 <a href="#id-470-released-16th-may-2023" id="id-470-released-16th-may-2023"></a>

* Improvements to forms
  * All form components to use the `{{field_id}}` (plus any appropriate suffix) for their ID, instead of name (same for label for attributes). This should simplify any JS or CSS referencing it.
  * All required fields will have an asterisk " \*" added after their labels by default. This can be changed in components.
  * All inputs will be given data-attributes containing the text of their human-readable label `data-sg-validation-label` and the main field ID for their field `data-sg-validation-id` (note this may be different from the ID of the element if there are multiple form elements responsible for controlling a field, e.g. checkboxes). These can be useful when writing custom validation rules.
  * If the error message from Siteglide validation references a field by ID, we will change the error message to be more human-friendly. The default is a generic message asking the user to complete missing fields, but a commented out alternative allows you to print the human-readable name of the first missing field. Likewise, we've added a more human-friendly error message when a captcha fails. These messages can be edited in the form layout JS.
  * Improvements for Date, File and Image fields when marked as required.
  * Improvements for rich-text textarea type fields when marked as required.
  * Added minimum value to date fields so they do not add a date which is out of range of Siteglide's date field. Siteglide dates must be within the unix epoch.
  * Improved animation transition on form progress bars.

***

#### 4.6.5 - Released 11th May 2023 <a href="#id-465-released-11th-may-2023" id="id-465-released-11th-may-2023"></a>

* Improvement to Flowbite Login Form Modal Layout - Wider padding and more modern syntax to make it less prone to closing accidentally. This may still happen if the user clicks on the backdrop, but is less likely to happen when missing a click event aimed at an input.

#### 4.6.4 - Released 11th May 2023 <a href="#id-464-released-11th-may-2023" id="id-464-released-11th-may-2023"></a>

* Supporting the ability to more easily add a parameter to redirect the form to a custom URL. Set `custom_form_redirect` parameter on the top include `form` tag or the include `form_layout_fields` tag.
* Fixes for dark mode on some Flowbite Layouts

#### 4.6.3 - Released 27th April 2023 <a href="#id-463-released-27th-april-2023" id="id-463-released-27th-april-2023"></a>

* Hotfix for Rich Text fields not submitting correctly in forms

#### 4.6.2 - Released 27th April 2023 <a href="#id-462-released-27th-april-2023" id="id-462-released-27th-april-2023"></a>

* Fix for Flowbite Typography dark mode on Flowbite Layouts
* Improvements and fixes to Sitebuilder Forms:
  * Type date fields now show initial values correctly, in local timezone, the same as Siteglide Admin. They also have max-values which don't allow invalid unix timestamps and expiry date will default to the max timestamp.
  * Textarea fields are now passed `data-sg-rich-text` attribute if `rich_text` is selected in the Siteglide Admin
  * Textarea fields now have rich-text-editor support when rich-text is turned on. This feature is powered by TinyMCE and requires a free API key to be added to remove warning notice. View the [docs](https://www.tiny.cloud/docs/tinymce/6/cloud-quick-start/#add-your-api-key) to add your API key and modify the settings.
* Added experimental support for datasources on Flowbite Live-updates WebApp table layout. This outputs the names of data-sourced webapp items in the table-cell instead of IDs. In future, we'd like to optimise this for performance, for now, we recommend only using it on short lists.

#### 4.6.1 - Released 26th April 2023 <a href="#id-461-released-26th-april-2023" id="id-461-released-26th-april-2023"></a>

* Fix for SiteBuilder forms- datasource (single) fields in edit forms were not previously showing initial values correctly.

#### 4.6.0 - Released 25th April 2023 <a href="#id-460-released-25th-april-2023" id="id-460-released-25th-april-2023"></a>

* Launching the JS Live Update API - Making it quick and easy to live-update server-side code on the client side when users interact with it and its state changes.
* New Flowbite Page Templates now have the beta feature option to select an alternative Template structure suitable for Portals and Applications. This supports a Flowbite sidebar layout.
* Improvements and Fixes for some Form Layouts
  * Added a variant of the Flowbite multi-part form with full-width fields for use in smaller form sections.
  * Flowbite multi-part forms now fill the container height, making it more convenient to add them inside a grid.
  * Fixes for edit email & password functionality on Flowbite forms (Bootstrap Theme did not have the bug)

***

#### 4.5.6 - Released 31st March 2023 <a href="#id-456-released-31st-march-2023" id="id-456-released-31st-march-2023"></a>

* Fixes for some Slider Layouts
  * fixes layouts which were either missing the Liquid to load the JS, or using an older, less efficient, version.
  * fixes for layouts with broken image alt fields.
* Fixes for compatible Themes, such as Flowbite Pro.
  * Fixed bug when installing a detail layout from a compatible theme on PageBuilder, where that layout would be given a list view tag.
  * Fixed bug in WebApp Layout field mapping where layouts from compatible Themes were given the wrong field slots.
  * Fixed bug viewing layouts from compatible themes on Layouts tab when the same ID was used in different Theme namespaces.

#### 4.5.0 - Released 16th March 2023 <a href="#id-450-released-16th-march-2023" id="id-450-released-16th-march-2023"></a>

* Added support for WebApp Layouts. WebApp Layouts allow agencies to map custom fields from a WebApp to slots in the Layout, so Generalised Layouts can suit a range of specific use-cases.
* UI Improvements including Validation and Accessibility
* Added a range of WebApp Layouts to the Flowbite Library.
* More WebApp Layouts coming soon.

***

#### 4.4.0 - Released 26th January 2023 <a href="#id-440-released-26th-january-2023" id="id-440-released-26th-january-2023"></a>

* Support for Siteglide Slider Module
* New optional JS script for layouts implementing a slider effect
* Added Slider layouts to Flowbite and Bootstrap Themes
* Fix for some layout options in Page Builder
* Improvements to UI

***

#### 4.3.0 - Released 6th January 2023 <a href="#id-430-released-6th-january-2023" id="id-430-released-6th-january-2023"></a>

* Support for WebApp and Module item add, edit and delete form layouts.
* Support for WebApp and Module item add forms to PageBuilder.
* Updated documentation to explain the new reliable way to change the order of custom fields in dynamic form layouts.
* Changed default order for system fields in forms to be negative. This will affect existing sites, so be prepared to review these when updating the module:
  * name: -40
  * email: -30
  * password: -20
  * Categories: -10\
    It is possible to order custom fields so that they fall before, after or between these system fields.
* PageBuilder UI updated to guide the user to select Page Template and name before the Theme is locked-in.
* Form Layout progress bars only display while form is submitting, not before.
* Improvements to Form Layout Image and File fields.
* Fixes to SiteBuilder UI

***

#### 4.2.1 - released 9th December 2022 <a href="#id-421-released-9th-december-2022" id="id-421-released-9th-december-2022"></a>

* Changed Home tab video

#### 4.2.0 - released 9th December 2022 <a href="#id-420-released-9th-december-2022" id="id-420-released-9th-december-2022"></a>

* Added new home tab to Module UI

***

#### 4.1.3 - released 7th December 2022 <a href="#id-413-released-7th-december-2022" id="id-413-released-7th-december-2022"></a>

* Fix for some issues in the settings page

#### 4.1.2 - released 30th November 2022 <a href="#id-412-released-30th-november-2022" id="id-412-released-30th-november-2022"></a>

* Further Static Layouts Fixes

#### 4.1.1 - released 30th November 2022 <a href="#id-411-released-30th-november-2022" id="id-411-released-30th-november-2022"></a>

* Fix for Static Layouts from compatible Themes e.g. Flowbite Pro, so that the Theme does not need to be installed on a Page Template, only installed to the Site, before the Static Layouts appear.

#### 4.1.0 <a href="#id-410" id="id-410"></a>

* Adds tips when a user adds a Module Layout in Page Builder, or when a Module Layout is installed.
* Links to Siteglide Admin from the UI now open in the same tab to take advantage of faster loading speeds.
* Multiple UI styling and responsiveness fixes

***

#### 4.0.4 <a href="#id-404" id="id-404"></a>

* Form field labels on Static Layouts now support apostrophe characters.

#### 4.0.2 <a href="#id-402" id="id-402"></a>

* Improves reliability of installs of layouts from compatible Themes.

#### 4.0.1 <a href="#id-401" id="id-401"></a>

* Fixes install bug
* Reduces Module install time

#### 4.0.0 <a href="#id-400" id="id-400"></a>

* Adds support for agencies to add SiteBuilder content through creating modules in the Siteglide Marketplace. These modules can be of two types, Themes which add entirely new Themes to SiteBuilder, or can extend existing compatible Themes. Or functional modules which add new content to Siteglide and can include SiteBuilder compatible layouts to extend any existing Theme. Read more in the documentation.
* New module UI which aims to deliver a clearer starting point for new users and better defaults for more experienced users.
* hcaptcha support for forms. This allows you to use Siteglide's recommended spam protection method.
* Remove unwanted PageBuilder sections
* Liquid tag recommendations when creating layouts
* More Modules and Sub-modules supported

***

#### 3.2.3 - released 13th October 2022 <a href="#id-323-released-13th-october-2022" id="id-323-released-13th-october-2022"></a>

* Bug fix for Form Layouts to support HTML entities like ' in form config field options e.g. in checkboxes.

#### 3.2.2 - released 22nd September 2022 <a href="#id-322-released-22nd-september-2022" id="id-322-released-22nd-september-2022"></a>

* PageBuilder Safari bugfixes

#### 3.2.1 - released 21st September 2022 <a href="#id-321-released-21st-september-2022" id="id-321-released-21st-september-2022"></a>

* PageBuilder UI design Improvements

#### 3.2.0 - released 21st September 2022 <a href="#id-320-released-21st-september-2022" id="id-320-released-21st-september-2022"></a>

* Released PageBuilder, a brand new user-interface for quickly building a page from scratch using SiteBuilder content. Access this by clicking a library and scrolling down to PageBuilder.
  * Search for and apply an existing Page Template
  * Add as many sections as you like and choose whether to add static or dynamic layouts
  * Visually preview and choose layouts from the current SiteBuilder library.
  * Use the UI to select module specific settings to automatically add to the Liquid tags when we build the page

***

#### 3.1.14 - released 14th September 2022 <a href="#id-3114-released-14th-september-2022" id="id-3114-released-14th-september-2022"></a>

* Support for form fields for changing email and passwords.

#### 3.1.13 - released 7th September 2022 <a href="#id-3113-released-7th-september-2022" id="id-3113-released-7th-september-2022"></a>

* Performance upgrade when adding duplicate layouts to the same PageBuilder Page
* Added support for adding Detail Layouts. Tip: use item\_ids to select a specific item's detail page
* Added Changelog to documentation

#### 3.1.0 - released 2nd August 2022 <a href="#id-310-released-2nd-august-2022" id="id-310-released-2nd-august-2022"></a>

* Added new contextual docs links
* Improved Page Template Creation wizard to add Header/ Footer options

***

#### 3.0 - released 12th July 2022 <a href="#id-30-released-12th-july-2022" id="id-30-released-12th-july-2022"></a>

* Introducing the Flowbite Library
