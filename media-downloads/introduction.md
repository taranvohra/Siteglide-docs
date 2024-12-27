---
title: Media Downloads
slug: VKOt-
createdAt: 2021-02-16T11:09:51.000Z
updatedAt: 2023-04-11T09:57:11.000Z
---

The Media Downloads Module allows you to upload files securely. You have control over who accesses the File, and how long links work for.

# Introduction

The Media Downloads Module is similar to File Manager, but is designed to handle files which need to be handled more securely. Some examples might include:

*   Files which exist behind a Secure Zone

*   eBooks and other files you may need a Subscription to access

In it's first release, the Module allows you to:

*   Upload Files Securely - It is not possible for internet users to "guess" the link to your files and download them.

*   Generate secure links on the Front-End; each link will only be valid for a short amount of time after reloading the Page. This allows you to control who has access to the link, and how long they will have access for.&#x20;

# Outputting List Views on the Front-End

Like with other Modules, you will use a Liquid Tag to output a list of Module Items on a Page, Page Template, Email or Partial Liquid File of your choice.

```liquid
{% raw %}
{%- include 'module'
    id: '17'
    layout: 'default'
    per_page: '20'
    show_pagination: 'true'
    sort_type: 'properties.name'
    sort_order: 'asc' 
-%}
{% endraw %}
```

 You can use the following parameters:

*   `ID` - This must be set to `17` as this refers to the ID of the Media Downloads Module

*   `layout` - The Layout Folder containing the List Layout

*   `per_page` - How many Items should be outputted on each Page. If more Items are available than this, Pagination controls will display.

*   `show_pagination` - if set to `'true'` , pagination controls will display in the default position when more than one Page of results is available.

*   `sort_type` - The field you'd like to sort by e.g. "properties.name", or "created\_at" 

*   `sort_order` - Choose `asc` for ascending values or `desc` for descending 

*   `category_ids` - Pass in a string of comma-separated IDs of Categories to filter the List so only Items assigned to those Categories can be displayed.

*   `item_ids` - Control exactly which Items can be displayed by passing in a string of comma-separated IDs. You can find the Items' IDs in the Admin. 

*   `expiry`  - The number of seconds that the link is valid for after the page has finished loading.  Default is 600 (10 minutes). Note this is different from&#x20;

*   `expiry_date`, see Available Fields.

# Media Downloads Layouts

## Creating a Layout File

Layouts can be created at the following path: `layouts/modules/module_17/my_layout_name/ `

<!-- ![](https://downloads.intercomcdn.com/i/o/201119735/c417f312d2c0f4cde259a3ef/image.png) -->

## Developing a List Layout

You'll need to create a `list` folder in your layout folder and fill it with the following files:

*   wrapper.liquid

*   item.liquid

Your `wrapper.liquid` file should contain the following Liquid which determines where the list of Items will go:

```liquid
{% raw %}
{%- include 'modules/siteglide_media_downloads/get/get_items'
    item_layout: 'item' 
-%}
{% endraw %}
```

## Available Fields

In your `item.liquid` file, you can use the following dynamic fields:

*   `{{this.id}}` - The Item's unique ID

*   `{{this.name}}` - The Item's name

*   `{{this.create_date}}` - The date this Item was created. Use Liquid Date Filters to format it.

*   `{{this.last_edit_date}}` - The date this Item was last edited. Use Liquid Date Filters to format it. 

*   `{{this.file_name}}` - The Module automatically works out File Name from the File itself.

*   `{{this.file_type}}` - The Module automatically works out File Type by its extension.

*   `{{this.url}}` - This will output the temporary secure link. See more details in the section below.

*   `{{this.weighting}}` - Optional Field used in sorting

*   `{{this.release_date}}` - The date this Item was released. Use Liquid Date Filters to format it. 

*   `{{this.expiry_date}}` - The date this Item will expire. Use Liquid Date Filters to format it. Note- this is different from expiry see Liquid parameters. 

*   `{{this.category_array}}` - An array of categories that the Item is assigned to.

*   `{{this.Description}}` - A description of the Download

*   `{{this.size_in_kb}}` - The file size of the download in Kilobytes

*   `{{this.size_in_mb}}` - The file size of the download in Megabytes-&#x20;

*   `{{this.size_in_gb}}` - The file size of the download in Gigabytes

# How the Media Download Links Work

When you output a link on the Front End, it contains security parameters that will be different on every Page load. The purpose of these is to tie a security key with a time-limited window to access the file.  The `expiry` parameter will be used to denote how long the link is valid for after the page has been loaded.  For example, if a user loads the page and then clicks the link 20 minutes later, the download link will already be invalid as it will be over the 10 minute default window.  At this point the user will have to reload the page to generate a new valid link.

Despite this, you can use the link exactly like a normal URL to an asset, except that there is no need to use `asset_url` because the link goes directly to the CDN. 

# Using Media Downloads with Secure Zones

A secure link is only as secure as the Page you output it on.&#x20;
By outputting your Layout on [a Page which is protected by a Secure Zone](/crm/quickstart-crm.md#3-securing-pages), you have full control over who will have access to your links. 

You could also use [Categories](/cms/categories/quickstart-categories.md) to manage which Media Downloads are available on each Secure Zone. A Category could be created to correspond to each Secure Zone and on the Secure Page, you could output a List of Media Download Items assigned to that Category.   
