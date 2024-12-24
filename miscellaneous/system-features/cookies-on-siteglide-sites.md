# Introduction

This document outlines all cookies used on Siteglide sites by default. You can use it to help you write your own cookie policy, but you may need to add to it on order to fully meet your obligations, particularly if you have added third-party code to your website which also uses cookies.

These technologies are evolving, so it's a good idea to keep up to date on how your users' privacy will be affected regularly. 

# What are cookies?

This subject can be tricky to understand for everyone, so we'll start here!

The ICO (an independent UK body set up to uphold information rights in the public interest) defines a cookie as follows: "A cookie is a small text file that is downloaded onto ‘terminal equipment’ (eg a computer or smartphone) when the user accesses a website. It allows the website to recognise that user’s device and store some information about the user’s preferences or past actions." You can read more about cookies from this trusted source here.

There are two main ways of categorising cookies which we'll discuss in the next sections:

# Types of cookies -  is the cookie 1st-party or 3rd-party?

What is the difference between 1st and 3rd party cookies?

The Mozilla Developer Network describes them as follows:

If the cookie domain and scheme match the current page, the cookie is considered to be from the same site as the page, and is referred to as a first-party cookie.

If the domain and scheme are different, the cookie is not considered to be from the same site, and is referred to as a third-party cookie.
Note: Third-party cookies are sometimes referred to as cross-site cookies. This is arguably a more accurate name, as third-party cookies imply ownership by a third-party company or organization. However, the behavior and potential issues are the same whether or not you own all the involved sites.

Source: MDN

This behaviour of 3rd party cookies where data is shared across sites is the main reason why cookies have become such a hot topic in terms of transparency and privacy. It will not be automatically transparent to site visitors that their data is being collected on servers outside of the site they are currently visiting, therefore there is more onus on the site owner to provide that transparency. Furthermore, a developer might include a small script on a website which performs a useful function, but does not realise that this script will allow a server on another site to store 3rd party cookie on the user's browser.

# Inspecting the Cookies on a Site

In your browser's inspect tools, you can normally inspect cookies using the "application" tab. In Google Chrome, you can open dev-tools by pressing F12 and you will see a list of cookies which might look like this:

The highlighted row _pos_session shows an example of a first-party cookie which has been stored on the browser. We know it's first-party because the domain is the same as the site we're visiting. 

The row below shows an example of a third-party cookie. The domain is .linkedin.com and the SameSite=None attribute has been set, which allows the cookie to be read across domains. Source: https://developer.chrome.com/docs/devtools/application/cookies

Only a small string of text is actually stored in the "value" column. Servers can use this as a unique identifier to recognise somebody. Any actual data associated with that user will usually be stored on the server, not in the cookie itself.

Both types of cookies, 1st and 3rd party, can be deleted from a user's browser. 

# 3rd-party cookie phase out begins

Google has announced that they are phasing out 3rd party cookies from their browser Chrome, starting in earnest from Autumn 2024. Since Chrome at the time of writing has a 62.85% market share, this means sites using 3rd party cookies will need to find an alternative soon. 

Rest-assured,  Siteglide sites do not, by default, use 3rd party cookies.

Therefore, Siteglide-provided features on your site will not be affected by the upcoming changes. However, you may have added independently added features from 3rd parties to your sites which are affected; visit their websites to find out if it is possible to update the plugin / script / code. 

Naturally, companies which make revenue from advertising will want to have a replacement for 3rd party cookies ready when 3rd party cookies are phased out. You should still carefully consider when writing your site's privacy policy any new technologies which may impact your users' privacy. See points 3, 4 and 5 here for some early hints on strategies companies will be using going forwards to achieve similar goals to 3rd party cookies: https://developers.google.com/privacy-sandbox/blog/cookie-countdown-2023oct#:~:text=If%20your%20site%20uses%20third,users%20from%20January%204th%2C%202024.

# Types of cookies - is the cookie essential or non-essential?

## Non-essential cookies

Some cookies are not necessary for the main functionality of the site that the user is trying to visit, but they make possible additional features that either the user or the site owner may benefit from.

These cookies may also be known as performance and tracking cookies.

As they are non-essential, the site's user should be given a fair opportunity to opt-in when they begin using a service.

## Essential cookies

The Information Commissioner's Office in the UK lists three kinds of cookies that you are unlikely to need consent for, but notes it is still good practice to be transparent and communicate their existence and purpose to your users:

- cookies used to remember the goods a user wishes to buy when they add goods to their online basket or proceed to the checkout on an internet shopping website;
- session cookies providing security that is essential to comply with data protection security requirements for an online service the user has requested – eg online banking services; or
- load-balancing cookies that ensure the content of your page loads quickly and effectively by distributing the workload across several computers.

Read more from the ICO page on cookies here. 

Some cookies can actually help users protect their privacy rights. Without a session cookie, for example, it would not be possible to allow users to log into a site and it would not be possible to remember their privacy preferences!

# Cookies used by your Siteglide Site by default
Currently, Siteglide Sites use two essential, 1st party cookies, which are applied automatically on all sites. If you're using the SiteBuilder module, a third cookie may be relevant.

|Name	|1st party or 3rd party?|	Essential or non-essential?|	Purpose:|
|_platformos_session|This is required in order to allow users to use essential features, such as logging into the site or storing shopping cart data.|Siteglide stores a short string of text on the User's browser and uses this to identify their session. It is then able to store fields in its own database relating to that session. You can see the exact fields stored on your site by outputting {{context.session}} on any the page.|
|CSRF-TOKEN|1st party	essential	This is required in order to help authenticate form submissions and the user session. It is a useful element in platformOS's security for defending against Cross-Site Request Forgery attacks.|
|sg-cookie-policy-settings|1st party	essential|	If you are using the SiteBuilder module and cookie popup layout, this cookie helps the server remember the visitor's cookie preferences and nothing else. Learn more about SiteBuilder.|

Important Exception: 

If you install the eCommerce Module and set up Payment Gateways, the Payment Gateway may add its own 3rd party cookies to the Site. This will by its nature be "essential" to using the eCommerce aspects of the Site. 

To find out more information, visit your chosen Payment Gateway's privacy and cookie policies.