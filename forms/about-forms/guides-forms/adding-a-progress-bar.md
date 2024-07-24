# 📋 Steps to Adding a Progress Bar

### Introduction

When a [Form](https://help.siteglide.com/article/99-forms-getting-started) is submitted on Siteglide, it may have a wide range of tasks to complete e.g. signing a User into a Secure Zone or making a Payment. Sometimes Users may have an improved experience if they know the submission is still making progress and has not frozen.

That's why we've added data-attributes to the Form which will let you know each time a process is complete. You can use these to optimise your User Experience. They won't tell you how much time the submission will take to complete- but they will give the User a sense of continuation and progress.

### Step 1) Inspect The Attributes

The following data-attributes will be added to the `<form>` element after the submission button is clicked.

* `data-s-form-progress` - This data attribute will let you know the most recent step that was completed by the Form Submission.
* `data-s-form-progress-max` - This data attribute will let you know the maximum number of submission steps. At the time of writing, it is fixed at 8, but this may change in future releases. Some steps will be counted in this number even if the Form completes them instantly e.g. the Secure Zone step will be skipped if the Form is not a Secure Zone Form.

You can use CSS which selects these data-attributes to change the User Experience of the Form.

### Step 2) Add HTML for a Progress Bar

```html
<!-- This should be added inside the <form> element -->
<div id="progressBar">
	<div id="progressContent"></div>
</div>
```

### Step 3) Add CSS rules to change the width of the progress bar on each step

The following example displays a progress bar which increments with each submission step that is completed. It uses CSS transitions to create a smooth movement between each discrete step:

{% tabs %}
{% tab title="CSS" %}
```css
#progressBar {
	width: 100px;
	height: 30px;
	background-color: #ffffff;
	border: solid 1px grey;
}

#progressContent {
	width: 0%;
	height: 30px;
	transition: width 0.3s;
	transition-timing-function: ease-in-out;
	background: linear-gradient(to left, #e66465, #9198e5);
	overflow: hidden;
}

.form[data-s-form-progress='0'] #progressContent{
	width: 0%;
}

.form[data-s-form-progress='1'] #progressContent{
	width: 10%;
}

.form[data-s-form-progress='2'] #progressContent{
	width: 20%;
}

.form[data-s-form-progress='3'] #progressContent{
	width: 30%;
}

.form[data-s-form-progress='4'] #progressContent{
	width: 40%;
}

.form[data-s-form-progress='5'] #progressContent{
	width: 50%;
}

.form[data-s-form-progress='6'] #progressContent{
	width: 60%;
}

.form[data-s-form-progress='7'] #progressContent{
	width: 80%;
}

.form[data-s-form-progress='8'] #progressContent{
	width: 100%;
}
```
{% endtab %}

{% tab title="HTML" %}
```html
<!-- This should be added inside the <form> element -->
<div id="progressBar">
	<div id="progressContent"></div>
</div>
```
{% endtab %}
{% endtabs %}
