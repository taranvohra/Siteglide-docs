---
description: >-
  Tips for agencies migrating sites from other platforms to Siteglide, and a
  checklist for how to migrate Forms
---

# 🔼 Migrating Forms

## Pre-Requisites

* Recommend migrating Pages first - optional

## Introduction

Forms in Siteglide are more than just HTML.

A Form should be created in the Siteglide Admin, making the following features possible:

* Server-side validation
* Storing Submitted Fields in Cases in the database
* CRM updates
* Secure Zone Access Granting
* User Login
* Automations, including Autoresponder and Workflow Emails

## Step 1) Create the Form in the Siteglide Admin

First, re-create your new Form in the Siteglide Admin, selecting the settings in the UI that you need e.g. the URL it will redirect to after a successful submission.

## Step 2) Add Fields in the Siteglide Admin

Add all the fields you need:

* If your field should update a User in the CRM, create it in CRM users first, then add it as a CRM custom field to the Form
* If you want to add a group of fields, consider creating a Custom Field Set first and add to the Form
* If you want to use a field for this Form and the Cases it creates only, add a standard custom field

## Step 3) Output the Siteglide Form in the Site

Next, find the Liquid file where your old Form is outputted; this is most likely a [Page](../pages/about-pages.md), but could also be a [Page Template](broken-reference) or a [Liquid Include](broken-reference). You may want to keep your old Form code there temporarily for reference, but now is the time to add the Siteglide Liquid code to output a Form there:

```
{% raw %}
{% include 'form', id: '1', layout: 'default' %}
{% endraw %}


```

The ID of your form should be the number associated with the Form in the Siteglide Admin.

A default Layout will be created automatically for you and updated whenever the Form settings change.

## Step 4) Create a Custom Layout - Optional

The new default layout should work fine, but it may not look or function the same way your old one did.

See the reference for tips on creating a Custom Form Layouts:

{% content-ref url="forms-reference.md" %}
[forms-reference.md](forms-reference.md)
{% endcontent-ref %}

## Step 5) Customise your Autoresponder and Workflow Emails - Optional

Automations will be created automatically for an Autoresponder and Workflow Email, but these can be removed or edited to suit your original site's brand and content.

You can also add new automations to trigger events when your Form submits.

## Step 6) Test and Clear Up

Once you're happy your new Form is working, remove your old Form code from the Site to tidy up.

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}
