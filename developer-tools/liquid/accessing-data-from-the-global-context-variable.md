---
title: Exploring the Context Object
slug: 8JFV-
createdAt: 2021-02-17T13:36:16.000Z
updatedAt: 2023-04-11T10:49:51.000Z
---

Want to use Liquid Dot Notation to find dynamic data on your Site? The context variable is most likely the place to look.

# Prerequisites

In this Article, we'll be using dot notation, so if you're not familiar with it, you may want to brush up here:

*   [Getting Started with Dot Notation](/developer-tools/liquid/accessing-data-from-liquid-objects.md)

*   [Advanced Dot Notation - Arrays and Key Maps](/developer-tools/liquid/accessing-data-by-looping-or-iterating-arrays-or-objects.md) - You might not need to fully understand this topic- but a first read of it will be very useful in helping you to recognise the more difficult to handle types of data structure- even if you're not ready to tackle them yet.

# Introduction

Once you've got a good understanding of Liquid Dot Notation, the next step is branch out and discover what is possible. 

Here are some of the most useful places to look for data:

*   `{{context}}` The platformOS object `context` contains a huge tree of information about your Site- often including variables you didn't know you wanted until you discovered them.

*   `{{context.exports}}` The object `exports` sits on the root level of `context` and its role is to allow a global storage location for any custom variables not already included in `context`. You'll mostly use it as a place to access Siteglide specific data, for example, it is the home of data relating to Siteglide categories and will contain WebApp or module data when you use the `collection` parameter in the `include` tag. `exports` will also contain any keys that you have entered within the [Integrations](/cms/automations/quickstart-automations.md) area in Siteglide Admin. You can also add your own data to a namespace in `exports` - see the [platformOS docs](https://documentation.platformos.com/api-reference/liquid/platformos-tags#export) to see how. This is especially useful if you want to include some data in a Content Section, Code Snippet or Layout- but access it in on a higher level e.g. the Page Template.

*   `{{this}}` - This is a Siteglide variable containing data specific to a Layout- you'll only be able to use if within a Layout file. The data will completely change depending on the type of content, so it's a good place to use Dot Notation to explore each time you try a new feature.

In this article, we'll explore the `context` object in more detail.

The `this` object is used differently in different features, so the best place to learn about it is by reading the documentation on the specific feature you're using it with.&#x20;

# Context

The `context` object's role is to provide your Site with contextual information which might help it render HTML in a more flexible and personalised way.

Context should be available in any Liquid file, and this includes auto-responder and workflow notifications. However, bear in mind that context may work subtly differently in an email- for example- it's not possible to see information about the person reading an email- `current_user`  would refer to the person submitting the Form which triggers the email to be queued. 

We'll go through the top level of context's keys and explain each namespace's role. Beyond that, you will have to explore for yourself! 

If a property is marked *advanced only*, it is because we haven't found a use-case for it yet on a Siteglide site, or they are not supported, or there is a newer version of this property which is easier to use. We may mark a feature as advanced only because it is possible for it to conflict with a Siteglide feature and it needs to be used with caution. You may be able to discover your own Use Cases for these- if so we'd be very interested to hear about them! To be clear, we can't offer support if these are used in your Site, but we're noting them here in order to be comprehensive.&#x20;

## authenticity\_token (value)

*Advanced only* - You won't need to use this directly- it is a frequently changing token used as part of the security on form submissions.&#x20;

## session (object)

platformOS uses a single cookie to identify a visitor- whether signed in or not. The `session` object holds information in the database which relates to the visitor with that cookie. This is used in Siteglide eCommerce to allow us to identify someone who has added items to a Cart, without requiring them to Sign In. Learn more about how we use this essential cookie [here](/miscellaneous/system-features/cookies-on-siteglide-sites.md).

***Adding Session Fields
***You can add fields to session and exports objects only. 

The easiest way to add session fields is to use the 
```liquid
{% raw %}
{% session %}
{% endraw %}
``` tag. <https://documentation.platformos.com/api-reference/liquid/platformos-tags#session>

**Compatibility**: To avoid conflicting with future Siteglide features, we recommend that if you use this feature, you prefix any new fields with the initials or name of your Agency.

e.g. Let's say a User has decided to opt-in to a particular non-essential feature or cookie. You could remember this: 
```liquid
{% raw %}
{% session agency_optional_features = 'true' %}
{% endraw %}
```

You can then use logic to only show these features to Users who have opted-in.

```liquid
{% raw %}
{% if context.session.agency_optional_features == 'true' %}
<script>
  //My optional feature script
</script>
{% endif %}
{% endraw %}
```

***Removing Session Fields
***To continue our previous example, if the User chooses to change their preferences and opt out, you can forget the setting by setting it to an empty String: 
```liquid
{% raw %}
{% session optional_features = '' %}
{% endraw %}
```

***Ending a Session***- Advanced only
&#x20;You can use custom GraphQL to completely forget a visitor and end their session. Use at your own risk as we cannot support Secure Zones with Users who have had their Session ended in this way: <https://documentation.platformos.com/api-reference/graphql/mutations#user_session_destroy>

## current\_user (object)

Unlike `session`, this only holds information relating to a User if they are currently logged in to a Secure Zone. It is more sensitive than `` `session` `` and will include a name and email address. If there is no current\_user, it will hold the value `null`.&#x20;

## headers (object) 

Headers are information sent and received when a browser sends a request to a server for an HTML Page. This is a technical area which can be nevertheless useful on some every-day use cases. 

For example, in this Article, we show you how to set up canonical URLs. We use the `headers` object to grab a useful version of the URL: [Preventing Duplicate Content](/cms/pages/page-templates/page-templates-seo-prevent-duplicate-content.md).

Another helpful request header is `HTTP_REFERER`. This tells you the URL of the Page that the User was visited before the current one- assuming this was not deliberately hidden. This can be really useful for redirecting a User back to a particular Page after carrying out an Action.

## params (object)

This object helpfully takes the URL of the current Page and dissects it into chunks which you can use. 

*   slugs refer to parts of a URL separated by forward slashes / - slug, slug2 and slug3 will be available to you only if they exist. This can be helpful if you're implementing breadcrumbs. 

*   query parameters will become available to you if they exist and will be available under the same key they use in the URL. E.g. a parameter in the URL https\://siteglide.com?password=test will become available here: `{{context.params.password}}`

*Advanced only*- When using CLI- `params` can also be used in a form\_configuration to interrogate the form data being sent to the server, including virtual fields.&#x20;

## language (value)

*Advanced only-* You can ignore this, as Siteglide does not support this pOS feature.

## environment (value)

*Advanced only*- This will currently only read the value of "Production" as currently all Siteglide Sites are Production ready- but watch this space!

## is\_xhr (value)

*Advanced only* - Returns true if the Page is being rendered by an XHR (sometimes referred to as Ajax) Request.&#x20;

## location (object)

This is analogous to "location" in JavaScript and can provide you with useful URL information. 

*   `{{context.location.url}}` will get you the full absolute URL for the current Page

*   `{{context.location.href}}`  will get you the relative URL for the current Page without query parameters- useful if you want to set new query parameters!

*   `{{context.location.pathname}}` will get you the relative URL for the current Page including query parameters.

This Object is often useful when you use it alongside `params`.

## page (object)

This contains metadata for the Page.&#x20;

## layout (object)

This actually gives you metadata relating to the chosen *Page Template*, not about Layouts on the Page. 

## modules (object)

This contains objects for each module you have installed on your Site. It includes Siteglide Modules and any Modules you've installed via platformOS. It only contains metadata- if you want data relating to items in that Module, you'll have to access it in a Layout with `{{this}}` or through making a `collection` and then looking in `{{context.exports}}`.

## visitor (object)

*Advanced only*- Contains the IP Address of the visitor.

## constants

*Advanced only*-&#x20;

## useragent

*Advanced only*- Use `device` instead!

## device

Device should give you information about your visitor's device, operating system and browser. However, use it with caution - you'll still need to make websites responsive! You could use this to suggest to certain Users that they will have a better experience if they update their browser to a modern one.&#x20;

## cookies

This lists the cookies currently used by the Site. 

Siteglide only uses the session cookie directly which you can learn more about [here](/miscellaneous/system-features/cookies-on-siteglide-sites.md)

Any payment gateways you are using as part of Siteglide eCommerce e.g. Stripe may also have a cookie listed here. 

You may also see cookies relating to browser extensions. Ignore these- as your Users will have different extensions to your Developers!

## version

*Advanced only*

## post\_params

*Advanced only*

## flash

*Advanced only*

## exports

This is where all context data is kept which is custom- either to Siteglide or that you have added to your Site.

