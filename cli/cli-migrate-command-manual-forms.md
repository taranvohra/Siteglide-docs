---
title: Migrate - Manual Form setup
slug: FPR1-migrate-manual-form-setup
createdAt: 2021-04-09T13:11:37.000Z
updatedAt: 2023-03-03T08:11:19.000Z
---



{% hint style="info" %}
## Note

This is only necessary if you are not updating to a form built within Siteglide Admin before go live.
{% endhint %}

Depending on your system configuration, sometimes forms will not automatically convert during the migration process.  If this has happened then please follow the steps below to do this manually:

## Download the Form files

Download the files from this release on Github - <https://github.com/Siteglide/migration-form/releases/tag/1.0.0>  You should use the "Source Code (Zip)" link under assets.

## Unpack the files

Now that you have the zip, they need to be put into the correct place.  Drag the `modules` folder from the zip alongside the `marketplace_builder` folder in the migration that you have just triggered.  It should look like the following:

![](https://archbee-doc-uploads.s3.amazonaws.com/rFmCA7ykprxhu_FeyERLM/OJxT6QYeamxHr9BLQ8vIk_screen-shot-2021-04-09-at-141534.png)

## Edit the files

The only line the needs to be edited are in `modules/simpleform/public/notifications/email_notifications/form.liquid` In this file replace line 2 where the `to:` field exists.  Simply replace `admin.email@example.com` with the email address where you would like to receive the workflow notifications.  After that has happened, the file should look like the below:

```yaml
---
to: dean@siteglide.com
from: no-reply@siteglide.com
subject: "New form submission! [{{ context.location.host }}]"
---
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html>
  <head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <style type="text/css" rel="stylesheet" media="all">
    body { width: 100% !important; height: 100%; margin: 0; } a { color: #3869D4; } a img { border: none; } td { word-break: break-word; } .preheader { display: none !important; visibility: hidden; font-size: 1px; line-height: 1px; max-height: 0; max-width: 0; opacity: 0; overflow: hidden; } /* Type*/ body, td, th { font-family: Helvetica, Arial, sans-serif; } h1 { margin-top: 0; color: #333333; font-size: 22px; font-weight: bold; text-align: left; } h2 { margin-top: 0; color: #333333; font-size: 16px; font-weight: bold; text-align: left; } h3 { margin-top: 0; color: #333333; font-size: 14px; font-weight: bold; text-align: left; } td, th { font-size: 16px; } p, ul, ol, blockquote { margin: .4em 0 1.1875em; font-size: 16px; line-height: 1.625; } p.sub { font-size: 13px; } /* Utilities*/ .align-right { text-align: right; } .align-left { text-align: left; } .align-center { text-align: center; } /* Buttons*/ .button { background-color: #3869D4; border-top: 10px solid #3869D4; border-right: 18px solid #3869D4; border-bottom: 10px solid #3869D4; border-left: 18px solid #3869D4; display: inline-block; color: #FFF; text-decoration: none; border-radius: 3px; box-shadow: 0 2px 3px rgba(0, 0, 0, 0.16); box-sizing: border-box; } .button--green { background-color: #22BC66; border-top: 10px solid #22BC66; border-right: 18px solid #22BC66; border-bottom: 10px solid #22BC66; border-left: 18px solid #22BC66; } .button--red { background-color: #FF6136; border-top: 10px solid #FF6136; border-right: 18px solid #FF6136; border-bottom: 10px solid #FF6136; border-left: 18px solid #FF6136; } @media only screen and (max-width: 500px) { .button { width: 100% !important; text-align: center !important; } } /* Attribute list*/ .attributes { margin: 0 0 21px; } .attributes_content { background-color: #F4F4F7; padding: 16px; } .attributes_item { padding: 0; } /* Related Items*/ .related { width: 100%; margin: 0; padding: 25px 0 0 0; -premailer-width: 100%; -premailer-cellpadding: 0; -premailer-cellspacing: 0; } .related_item { padding: 10px 0; color: #CBCCCF; font-size: 15px; line-height: 18px; } .related_item-title { display: block; margin: .5em 0 0; } .related_item-thumb { display: block; padding-bottom: 10px; } .related_heading { border-top: 1px solid #CBCCCF; text-align: center; padding: 25px 0 10px; } /* Discount Code*/ .discount { width: 100%; margin: 0; padding: 24px; -premailer-width: 100%; -premailer-cellpadding: 0; -premailer-cellspacing: 0; background-color: #F4F4F7; border: 2px dashed #CBCCCF; } .discount_heading { text-align: center; } .discount_body { text-align: center; font-size: 15px; } /* Social Icons*/ .social { width: auto; } .social td { padding: 0; width: auto; } .social_icon { height: 20px; margin: 0 8px 10px 8px; padding: 0; } /* Data table*/ .purchase { width: 100%; margin: 0; padding: 35px 0; -premailer-width: 100%; -premailer-cellpadding: 0; -premailer-cellspacing: 0; } .purchase_content { width: 100%; margin: 0; padding: 25px 0 0 0; -premailer-width: 100%; -premailer-cellpadding: 0; -premailer-cellspacing: 0; } .purchase_item { padding: 10px 0; color: #51545E; font-size: 15px; line-height: 18px; } .purchase_heading { padding-bottom: 8px; border-bottom: 1px solid #EAEAEC; } .purchase_heading p { margin: 0; color: #85878E; font-size: 12px; } .purchase_footer { padding-top: 15px; border-top: 1px solid #EAEAEC; } .purchase_total { margin: 0; text-align: right; font-weight: bold; color: #333333; } .purchase_total--label { padding: 0 15px 0 0; } body { background-color: #F4F4F7; color: #51545E; } p { color: #51545E; } p.sub { color: #6B6E76; } .email-wrapper { width: 100%; margin: 0; padding: 0; -premailer-width: 100%; -premailer-cellpadding: 0; -premailer-cellspacing: 0; background-color: #F4F4F7; } .email-content { width: 100%; margin: 0; padding: 0; -premailer-width: 100%; -premailer-cellpadding: 0; -premailer-cellspacing: 0; } /* Masthead ----------------------- */ .email-masthead { padding: 25px 0; text-align: center; } .email-masthead_logo { width: 94px; } .email-masthead_name { font-size: 16px; font-weight: bold; color: #A8AAAF; text-decoration: none; text-shadow: 0 1px 0 white; } /* Body*/ .email-body { width: 100%; margin: 0; padding: 0; -premailer-width: 100%; -premailer-cellpadding: 0; -premailer-cellspacing: 0; background-color: #FFFFFF; } .email-body_inner { width: 570px; margin: 0 auto; padding: 0; -premailer-width: 570px; -premailer-cellpadding: 0; -premailer-cellspacing: 0; background-color: #FFFFFF; } .email-footer { width: 570px; margin: 0 auto; padding: 0; -premailer-width: 570px; -premailer-cellpadding: 0; -premailer-cellspacing: 0; text-align: center; } .email-footer p { color: #6B6E76; } .body-action { width: 100%; margin: 30px auto; padding: 0; -premailer-width: 100%; -premailer-cellpadding: 0; -premailer-cellspacing: 0; text-align: center; } .body-sub { margin-top: 25px; padding-top: 25px; border-top: 1px solid #EAEAEC; } .content-cell { padding: 35px; } /*Media Queries*/ @media only screen and (max-width: 600px) { .email-body_inner, .email-footer { width: 100% !important; } } @media (prefers-color-scheme: dark) { body, .email-body, .email-body_inner, .email-content, .email-wrapper, .email-masthead, .email-footer { background-color: #333333 !important; color: #FFF !important; } p, ul, ol, blockquote, h1, h2, h3 { color: #FFF !important; } .attributes_content, .discount { background-color: #222 !important; } .email-masthead_name { text-shadow: none !important; } }
    </style>
    <!--[if mso]>
    <style type="text/css">
      .f-fallback  {
        font-family: Arial, sans-serif;
      }
    </style>
    <![endif]-->
  </head>
  <body>
    <table class="email-wrapper" width="100%" cellpadding="0" cellspacing="0" role="presentation">
      <tr>
        <td align="center">
          <table class="email-content" width="100%" cellpadding="0" cellspacing="0" role="presentation">
            <tr>
              <td class="email-masthead">
                Data submitted
              </a>
              </td>
            </tr>
            <tr>
              <td class="email-body" width="100%" cellpadding="0" cellspacing="0">
                <table class="email-body_inner" align="center" width="570" cellpadding="0" cellspacing="0" role="presentation">
                  <tr>
                    <td class="content-cell">
                      <div class="f-fallback">
                        <table class="attributes" width="100%" cellpadding="0" cellspacing="0" role="presentation">
                          <tr>
                            <td class="attributes_content">
                              <table width="100%" cellpadding="0" cellspacing="0" role="presentation">
                                {% for d in data %}
                                  <tr>
                                    {% unless d[0] == "slug" or d[0] == "format" %}
                                      <td class="attributes_item"> {{ d[0] }} </td>
                                      <td class="attributes_item"> {{ d[1] }} </td>
                                    {% endunless %}
                                  </tr>
                                {% endfor %}
                              </table>
                            </td>
                          </tr>
                        </table>
                      </div>
                    </td>
                  </tr>
                </table>
              </td>
            </tr>
          </table>
        </td>
      </tr>
    </table>
  </body>
</html>
```

## Sync the files

Turn on `siteglide-cli sync` and save both the `modules/simpleform/public/notifications/email_notifications/form.liquid` and the `modules/simpleform/public/views/pages/form.html.liquid` You will see confirmation in your terminal that the files have uploaded.

## Test a form

Find a form on your website and fill it in, you should then receive a workflow notification to your email address entered above
