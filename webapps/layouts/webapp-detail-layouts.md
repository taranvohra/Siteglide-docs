# ℹ️ WebApp Detail Layouts

When enabled, WebApps have automatically generated Detail Pages, which use your chosen Detail Layout to display each WebApp Item's content. Users can make new WebApp items and the page will automatically be created for them.

## Syntax

To output a WebApp list within a detail layout you must include the following parameter: `type: 'list'`

<!-- See more about nesting dynamic content inside your WebApp Layouts in the [Nested Content and Datasources](https://help.siteglide.com/article/201-datasources-and-nested-dynamic-content-introduction) section of the documentation. See more about list output parameters on the [List Layouts](/webapps/layouts/webapp-list-layout.md) doc. -->

## Folder Structure

When you create a WebApp, default files are automatically created for you. WebApp list layouts are stored in the following folder structure, which you can view via Code Editor: `layouts/webapps/webapp_ID (My WebApp)/`

Within this folder you will find the following:

* `detail/` - the detail layouts of the WebApp, visible on the url of the item
  * `default.liquid` - the default detail layout

## Editing Layouts

To create a custom layout file, right click on the detail folder. Alternatively, you can edit the default file. All layout files must use the `.liquid` file extension, for example `mylayout.liquid`. You can select which detail layout a WebApp from a dropdown on the edit WebApp page.

While editing the layout of the WebApp using Code Editor, you can output any field using the dropdown along the top of the editor.
