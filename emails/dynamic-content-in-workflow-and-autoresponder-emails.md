# 👀 Automations Reference

The body of an Automation, whether it is an Email Notification, Custom Liquid Action or API call is a Liquid file, so they can include includes/partials. You can also output fields that were submitted in the Form.

There are a few limitations of this Liquid rendering environment:

* The `export`, `content_for` and `yield` tags are not supported in this environment, which means:
  * The ordinary constants file we include on Pages to make variables like [Company Information](../company-information/company-information.md) work, won't work here. See here instead: Email&#x20;

## Introduction

Emails are Liquid files, so they can include WebApp or Module List Views. They can also include Liquid filters, logic and loops.

## Outputting Form Fields - submitted in the Form which triggered the Email

Let's say you have a User fill in a [form](https://help.siteglide.com/article/99-forms-getting-started) and you want to send a confirmation Email to them, wouldn't it be great to personalise it to them a little? Since they've just filled in their name and other information in the form, accessing the form submission information is extremely useful.

To test, and find the real names of the fields you might need, output all available form submission data in a test Email with: `{{form}}`Use that to identify form fields that you would like to output and use dot notation to output the ones you need.

For example, it should be possible to access the name of the User submitting the form with the following: `{{form.properties.name}}` Custom Fields can also be accessed here, though their database names will show instead of their user-friendly names, so its best to use the content to identify them while testing: `{{form.properties.form_field_4_1}}`

### Outputting WebApp and Module Data in the Email

Visit the related Articles below for reference on the Liquid tags needed to output this kind of Content. One extra thing to think about here is, what if I want to dynamically determine which item I should display in the Email?

#### Outputting a Specific WebApp Item in an Email

To make sure that the Email can access the dynamic ID of custom content you want to display, you can create a custom field in the Form.

This would probably either need to be hidden from the User, or be a datasource type field to allow the user to select an item.

If you prefer the hidden option, you could add the HTML "hidden" parameter in the Form Layout (If this is not enough due to CSS rules, you may also want to wrap it in a `<div>` element with `style="display: none"`.

Note- the first line of the next example has been left as a generic assign (which should work on a Starter Site). You could replace the first line of the example with a ID from a more dynamic source e.g. if the form is outputted within a WebApp List Layout item.layout file, you could use `this.id` .

_E.g. in the Form Layout:_



\`\`\`liquid \{% assign my\_dynamic\_webapp\_id = "98657" %\}

````

</div>

<div data-gb-custom-block data-tag="tab" data-title='Email Automation Liquid'></div>
```liquid
{% raw %}
{% assign my_dynamic_webapp_id = form.properties.form_field_2_1 %}
{% endraw %}
{%- include 'webapp'
    id: '1' 
    item_ids: my_dynamic_webapp_id
    layout: 'portfolio_2'
    per_page: '1'
    sort_type: 'properties.name'
    sort_order: 'asc' 
-%}


````

## Related Articles

* [WebApp List Layouts](https://developers.siteglide.com/webapp-list-layouts)
* [Product List Layouts](https://developers.siteglide.com/list-layouts)
* [Blog Module](https://developers.siteglide.com/blog)
* [FAQs Module](https://developers.siteglide.com/vTdS-faq)
* [Slider Module](https://developers.siteglide.com/slider)
* [Testimonials Module](https://developers.siteglide.com/testimonials)
