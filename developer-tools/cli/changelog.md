# 🛳️ CLI Changelog

### 1.10.1 - 19th February 2025

* Add support for new London server stack

***

### 1.9.8 - 20th August 2024

* Add support for Node LTS (v20.16.0)

***

### 1.9.6 - 3rd August 2022

* Allow `.md` and `.htm` file extensions

***

### 1.9.5 - 22nd March 2022

**Bug Fixes**

Logs

* Fix a crash on logs when a specific deprecation warning is shown

***

### 1.9.4 - 15th March 2022

**Bug Fixes**

Export/Pull

* Extend wait time to 2 minutes to lessen "Pull Failed" issue

***

### 1.9.3 - 25th January 2022

**Bug Fixes**

GraphiQL

* Fix missing error/warning linting in editor

***

### 1.9.2 - 25th January 2022

**Features**

Sync

* Show which file is failing if a sync error occurs

**Misc**

* Update dependencies

***

### 1.9.1 - 21st January 2022

**Bug Fixes**

Pull

* Improve pull support on Windows for page redirects with special characters

**Misc**

* Improve log loading performance
* Remove unused code
* Update dependencies and remove unused dependencies

***

### 1.9.0 - 23rd September 2021

**Features**

Pull

* You can now pull modules that are placed in the `modules` folder alongside `marketplace_builder` To do this pass in the name of the module to the pull command, for example `siteglide-cli pull production --module my_great_module`

Modules

* A new command that will display a list of modules installed on the site. These names can then be used in the pull command to download the content of those modules. Example: `siteglide-cli modules production`

**Bug Fixes**

Migrate

* Ignore `BannerProcess.aspx` pages when migration from Adobe BC

***

### 1.8.19 - 20th September 2021

**Bug Fixes**

Sync

* Fix Studio sass not compiling when either `custom.scss` or `custom_variables.scss` was synced

***

### 1.8.18 - 10th September 2021

**Bug Fixes**

Migrate

* Fix CSS not converting to asset urls for Muse sites
* Fix muse `data-hidpi-src` not migrating correctly

***

### 1.8.17 - 2nd September 2021

**Bug Fixes**

Migrate

* Ignore converting BC search forms when migrating

***

### 1.8.16 - 31st August 2021

**Bug Fixes**

Migrate

* Fix migrate command failing to run

***

### 1.8.15 - 27th August 2021

**Bug Fixes**

Deploy

* Fix a sites homepage not updating during a deploy

Misc

* Improved messaging of some logs

***

### 1.8.14 - 17th June 2021

**Features**

Export

* Allow export of .heic images

Sync

* Add the following file types to the sync watcher:
  * heic
  * key
  * mov
  * mp3
  * numbers
  * ttf
  * pages
  * pptx

***

### 1.8.13 - 15th June 2021

**Features**

Migrate

* The size of your assets and codebase will now be displayed when the migrate command has finished

**Fixes**

Migrate

* Ignore OrderRetrieve pages from Business Catalyst

***

### 1.8.12 - 3rd June 2021

\*\*Fixes \*\*Deploy

* Block deploy and show an error if assets are over 5GB

Migrate

* Improve compatibility with images using Fill Proportional within Business Catalyst websites

***

### 1.8.11 - 29th April 2021

**Fixes** Migrate

* Improved compatibility with Siteglide forms and CLI Migrated pages

***

### 1.8.10 - 21st April 2021

**Fixes** Migrate

* Fixed a bug where migrate would fail if a site had no assets
* Fixed a bug where migrate would fail if an asset did not have a valid link/href/src

Misc

* Improved error messages throughout

***

### 1.8.9 - 13th April 2021

**Features** Migrate

* Full Adobe Muse Support: When migrating Adobe Muse sites, CLI migrate will not correctly download all assets and configuration files. Please append the flag --muse to your migrate command when migrating a Muse site.

***

### 1.8.8 - 9th April 2021

**Fixes** Migrate

* Add support for finding images within a `data-orig-src` attribute. These are commonly used with Muse websites
* Improved the "Something went wrong" error during form conversionFixes

***

### 1.8.7 - 30th March 2021

**Fixes** Migrate

* Fix ModuleStyleSheet.css missing from migrated Business Catalyst sites

***

### 1.8.6 - 29th March 2021

**Fixes** Migrate

* Fix migrate command not running

GUI

* Fix open command not working
* Fix open command opening browser before GraphiQL was ready

**Misc** GraphQL

* Removed the deprecated graphql command, please use gui instead

GraphQL - Removed the deprecated graphql command, please use \`gui\` instead

***

### 1.8.5 - 23rd March 2021

**Fixes**

Deploy

* Fix for deploying with images reporting an internal server error

***

### 1.8.4 - 23rd March 2021

**Fixes**

Deploy

* Fix deploy potentially not working correctly

Logs

* Fix filter flag potentially not working correctly

***

### 1.8.3 - 22nd March 2021

**Fixes** Sync

* Improvement to fix for syncing assets after sync had been running for more than 1 hour
* Improved sync messaging

***

### 1.8.2 - 21st March 2021

**Fixes** Add

* The Add command will now detect if you are trying to run the it within your computers home folder and stop you continuing

Sync

* On macOS, sync will no longer report errors about `.DS_Store` files
* Fixed an issue trying to sync assets after sync had been running for more than 1 hour General
* Improved error messaging

***

### 1.8.1 - 12th March 2021

**Fixes**

Migrate

* Improve image compression process
* Fix deploy too large error when image compression fails

***

### 1.8.0 - 11th March 2021

**Features**

List

* A new command of `siteglide-cli list` which will show an output the current environments setup for the site. These will display in the format of `- [environment name] [url]`

Migrate

* New flag of `-m` or `--max-recursive-depth` that will allow you to define how many html links deep the scraper should follow. As an example: - Your homepage links to page /B - Page /B links to page /C Setting `-m 1` will only download the homepage and page /B. Page /C will not be downloaded as it is more than 1 link deep away from the entry point of the migration. Any assets of the pages are downloaded as normal.
* New flag of `-i` or `--ignore` to ignore certain URLs. This is a string that gets passed into a `if(currentURL.includes(ignore))` function. For example if you do not want your blog to be migrated and the URL of your blog posts are `site.com/post/post-name` then you can pass in `/post/` for them to be ignored. These can be stacked with multiple ignores, for example to ignore both your about and contact page you would do `siteglide-cli migrate <env> --url <url> -i /about -i /contact.`

**Bug Fixes**

Migrate

* Fix migrate not completing on Windows due to invalid characters in folder paths and file names

Global

* Fixed the progress spinner icon missing in certain environments

***

### 1.7.7 - 17th February 2021

**Features**

Migrate

* Images within a `data-src` element are now found, migrated and the URL converted. For example the following image: `<img data-src="/img/image.jpg" />` would be correctly migrated to: `<img data-src="{{ 'img/image.jpg' | asset_url}}" />`

**Bug Fixes**

Sync

* Assets with an uppercase file extension can now be synced correctly

Migrate

* Improved support for Adobe Muse sites
* Asset file name casing is preserved instead of being automatically converted to lowercase

**Misc**

* Show Changelog in update message
* Updated minimum NodeJS version to 12

***

### 1.7.6 - 12th February 2021

**Bug Fixes**

Sync

* Fix syncing assets

Deploy

* Fix deploying assets

General

* Fix incorrect message within update prompt

***

### 1.7.5 - 8th February 2021

**Bug Fixes**

Sync

* Temporarily revert to the non-direct to S3 version

***

### 1.7.4 - 13th January 2021

**Features**

Sync

* Syncing direct to S3 has now become the default. This removed the `-d` flag as it is no longer needed

***

### 1.7.3 - 27th November 2020

**Features**

Sync

* New flag of -l on sync for live reload functionality. When you save an item within your IDE, your browser will automatically reload to show you the changes. Please make sure you have the relevant [browser extension](https://http/livereload.com/extensions/) installed for this to work

Export

* New flag of -a for asset export only. This will export code based assets within the sites `/assets` folder, but not the sites codebase (pages, headers, footers etc). You can mix this with `-w` to download only assets and include files like images, video etc

**Bug Fixes**

Deploy

* Fixed a misleading error message if a deploy failed with a 5xx error

***

### 1.7.2 - 18th November 2020

**Bug Fixes**

Migrate

* Fixed a bug that caused some Javascript files to have the contents \`undefined\` after being migrated

***

### 1.7.1 - 11th November 2020

**Features**

Pull

* A new flag for ignoring assets that Pull would usually download such as JS, CSS and JSON files. The default is that Pull will download developer assets, but the new `-i` flag will ignore that folder completely. This is useful if you want to pull the updates to pages, but know that no developer files such as CSS or JS have changed

***

### 1.7.0 - 6th November 2020

**Features**

Liquid Evaluator - Alongside our GraphiQL editor, we now have a new Liquid Evaluator tool. This will let you quickly test Liquid from the CLI, without having to create and save a page in Siteglide Admin. To use this new tool, we have moved it and GraphiQL to `siteglide-cli gui <env>` command. The `siteglide-cli graphql <env>` command will continue to work, but is now deprecated and will be removed in a future update

Sync

* Sync now watches for and syncs .map files which are commonly used alongside minified CSS or JS files.

Export

* Export has a new optional flag of `--csv`, this will export the data files as a zip of multiple CSV files instead of JSON.

Migrate:

* Migrate will now no longer automatically deploy the site when it has finished. This gives you time to remove and folders/pages that you may not want to be migrated. You can then use the `siteglide-cli deploy <env> -w` command as normal to deploy the site. You can use automatic deploy within a migration by including the `-a` flag

**Bug Fixes**

Deploy

* Fixed an issue where the homepage would not update properly when the site is deployed

Pull

* Pull will now automatically stop and exit if it fails

Migrate

* Fixed an issue where migrate would not run under certain environments
* Fixed an issue where after a migration the sites homepage would not save correctly in Siteglide Admin

***

### 1.6.10 - 22nd September 2020

**Bug Fixes**

Fixed a bug when running the add command with sites on the Sydney Datacenter

***

### 1.6.9 - 22nd September 2020

**Bug Fixes**

Fixed a bug where the add command would not correctly write the configuration file to disk. In previous versions this would case a “permission or site locked” error. To fix any sites with this issue, simply update and then re-run the add command for that site.

***

### 1.6.8 - 18th September 2020

**Features**

Pull now also downloads the following file types:

* `Less`
* `txt`
* `html`
* `svg`
* `map`
* `json`
* `htm`

**Bug Fixes**

General

* Improved logging throughout if a URL is invalid
* CLI will let you know of an update straight away, not after you have finished running your command

Migrate:

* Ignore Literature retrieve pages for Business Catalyst Sites

***

### 1.6.7 - 7th August 2020

**Bug Fixes**

General

* Fix instructions within update notifier

***

### 1.6.6 - 6th August 2020

**Bug Fixes**

Pull/Export

* Fix warnings related to modules folder for some instances

***

### 1.6.5 - 16th July 2020

**Bug Fixes**

Migrate

* Fix “Last edited” date in Admin for pages that have been migrated via CLI
* Improve performance by updating the core page conversion library
* Fixed incorrect download of some Business Catalyst pages

***

### 1.6.4 - 29th June 2020

**Bug Fixes**

Migrate

* Allow `.aspx` pages, fixes pagination within Business Catalyst WebApps
* Slow down the concurrency of downloads to improve stability
* Fix “type error” log that sometimes appeared
* Added a user agent to help with any potential site blocks
* Fixed "Undefined error" that sometimes appeared

Deploy

* Fixed error logging when a deploy fails because of invalid syntax

**Misc**

GraphQL

* Update dependencies

***

### 1.6.3 - 22nd June 2020

**Features**

Pull/Export/Sync/Deploy

* Support for Modules folder

**Bug Fixes**

Migrate

* Fix migrated forms not working correctly

***

### 1.6.2 - 15th June 2020

**Bug Fixes**

Migrate

* Fixed an out of memory error when trying to migrate large sites

Deploy

* Improved error messaging if the codebase of a site is larger than the allowed limit

***

### 1.6.1 - 4th June 2020

**Features**

Migrate

* Add a certification command to migration

Help

* The `--help` flag on all commands will now show the correct usage and a brief description of the command

**Bug Fixes**

Migrate

* While downloading a site, the CLI will now ignore any files that return a response header outside of the `2xx` range.
* Links to asset files that had the word assets within the URL will now be linked correctly
* Home page will be set visually within Siteglide Admin
* Fix form detection/conversion for certain sites
* Improved logging during migration
* Upgraded core packages for image compression

***

### 1.6.0 - 27th May 2020

**Features**

Migrate

* A brand new tool to migrate your existing websites from anywhere on the web. After adding your instance simply run `siteglide-cli migrate <env> --url <existing site>`. For more information see [here](https://developers.siteglide.com/introducing-siteglide-cli#migrate)

Deploy

* Deploy to S3: When deploying assets using the `-w` flag, assets will now get directly sent to S3, improving the performance of the deploy command. This also means that your assets can be up to 5gb in size, up from the existing 50mb limit.

**Bug Fixes**

Sync

* The “Enabled Sync” message has been updated to be clearer

Pull

* Fixed a warning related to modules that sometimes was shown
* Improved speed and reliability of assets

Deploy

* The deploying logs have been updated to be clearer

**Misc**

* Support for upcoming version of NodeJS

***

### 1.5.3 - 13th May 2020

**Features**

Sync

* Supports syncing of video files with extensions of `.mp4`, `.ogg` and `.webm`

**Bug Fixes**

Sync

* Improve error messaging for files that are not allowed

***

### 1.5.2 - 9th May 2020

**Misc**

* Support for upcoming v14 of NodeJS

***

### 1.5.1 - 23rd April 2020

**Bug Fixes**

Pull

* Fix certain files not pulling correctly

Export

* Fix certain files not exporting correctly
* Improve error messaging

***

### 1.5.0 - 22nd April 2020

**Features**

GraphiQL

* Add “Explorer”! This new functionality will allow you to explore and build your Graph Queries using a simple dropdown and checkbox method
* Add an `--open` (shorthand: `-o`) flag that will automatically open a window to the GraphiQL editor in your default web browser

Sync

* Sync delete: If you have sync running and delete a file locally on your computer, it will also remove that file from your website.
* Sync Direct to S3: Add an optional flag of `--direct-assets-upload` (shorthand `-d`) that syncs asset files directly from your machine to your sites Asset URL which improves speed of syncing. This will become default in the future

Export

* Remove the limit when downloading assets via export `--with-assets`

Logs

* You can now filter the type of logs you would like to see with the flag `--filter` (shorthand: `-f`). This is useful if you would only like to see error message from your liquid logs
* More context data will now log under each line showing information such as the path the error occurred on, the users email address if they were logged in and the Liquid partial the error originated from.
* Add a `--quiet` (shorthand: `-q`) flag which will suppress the above extra context data

**Bug Fixes**

Sync

* When using a pre-processor (e.g. Sass), there were cases where the CLI would sync the outputted CSS file before it had finished being compiled, resulting in an empty CSS file on your site. The Sync command will now wait for the compiled file to finish being written to your local disk before attempting to sync it.

Pull/Export

* Pull/Export: Improved downloading of code files to improve reliability and also speed
* Export: Allow shorthand flag of `-w` that acts the same as `--with-assets`

Init

* Improved CLI Init download method

***

### 1.4.1 - 26th March 2020

**Bug Fixes**

* Export - Excludes some automatically generated Siteglide files from export

***

### 1.4.0 - 25th March 2020

**Features**

* Export - A new optional flag of `--with-assets` that will allow export to download non-developer assets (such as: pdfs, images, videos etc). Note: This is currently limited to sites with less than 1,000 total assets. A future update will remove this limit

***

### 1.3.0 - 4th February 2020

**Features**

* Deploy - If you have made a lot of changes in your codebase, then you can use deploy to re-send all files to your site at once.
* Export - Export is very similar to Pull, but it will also grab all data.

***

### 1.2.2 - 15th November 2019

**Features**

* Pull will find and download and Sass (`.scss`, `.sass`) and LESS (`.less`) files

***

### 1.2.1 - 2nd October 2019

**Bug Fixes**

* Fix a bug that caused unknown command error on new installs of CLI.

***

### 1.2.0 - 10th September 2019

**Features**

* GraphiQL support! Now with the `siteglide-cli graphql <env>` command
* Logs support! Now with the `siteglide-cli logs <env>` command
* Version command has been moved to -v and not -V to better align with other tools

**Bug Fixes**

* Better error handling when no API Key has been generated in Siteglide Admin Portal (instead of just silently failing)

**Misc**

* Minimum version of NodeJS 10 now (up from NodeJS 8)

***

### 1.1.2 - 16th July 2019

**Misc**

* Update dependencies

***

### 1.1.1 - 11th July 2019

**Features**

* Error reporting within sync command for incorrect liquid
* Allow syncing of zip files

**Misc**

* Up to 4x increase in syncing speed

***

### 1.0.0 - 22nd May 2019

* Initial release
