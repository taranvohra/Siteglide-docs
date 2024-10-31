# 📋 Steps to Optimise Images on the Fly with Cloudinary

## Introduction

[https://cloudinary.com/](https://cloudinary.com/) is a 3rd party service which we recommend as a convenient way to transform assets on the fly to change their size or format.

When building sites for fast performance, there is often a compromise with convenience. Tools like [Google Page](https://pagespeed.web.dev/)[ Speed Insights](https://pagespeed.web.dev/) remind you to store multiple sized versions of the same image in order to optimise them to different sized device screens and resolutions. You also want to serve images in next-gen formats like `webp`, but your client will usually upload `jpg` or `png` images.

Cloudinary allows you to get the best of both worlds, by using the Siteglide File Manager's AWS CDN to store single original copies of each image for a clutter-free, easy experience for clients, while in the code you can dynamically transform images to optimise them perfectly to the site vistors. Cloudinary also caches their transformations, so after the first time they are delivered as fast as if you had already uploaded different versions to the CDN.

## Step 1 - Create a Cloudinary Account

Go to [https://cloudinary.com/](https://cloudinary.com/) and follow the steps to create an account.

## Step 2 - Make a Note of your Cloud Name

This will be an essential part of the URLs.

[https://cloudinary.com/documentation/cloudinary\_credentials\_tutorial](https://cloudinary.com/documentation/cloudinary\_credentials\_tutorial)

## Step 3 - Generate your first URL inside your code

To build a URL, you will need to start with the beginning of the Cloudinary URL, which will direct the browser to their API endpoint, replacing 'demo' with your cloud name from step 2:

`https://res.cloudinary.com/demo/image/fetch/`\\

Next add your optional transformations to resize the image by a number of pixels width or height:

`https://res.cloudinary.com/demo/image/fetch/h_200,w_200`

Next optionally add transformations to automatically transform to next-gen image formats on supported browsers only:

`https://res.cloudinary.com/demo/image/fetch/h_200,w_200/f_auto/`

then use Liquid to get the path to the original image on Siteglide's CDN. See

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

For example:

`{{'images/example.jpg' | asset_url}}`

Putting it all together:

```liquid
{% raw %}
https://res.cloudinary.com/demo/image/fetch/h_200,w_200/f_auto/{{'images/example.jpg' | asset_url}}
{% endraw %}
```

## Step 4 - Add HTML to deliver the Appropriate URL to several Screen Resolutions - Optional

[Source: MDN](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia\_and\_embedding/Responsive\_images)

```liquid
{% raw %}
<img
  srcset="https://res.cloudinary.com/demo/image/fetch/w_480/f_auto/{{'images/example.jpg' | asset_url}} 480w, https://res.cloudinary.com/demo/image/fetch/w_800/f_auto/{{'images/example.jpg' | asset_url}} 800w"
  sizes="(max-width: 600px) 480px,
         800px"
  src="https://res.cloudinary.com/demo/image/fetch/w_800/f_auto/{{'images/example.jpg' | asset_url}}"
  alt="Example of serving different sized images on different screen widths" />
{% endraw %}
```

Learn more about the

## Step 5 - Read the Cloudinary Docs and Experiment with more Image Transformations - Optional

There are many more options available. Read more here:

[https://cloudinary.com/documentation/image\_transformations](https://cloudinary.com/documentation/image\_transformations)\
\
In these examples, you may need to replace 'upload' with 'fetch' in the URL to support remote images from the Siteglide file manager.

Also check out using client hints on some browsers to further fine-tune image requests:

[https://cloudinary.com/documentation/responsive\_server\_side\_client\_hints](https://cloudinary.com/documentation/responsive\_server\_side\_client\_hints)
