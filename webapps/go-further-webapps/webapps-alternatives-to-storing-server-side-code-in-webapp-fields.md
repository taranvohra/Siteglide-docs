# 📋 Alternatives to Storing and Executing Liquid from Database Items

This Article will show how to use custom fields to fetch dynamic content in a WebApp Layout.

## Introduction

Partners often ask us about outputting Liquid from a Rich Text Editor in their WebApps. Unfortunately it's not currently possible to do this- but here we'll explain a little about why- and a technique you can use to achieve the same effects.

## Answer

Currently platformOS doesn't allow Liquid code to be executed within Liquid Fields (such as a Blog's description field). This policy improves security, by making sure it's impossible for user-submitted content to inject malicious Liquid code into your Site- giving you peace of mind that any Liquid code you write is for your eyes only.

We're working on a secure method to allow something like this in the future, but in the meantime, this Article will show you how to use custom fields to fetch dynamic content in the Layout- either above or below your Rich Text field output.

In this example, we'll be adding a Form below the WebApp rich text field.

### Step 1) Add custom fields

You'll need to add the following fields to your WebApp structure:

* Show Form - Checkbox containing values True & False.
* Form ID - String field containing the ID of the Form you'd like to output.
* Form Layout - String field containing the name of the Forms Layout.

![](https://downloads.intercomcdn.com/i/o/233174134/8ae4f6c0a1df33f82eebb2c1/image.png)

### Step 2) Add data to a WebApp Item

Now the fields we'll be using have been defined, add the relevant information to the fields.

### Step 3) Add Liquid to the WebApp Layout where the content will be displayed

Next, locate the WebApp Layout Folder where the Form will be outputted.

Here we can output the Form using the fields that have just been set- wrap the whole include within an IF statement checking whether "Show Form" is "true" if so the Form will be outputted (with the parameters being pulled in from our WebApp). In our example, the Form will be added underneath a Rich Text field.

```javascript
<p>{{this['Rich Text Field Example']}}</p>
{% raw %}
{% if this['Show Form'] == "true" %} 
    {%- include 'form', id: this['Form ID'], layout: this['Form Layout'] -%}
{% endif %}
{% endraw %}


```

Now the fields within the WebApp control whether a Form is outputted for each item.

#### Alternative options for moderating which content the Client can add

\*Hardcoding parameters \*If you only wish the Client to be able to display a single type of Form, you could hardcode the ID and Layout name of this Form straight to the WebApp Layout.

The Client would have control over whether or not to show a Form, but the Form type would always be the one you approved.

\*Using Content Sections \*Content Sections and Code Snippets can also be outputted depending on ID and could provide a range of ready-built content which you could allow the Client to add into their WebApp items.

\*Expanding the Logic \*You could use Liquid Logic in the Layout to only allow certain Form / Content Section IDs to be displayed and forbid others. In this example, Form 2 will never be displayed, even if it is selected:

```javascript
{% raw %}
{% if this['Show Form'] == "true" and this['Form ID'] != "2" %}
    {%- include 'form', id: this['Form ID'], layout: this['Form Layout'] -%}
{% endif %}
{% endraw %}


```

{% hint style="info" %}
You can also use GraphQL queries and mutations to modify and read Pages and Partial files containing Liquid. If you are creating a module and wish for users to be able to organise, store and execute Liquid, this may be a viable method to make this possible safely.
{% endhint %}
