# 📋 Steps to Testing Emails on a Staging Site

## Introduction

Staging sites are great as a place to start building your business, or as a place to develop new updates to a site before they're ready to see the world. However, what if you did a Site Copy of your live site to test a new feature on staging and accidentally sent an unfinished email to real customers?

Don't panic! That can't happen!

Staging sites deliberately block outgoing emails.

Okay so how do we test?

## Step 1) Find your Site in the Siteglide Portal

Click the "Configuration" tab:

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Step 2) Fill in the Test Email Field

Enter the email addresses of anyone who would like to receive test emails for this site. It doesn't matter if they are Siteglide users or not: e.g.\
\
example@siteglide.com,example@agency.com,example@client.com

{% hint style="info" %}
When you get to step 3, you'll realise that being added to this list can mean getting a lot of emails, so make sure you get permission before adding people to this list or they may be annoyed!&#x20;
{% endhint %}

## Step 3) Test an Email

E.g. Test submitting a Form which has an Email Automation attached, even if your email address is **not** in the `to` field.&#x20;

You'll see that if you added your email in step 2, you'll receive **all** emails on the site, regardless of who they are addressed to. This makes it easy to test emails without running lots of email accounts for different user types.&#x20;

## Step 4) Checking the To Address is Correct

If you're getting all the emails, how do you check if they go to the right person?

When the email is blocked from sending as normal, the system adds the address it would have sent to in a production environment in brackets to the subject line on a staging site. You can use this to identify the test email in your inbox or check if it is sending to the correct address before going live.
