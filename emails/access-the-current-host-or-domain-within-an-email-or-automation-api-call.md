---
title: How do I get the current host within the context of an automation email?
slug: w0bR-how-do
createdAt: 2024-03-06T09:29:26.478Z
updatedAt: 2024-03-06T09:31:54.605Z
---

Normally you can use `{{context.location.host}}` to get the current host (domain) of the page in Liquid.

Within the context of an email, the email is scheduled asynchronously, so technically the Liquid context is not *currently *on a page in a browser. In this context, you can use `{{platform_context.host}}` to get the host of the "default domain". You can set the default domain of your instance in the domains tab in Siteglide Portal.&#x20;