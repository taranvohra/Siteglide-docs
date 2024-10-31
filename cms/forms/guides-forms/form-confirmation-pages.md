---
description: >-
  After a User submits a Form and you redirect them to a Confirmation Page, you
  can now insert a dynamic message using fields from the Form.
---

# 📋 Steps to Adding Form Confirmation Pages

After a User submits a Form and you redirect them to a Confirmation Page, you can now insert a dynamic message using fields from the Form.

<figure><img src="../../../.gitbook/assets/single-order (1) (1).jpg" alt=""><figcaption><p>The Form Confirmation can display the information which was just submitted, as a confirmation. They can also be used to display information about an eCommerce transaction.</p></figcaption></figure>

## Prerequisites

* You have set up a [Form](https://help.siteglide.com/article/99-forms-getting-started)

## Introduction

After a User submits a Form, you can redirect them to a Confirmation Page.

Including a Form Confirmation message on the Page they land on allows you to develop a customisable message which can:

* Give Users peace of mind that they submitted the correct information, and allow them to contact you (via a new submission) if they have made any mistakes.
* Include a nested [Order Confirmation](https://developers.siteglide.com/order-confirmation-emails) Layout (previously only available in Emails), which can give full details of any eCommerce Products ordered in the Form submission
* Give a personal touch by including details like the User's name in the message.

## Refresher- How to set up a redirect to a confirmation Page

Step 1) Create a Page in the Siteglide Admin under `CMS > Pages` - this will serve as your Confirmation Page.

Step 2) Edit your Form in the Siteglide Admin under `CMS > Forms`

Step 3) Fill in the \`\`Redirect To\`\` field with the URL of your Confirmation Page:

## Step 1) Including the Confirmation Message

In the Siteglide Admin under `CMS > Pages` in the Code tab, add the Form Confirmation with this Liquid tag:

```liquid
{% raw %}
{% include 'form_confirmation', layout: 'default' %}
{% endraw %}
```

The Layout parameter takes the name of the Layout File you wish to use, without the `.liquid` extension.

## Step 2) Building Form Confirmation Layouts

### File Structure

We store Form Confirmation Layouts at the following Path: `layouts/form_confirmation/` Each Layout should be a single Liquid file with a name of your choice followed by `.liquid`.

{% content-ref url="../forms-file-structure.md" %}
[forms-file-structure.md](../forms-file-structure.md)
{% endcontent-ref %}

### Developing a Layout

You can use the Default Layout, or develop your own.

### Variables

When setting up this feature, we wanted to make sure you could easily keep Layouts consistent between the on-Page and Email success messages.

In an email notification you have access to the "form" variable, containing details of the fields that were submitted in the Form. In the Form Confirmation Layout, we've given you access to this `{{form.properties}}` variable in the same format, as well as the usual `this` variable you may be more familiar with in other Layouts.

You can either copy and paste your Layout from an email notification over to the Form Confirmation Layout and continue to use `{{form.properties}}` , or use the `{{this}}` object as you may be used to in other Layouts.

Note- you will not currently be able to use the `{{this}}` variable inside an Email Notification. If you want to keep the same Layout, stick to the `{{form}}` variable!

_Using`{{this}}`_

```liquid
{% raw %}
<h1>Thanks for getting in touch!</h1>
<p>Nice to meet you {{this.name}}!</p>
<p>We'll get back to your query as soon as possible.</p>
{% endraw %}
```

_Using `{{form.properites}}` in a Layout copied from an Email Notification_

```liquid
{% raw %}
<h1>Thanks for getting in touch!</h1> 
<p>Nice to meet you {{form.properties.name}}!</p> 
<p>We'll get back to your query as soon as possible.</p> 

{% endraw %}
```

#### Outputting Fields Dynamically

You can choose to re-use the same confirmation message for multiple Forms. Here is an example which will list the submitted fields (whatever they may be!) in an HTML table. Be aware, depending on the Form, it may always need some adjustments to cover more unusual field types e.g. Checkboxes:

```liquid
{% raw %}
<p>In the meantime, please double check the information you provided us below:</p>
<div class="responsive-table-container">
  <table>
    <tbody>
      {% for field in this %}
        {% comment %}Use the following unless condition to List fields you'd like to leave out of the message.{% endcomment %}
        {% unless field[0] == "properties" or field[0] == "user_id" or field[1] == blank %}
          <tr>
            <th style="border: solid 1px black">{{field[0]}}</th>
            <td style="border: solid 1px black">{{field[1]}}</td>
          </tr>
        {% endunless %} 
      {% endfor %}
    </tbody>
  </table>
</div>
{% endraw %}
```

If you're interested to read more about using Liquid to loop over the properties of an object, as we've done in this example, see more in this advanced tutorial:

## Step 3) Optional - Including an eCommerce Order Confirmation

You output Details about any eCommerce Order that was made using the Form Submission. You may be familiar doing this already within an email automation.

We've included an \`

\` statement in the example, because this will only work properly if a \`form.properties.\`order\\\_id field is available on the Page. Otherwise it may be that the Form was submitted without the User making an Order.

```liquid
{% raw %}
{% if form.properties.order_id %} 
  {% include "ecommerce/order_details", layout "siteglide_example" %} 
{% else %}
  <p>Looks like you've not ordered anything with us this time. We hope to see you again soon!</p>
{% endif %}
{% endraw %}


```

## Step 4) Optional - Make sure the Confirmation Message is only Displayed Once

The Form Confirmation feature will continue to show details of the most recent Form Submission. If the feature is added to a Page that will have visitors who have not just submitted a Form, this may no longer be relevant.

To prevent confusion, you can choose to clear the Form data from their session so that once the message has been read, it won't display again.

We store two values "form\_id" and "form\_fc" within `{{context.session}}`, which are then used to check whether the Form Confirmation Layout should be inlcuded.

If we wipe these values the first time "Form Confirmation" is included then the Layout won't be included again, this code should be added to your Form Confirmation Layout:

```liquid
{% raw %}
{% session form_id = null %}
{% session form_fc = null %}
{% endraw %}
```
