# 🔹 About Assets

### What is an Asset?

A website asset normally refers to a file or resource used by a website which will be used multiple times by the browser across the website. Some examples of files we normally refer to as assets would be:

* Stylesheets
  * .css
* Scripts
  * .js
* Images
  * .jpg
  * .png
  * .webp
* Videos
  * .mp4
* Sounds
  * .mp3
* Documents
  * .pdf

The term assets generally does not refer to elements which contain textual content like pages.

Asset files can be quite large, so when badly managed they can really slow down a website and guzzle up mobile data on phones. With the help of platformOS and AWS, Siteglide uses a range of techniques to cache assets as efficently as possible while making it convenient for developers to make changes to files like CSS and JS and see the results instantly on the next browser refresh.

### Where are Assets Hosted?

Assets you upload to your Siteglide websites are stored directly on an Amazon Web Services (AWS) server, separate to the website you are building on, so that they can be accessed using CloudFront content delivery network (CDN) from your website.

Checkout [File Manager - Introduction](./) for supported file types.

### Caching Control

Assets have automatic caching control using timestamps each time a file is updated. The Content Delivery Network (CDN) offers a multi-tier cache by default, with regional Edge caches around the world.

When an asset is updated, the timestamp changes too, forcing the browser to use the newer version from the CDN, instead of using the locally cached version on the visitor's device.

The result is that anyone who views your website will see none other than the most up-to-date versions of your files.

### Edge Locations

The Amazon CloudFront content delivery network (CDN) is massively scaled and globally distributed. The CloudFront network has 217 points of presence (PoPs), and leverages the highly-resilient Amazon backbone network for superior performance and availability for your website visitors.

When a website visitor views a page, cached assets are retrieved from the closest PoP to their current location.

Caching content gives you the performance and scale you need to give your visitors a fast, reliable and secure experience while viewing your website.

Checkout [Accessing Assets](./) to find out how you can use this on your website.
