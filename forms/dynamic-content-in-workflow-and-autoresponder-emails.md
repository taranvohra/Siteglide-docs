# Dynamic Content in Workflow and Autoresponder Emails

Emails are Liquid files, so they can include WebApp or Module List Views. You can also output fields that were submitted in the Form.

## Introduction

Emails are Liquid files, so they can include WebApp or Module List Views. They can also include Liquid filters, logic and loops.

![](https://downloads.intercomcdn.com/i/o/166272400/412acd207399781addf3d2de/image.png)

## Outputting Form Fields - submitted in the Form which triggered the Email

Let's say you have a User fill in a [form](https://help.siteglide.com/article/99-forms-getting-started) and you want to send a confirmation Email to them, wouldn't it be great to personalise it to them a little? Since they've just filled in their name and other information in the form, accessing the form submission information is extremely useful.&#x20;

To test, and find the real names of the fields you might need, output all available form submission data in a test Email with: `{{form}}`Use that to identify form fields that you would like to output and use dot notation to output the ones you need.&#x20;

For example, it should be possible to access the name of the User submitting the form with the following: `{{form.properties.name}}` Custom Fields can also be accessed here, though their database names will show instead of their user-friendly names, so its best to use the content to identify them while testing: `{{form.properties.form_field_4_1}}`

### Outputting WebApp and Module Data in the Email

Visit the related Articles below for reference on the Liquid tags needed to output this kind of Content.  One extra thing to think about here is, what if I want to dynamically determine which item I should display in the Email?

#### Outputting a Specific WebApp Item in an Email

To make sure that the Email can access the dynamic ID of custom content you want to display, you can create a custom field in the Form.&#x20;

![](https://downloads.intercomcdn.com/i/o/166265732/fff1397765284577d55dd591/image.png)

This would need to be hidden from the User, so you could add the HTML "hidden" parameter in the Form Layout (If this is not enough due to CSS rules, you may also want to wrap it in a `<div>` element with `style="display: none"`.

Note- the first line of the next example has been left as a generic assign (which should work on a Starter Site). You could replace the first line of the example with a ID from a more dynamic source e.g. if the form is outputted within a WebApp List Layout item.layout file, you could use `this.id` .

_E.g. in the Form Layout:_

```html

<div data-gb-custom-block data-tag="assign" data-my_dynamic_webapp_id='98657'></div>

<div style="display: none;">
  <input 
    hidden class="form-control" 
    name="{{ form_builder.fields.properties.form_field_2_1.name }}" 
    data-cfs="4-1-input_text" 
    type="text" 
    value="{{my_dynamic_webapp_id}}"
  />
</div>
```

\*In the Email: \*

```html

<div data-gb-custom-block data-tag="assign" data-0='2' data-1='2' data-2='2' data-3='2' data-4='2' data-5='2' data-6='2' data-7='2' data-8='2' data-9='2' data-10='2' data-11='2' data-12='2' data-13='2' data-14='2' data-15='2' data-16='2' data-17='2' data-18='2' data-19='2' data-20='2' data-21='2' data-22='2' data-23='2' data-24='2' data-25='2' data-26='2' data-27='2' data-28='2' data-29='2' data-30='2' data-31='2' data-32='2' data-33='2' data-34='2' data-35='2' data-36='2' data-37='2' data-38='2' data-39='2' data-40='2' data-41='2' data-42='2' data-43='2' data-44='2' data-45='2' data-46='2' data-47='2' data-48='2' data-49='2' data-50='2' data-51='1' data-52='1'></div>

{%- include 'webapp'
    id: '1' 
    item_ids: my_dynamic_webapp_id
    layout: 'portfolio_2'
    per_page: '1'
    sort_type: 'properties.name'
    sort_order: 'asc' 
-%}
```

## Related Articles

* [WebApp List Layouts](https://developers.siteglide.com/webapp-list-layouts)
* [Product List Layouts](https://developers.siteglide.com/list-layouts)
* [Blog Module](https://developers.siteglide.com/blog)
* [FAQs Module](https://developers.siteglide.com/vTdS-faq)
* [Slider Module](https://developers.siteglide.com/slider)
* [Testimonials Module](https://developers.siteglide.com/testimonials)
