---
title: Accessing Assets
slug: cvse-
createdAt: 2021-02-17T16:38:54.000Z
updatedAt: 2023-03-03T08:09:58.000Z
---

# 🔹 Linking to Assets Explained

Find out how to use the asset\_url filter to generate a path to your assets and understand the benefits of hosting assets on our CDN.

## Introduction

Assets are stored directly on an Amazon Web Services (AWS) server, separate to the website you are building on. They can be accessed using a Content Delivery Network (CDN) from your website.

## Benefits

The use of this method offers automatic Caching control, which decreases the likelihood that someone views your website with anything other than the most up-to-date versions of your files. The CDN also reduces page load times, as the assets are not stored on your site, but instead are distributed to over 100 edge locations around the world.

## CDN Asset URLs for the Best Performance

If you have uploaded an image to the images folder using File Manager, it will have a file path like this in the database: `images/SG-Logo-White.svg`

You would add the following liquid to your page, so that the server automatically appends the CDN URL: `{{ 'images/SG-Logo-White.svg' | asset_url }}`

You will see that the asset will render on the page with a similar path to this: `https://uploads.prod01.oregon.platform-os.com/instances/283/assets/images/SG-Logo-White.svg?updated=1549914206`

Each site has a unique CDN path, you can find out what yours is by rendering an image on the page and inspecting on it. `?updated=` is a parameter automatically included that time stamps your files, helping with cache control.

## Relative Asset URLs - Good Performance and convenient but may have caching issues for regularly updated assets

Using ../ automatically appends the URL to your asset within CSS files:

`background-image: url('../images/SG-Logo-White.svg');`

`../` is relative to the location of your stylesheet which will already be inside the CDN. This is especially useful for background images. You can look up CSS relative paths online for more information.

Note that this can have drawbacks with assets which are regularly updated, as you may pull in a cached version of the image. Using `asset_url` instead prevents this as it always appends the URL with a timestamp, busting the cache and getting the most recent version.&#x20;

## Vanity Asset URLs - Slower Performance, but sometimes a Client Requirement

In some cases you may wish to hide the AWS CDN `(https://uploads.prod01.oregon.platform-os.com)` and only refer to the vanity domain of the site (https://www.mydomain.com). To dynamically achieve this, you can use the liquid parameter `asset_path` rather than `asset_url` when calling an asset to a page. Any of the above examples are also applicable with this method.

`{{ 'images/SG-Logo-White.svg' | asset_path }}`

You will see that the asset will render on the page with your vanity domain in it's path, similar to this: `https://www.mydomain.com/assets/images/SG-Logo-White.svg?updated=1549914206`
