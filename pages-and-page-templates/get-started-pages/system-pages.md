# ℹ️ System Pages

System Pages work similar to other pages- but they are stored under Site Manager as they are most likely to be looked at by a Developer.

### Available System Pages

You can currently edit the content of the following system pages:

* **404 page** - Users are redirected to this page if they try to visit a page which does not exist.
* **401 page** - Users are redirected here if they try to access a page within a Secure Zone they don't have access to. (When editing within CLI, both **marketplace**_**builder/views/pages/system**_**pages/401.liquid** and **marketplace\_builder/views/partials/401.liquid** will need to be edited. These 2 files are used in different places in the Secure Zone system.)
* **Recover Password** - This page contains a button which will send the User a recover-password email.
* **Reset Password** - If the User clicks a link in a recover-password email, they will be sent to this page with a token included in the request. If the token is valid, they will be allowed to choose a new password, otherwise, an error message will show.
* **Robots** - This allows you to create a "robots.txt" file which can be used to give recommendations to search engines about which pages they should avoid crawling. This is a special kind of liquid page which will render to .txt format before the server sends it to the browser.
* [XML Sitemap](/site-manager2/system-pages/automatic-sitemap-generation.md) - This allows you to give search engines a helpful map which helps them find all the pages you would like to be indexed. This is a special kind of liquid page which will render to .xml format before the server sends it to the browser.

You can create additional system pages via the CLI.

### Learn more

You can learn more about writing an XML sitemap here: [https://support.google.com/webmasters/answer/183668?hl=en](https://support.google.com/webmasters/answer/183668?hl=en)

You can learn more about writing a robots.txt file here: [https://support.google.com/webmasters/answer/7424835?hl=en](https://support.google.com/webmasters/answer/7424835?hl=en)

The advantage of a Siteglide System Page is that you can write liquid to make the page dynamic and easier to maintain. Create a trial site and install the Starter Kit to see a working example of a Dynamic Sitemap.
