---
title: Accessing Assets
slug: cvse-
createdAt: 2021-02-17T16:38:54.000Z
updatedAt: 2023-03-03T08:09:58.000Z
---

# 🔹 Linking to Assets Explained

Find out how to use the asset\_url filter to generate a path to your assets and understand the benefits of hosting assets on our CDN.

You can see more examples in the [Assets Reference](/cms/file-manager/assets-reference.md)

## Introduction

Assets are stored directly on an Amazon Web Services (AWS) server, separate to the website you are building on. They can be accessed using a Content Delivery Network (CDN) from your website.

## Benefits

The use of this method offers automatic Caching control, which decreases the likelihood that someone views your website with anything other than the most up-to-date versions of your files. The CDN also reduces page load times, as the assets are not stored on your site, but instead are distributed to over 100 edge locations around the world.

## CDN Asset URLs for the Best Performance

If you have uploaded an image to the images folder using File Manager, it will have a file path like this in the database: `images/SG-Logo-White.svg`. But the real URL for the asset will be on a completely different domain, specific to the instance of the CDN your site is using. It would be frustrating to find and type out the long URL to the CDN each time you want to use an asset, so there is a shortcut:

The best way to add the image to a Liquid file of any kind, whether that's a Page, Page Template, Layout or Automation email is to add the following liquid to your page, so that the server automatically appends the CDN URL: `{{ 'images/SG-Logo-White.svg' | asset_url }}`

You will see that the asset will render on the page with a similar path to this: `https://uploads.prod01.oregon.platform-os.com/instances/283/assets/images/SG-Logo-White.svg?updated=1549914206`

This also works if you add an image path to a file in File manager as a string, and use the same `asset_url` filter:

```liquid
{% raw %}
<div class="bg-image" style="background-image: url('{{"images/example.jpg" | asset_url}}')"></div>
{% endraw %}
```

Which renders to:

```html
<div class="bg-image" style="background-image: url('https://cdn.staging.oregon.platform-os.com/instances/xxxxxx/assets/js/myfile.js?updated=1733383736255')"></div>
```

Each site has a unique CDN path, you can find out what yours is by rendering an image on the page and inspecting on it. `?updated=` is a parameter automatically included that time stamps your files, helping with cache control.

{% hint style="info" %}
You can get the CDN URL fully formed from File Manager. But there is a small catch! The URL will only give the current value of the "updated" parameter, which means it won't dynamically updated if the image is updated. This is useful in a Blog post where the content cannot be dynamic, but if working in Liquid the best practice is to dynamically generate the CDN URL with `asset_url`.
{% endhint %}

## Relative Asset URLs - Good Performance and convenient but may have caching issues for regularly updated assets

Using ../ automatically appends the URL to your asset within CSS files:

```css
.any-class {
  background-image: url('../images/SG-Logo-White.svg');
}
```

`../` is relative to the location of your stylesheet which will already be inside the CDN. This is especially useful for background images. You can look up CSS relative paths online for more information.

Note that this can have drawbacks with assets which are regularly updated, as you may pull in a cached version of the image. Using `asset_url` instead prevents this as it always appends the URL with a timestamp, busting the cache and getting the most recent version.&#x20;

## Vanity Asset URLs - Slower Performance, but sometimes a Client Requirement

In some cases* you may wish to hide the AWS CDN `(https://uploads.prod01.oregon.platform-os.com)` and only refer to the vanity domain of the site (https://www.mydomain.com). To dynamically achieve this, you can use the liquid parameter `asset_path` rather than `asset_url` when calling an asset to a page. Any of the above examples are also applicable with this method.

{% hint style="info" %}
This might be a client requirement for example, if an end user is downloading an PDF, and wants to see your site's domain in the download URL. However, it is still not considered best practice, since it is slower.
{% endhint %}

`{{ 'images/SG-Logo-White.svg' | asset_path }}`

You will see that the asset will render on the page with your vanity domain in it's path, similar to this: `https://www.mydomain.com/assets/images/SG-Logo-White.svg?updated=1549914206`
