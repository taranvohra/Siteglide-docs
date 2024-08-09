---
title: Secure Zones
slug: qV4--
createdAt: 2021-02-16T14:30:04.000Z
updatedAt: 2023-12-14T15:18:54.409Z
---

# ℹ️ About

We provide the Liquid for Sign Up, Login and Password Reset Forms and for checking if the current User is signed in

## Introduction

In this Article we'll provide the Liquid which can be used to manage access to [Secure Zones](https://help.siteglide.com/en/article/secure-zones-getting-started-15nnl5f/). It can be used across most Liquid Files (excluding emails).

## Syntax

### Log In

`<div data-gb-custom-block data-tag="-" data-0='login_form' data-1=', layout: ' data-2='default' data-3=', redirect: ' data-4='/'></div>`

### Log In / Sign Up

`<div data-gb-custom-block data-tag="-" data-0='form' data-1='form' data-2='1' data-3='1' data-4=', layout: '></div>`

This is the same syntax for inserting a custom Form, where the id parameter should be the id of your Form. See the section [Creating a Sign Up Form](https://help.siteglide.com/article/138-secure-zones-getting-started#2-adding-a-sign-up-form) to learn more.

Once you have created a Form, you can select the Form from Toolbox and it will dynamically fill in the ID for you.

### Log Out

`<div data-gb-custom-block data-tag="-" data-0='logout_button' data-1=', layout: ' data-2='default'></div>`

### Recover Password Flow

#### Recover Password Form

The recover password form is the first step in recover password flow. Users should be presented with this form as they first realise they've forgotten their password. Completing the form sends an email to the provided address containing next steps.

By default, a system page will already be created on your site at `/system/recover-password`, which can be found in Admin under `Site Manager/System Pages` . You can edit that page, or add the form to a new page with the tag:

```liquid
{% include 'recover_password',
	buttonText: 'Submit',
	redirect: '/'
-%}

```

#### Password Reset Email

You can find and edit the Password Reset email in the Siteglide Admin under `Site Manager/System Emails`

It must contain a link to the dynamically generated URL: `{{context.exports.reset_password.data.reset_password_url}}`.

This will be the system page `/system/reset-password` with a dynamically generated token attached as a parameter.

#### Reset Password Form

This is the last step in the recover password flow where the user has already clicked the link in the email. If the token in the link is correct, they will be able to complete the form and their password will be changed.

This form should normally be outputted on the `/system/reset-password` System Page, as this is where the dynamic link from the email will point. You can optionally redirect users back to the page where they can sign in with their new password.

```liquid
{% include 'reset_password'
	failContent: 'The provided token is no longer valid. Please request password instructions again.',
	buttonText: 'Submit',
	redirect: '/'
-%}
```

## Liquid Tags

These Liquid tags can be outputted in most contexts to get you quick information about a logged in user. They are not currently supported inside emails.

| **Field Name**          | **Liquid Tag**                            | **Description**                                                                                                      |
| ----------------------- | ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| is\_logged\_in          | \{{context.exports.is\_logged\_in.data\}} | true/false (boolean), the value is not stored as a string. Used to determine if the user is logged in or logged out. |
| Current User First Name | \{{context.current\_user.first\_name\}}   | Outputs First Name of User currently signed in                                                                       |
| Current User Last Name  | \{{context.current\_user.last\_name\}}    | Outputs Last Name of User currently signed in                                                                        |
| Current User Email      | \{{context.current\_user.email\}}         | Outputs Email Address of User currently signed in                                                                    |
