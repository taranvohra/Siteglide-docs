Caching is a good way to speed up Page load for most of your Users for a period of time.

# Introduction

When you load a Page, a key metric is Server Response Time- the time it takes for the Server to deliver an HTML Page to the browser. This can be slightly higher for a Page which relies on dynamic content, because the server has more work to do.&#x20;

Caching is one way you can reduce this time for most of your users. There are a few different ways to cache Liquid, but here we will cover Fragment Caching, as it doesn't require Siteglide CLI and is the easiest to get started with.&#x20;

Here's how it works: 

1.  The Developer implements Fragment Caching around a block of code which includes some Liquid. 

2.  When the next visitor arrives on the Page, it will load as normal, but a snapshot of that Liquid code (a cache) is taken by Siteglide. It is stored on the server with an expiry time and a "key". 

3.  The Cache remains in place until either the expiry time runs out or the Cache "Key" is changed. During that time, visitors to the Page will enjoy a faster experience- because instead of running the Liquid, the server will deliver the snapshot of HTML instead. This does mean that they won't receive any updates made to content while the Cache is active- we'll discuss this below.

4.  Once the Cache expires, the next User to visit will have to wait for Liquid content to load and another Cache snapshot will be taken.

# Syntax

## Cache Key

You'll need to create a Cache Key. This is a String that effectively names the Cache that is taken of your Site. Changing it will bust the Cache and cause a new Cache snapshot to be taken. The Liquid Capture tag just creates a String with the contents you include inside it, so you don't need quote marks. You can give the variable any name you like, so here I've gone for `my_cache_key
{% capture my_cache_key %}<!-- Add a string here -->{% endcapture %}`

You can include dynamic content in your cache key- a really useful thing to do is to include the URL of your Page in the Cache Key. This will allow things like Pagination to bust the Cache and load a new one- without it, changing Page will keep loading the same content. This is the same for things like search queries.&#x20;
`{% capture category_cache_key %}{{context.headers.PATH_INFO}}{% endcapture %}`

## The Cache Tag

You can use the Cache tag to wrap the block of Liquid code that is slowing your Page down. You can wrap languages like JavaScript too, but it will have no effect on performance, as they will run on the Browser - long after the Cache has loaded.&#x20;

```html
{% cache category_cache_key, expire: 60 %}
   <!-- code here -->
{% endcache %}
```

### The Expire Parameter:

Getting this right is a fine art. It really depends on your Site and what you are trying to achieve. An integer is needed to determine the number of **minutes** a Cache will be active for before it expires and a new Cache is made.

Set this as a large number of minutes (e.g. a day 300000) if:

*   Performance is essential to your Page's purpose

*   Content is not updated regularly

*   Lots of Liquid is used on the Page, especially several `` `{% include 'webapp' %} `` tags. 

*   You have a low traffic rate- If only a few users visit each day, you will need a longer expiry in order for the difference to be noticed.

Set this as a small number of minutes (e.g. 60) if:

*   Content is regularly updated

*   You just want to protect against DDOS attacks or you have high traffic and want to improve the experience for a large number of users.

# Busting the Cache using the Key

What if you want the Cache to last from a long time normally, but you want content to be updated immediately when there is an update to a key piece of dynamic content? You may even just want to bust the Cache while you are developing something.

To do this, you want to change the Cache key.&#x20;

Let's say the Cache key is just the URL of the Site.:

`{% capture category_cache_key %}{{context.headers.PATH_INFO}}{% endcapture %}`

To bust the Cache manually, you can either:

*   Add a parameter to the URL - `?test=test`

*   Change the Cache key e.g. add a number at the end.

`{% capture category_cache_key %}{{context.headers.PATH_INFO}}-1{% endcapture %}
`
To change the Cache Key dynamically, add dynamic Liquid to the Cache Key, e.g. from a custom GraphQL query, a WebApp or a Module.

