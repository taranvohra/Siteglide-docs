---
title: >-
  In a Form Layout, Dynamically Select a Secure Zone from an Approved List in
  Admin
slug: u352-
createdAt: 2021-02-16T14:35:55.000Z
updatedAt: 2023-03-03T08:09:51.000Z
---

# Dynamically Assign a Secure Zone during Form Submission

This will show you how and help you decide if using a dynamic single Form or multiple Forms is right for your Use Case.

## Prerequisites

* This Article is written for Secure Zones version 1.2.0. Some of the contents may not apply to earlier versions.

## Introduction

Secure Zones are a useful tool for managing which Users will have access to content on a Site.

To give a User access to one or more Secure Zones, you can attach Secure Zones to a Form. The default behaviour is that a Form will Sign Up a User to all the Form's Secure Zones.

However, it is possible to change this behaviour using a hidden field on the Form Layout. This hidden field's value will by default contain all Secure Zones attached to the Form, but can be modified to contain only a sub-set of those Secure Zones.

{% hint style="warning" %}
#### Note

The hidden field cannot contain a value of a Secure Zone unless it is also attached to the Form.
{% endhint %}

### Continuing to Apply the Exact List of Secure Zones Attached to the Form

If you wish to add single or multiple Secure Zones to a Form and have all those Secure Zones applied to the User with a single Form submission, this continues to be default behaviour and you don't need to do anything different.

You can also remove the hidden field from your Form to keep the default behaviour and avoid any front-end changes: `<input id="s_sz_id" value="55665" type="hidden">`

## An Example Use Case

In this example, let's assume you have the following Secure Zones on your Site:

* Public UK
* Public USA
* Private Employees Only

In this example, we want any Users to be able to complete the "Public Sign Up" Form.

Users filling out this Form will choose their location and we'll automatically change the Secure Zone to match either "Public UK" or "Public USA" depending on their preference.

We do _not_ want ordinary Users accessing the "Private Employees Only" Secure Zone, so we want to be able to exclude this from the options and prevent malicious Users from manipulating the Front End code and gaining access.

## Step 1) Setting Up the Sign Up Form in Admin to Create an Allowed List

In the configuration for the "Public Sign Up Form" in the Siteglide Admin, we can attach the public Secure Zones to the Form: "Public UK" and "Public USA".

By default, the Form will assign Users to both these Secure Zones, but we'll change that later.

![](https://downloads.intercomcdn.com/i/o/260749877/3fd79df2e2edc237e78eb489/image.png)

### A Note on Security

The important thing at this stage is that we have **not** added "Private Employees Only" to the Allow List.

Thanks to this choice, malicious Users with knowledge of developer tools and JavaScript will not be able to manipulate the Public Form to add them to the "Private Employees Only" Secure Zone.

A malicious User from the USA may use Front End code to Sign themselves up to the "Public UK" Secure Zone, just as a malicious User could be untruthful on a Form. But by attaching both Secure Zones to the Form, the Partner or Client is making a clear decision that these "public" Secure Zones are both safe. By safe, we mean nobody will see content they shouldn't if they complete this Form- even if they switch to another zone.

It is the responsibility of Partner and Client to make sure that if a User has access to a Form, that Form only has Secure Zones attached that it would be safe for that User to access.

## Step 2) Adding User Input

In this example, we'll use a Form Field to provide User Input which will change the active Secure Zone dynamically. This is optional, as you may have other reasons for assigning a particular Secure Zone.

![](https://downloads.intercomcdn.com/i/o/260753908/3a71c01de3d8a11f231bf0f9/image.png)

## Step 3) Creating a Custom Form Layout

In order to dynamically assign Users to the correct public Secure Zone, we'll need to create a custom Form layout.

![](https://downloads.intercomcdn.com/i/o/260752059/b500b2ef82a11d495ebeb876/image.png)

A quick tip for setting up the Custom Layout quickly is to start by copying and pasting the content of the default Layout.

## Step 4) Add the Form to a Page

![](https://downloads.intercomcdn.com/i/o/260769080/abe61451d48841f3548bae61/image.png)

## Step 5) Adding JavaScript to the Custom Form Layout

In the code from the default Layout that we've copied, we can see the dropdown field that my Users will use to select their location (and thanks to the code we will write now, their Secure Zone).

```liquid
<div class="row mt-4 select">	
    <div class="col">
    		<label for="form_field_12_1">Location</label>
    		<select class=" required" 
					name="{{ form_builder.fields.properties.form_field_12_1.name }}" 
					id="form_field_12_1">
        			<option value="UK">UK</option>
        			<option value="USA">USA</option>
    		</select>
	</div>
</div>
```

We can also see the hidden field that we must change the value of in order to change the active Secure Zone: `<input id="s_sz_id" value="743,744" type="hidden">` Note- this includes the IDs of the Secure Zones, not their names, so Admin should be referenced so that you know which is which.

The JavaScript will need to select the "#form\_field\_12\_1" element, watch for a change event and then select and change the value of the "#s\_sz\_id" element.

```javascript
<script>

  var locationSelector = document.querySelector('#form_field_12_1');
  
  var chooseSZ = document.querySelector('#s_sz_id');
  
  locationSelector.addEventListener('change', changeSecureZone);

  function changeSecureZone() {

    var eventTargetValue = event.target.value;    if (eventTargetValue == "UK" ) {

      chooseSZ.value = "743";
    } else if ( eventTargetValue == "USA" ) {
      chooseSZ.value = "744";
    }
  }
</script>
```
