A practical example of how to use our .form\_submitting class to build better User Experience for your Forms

# Introduction

When you submit a [Siteglide Form](https://help.siteglide.com/article/99-forms-getting-started), we apply two classes to the \<form> element:

*   `.form_submitting `

*   `.form_x_submitting` - where x is the ID of your Form in Admin.

If the Form fails validation, both classes will be removed.

This Article explains how you can use this feature as a starting point to build more complex User Experiences with your Forms, for example, adding a Spinner while the Form is submitting to give Users confidence it is working as expected.&#x20;

These code snippets are intended as examples only and are not Siteglide Features in themselves. Feel free to use and adapt them in your own Sites, but front-end code is not covered by our [Support Policy](https://help.siteglide.com/article/62-siteglide-support-policy).

# Answer

In this example, we'll show you how to add an SVG spinner icon using SVG animation.
We'll then use the Siteglide classes to show the spinner only when needed.

## Add HTML & CSS

This adds an SVG spinner within a container that centres the content.  In this example, we nest the HTML inside the {% form %} tag (effectively inside the \<form> HTML tag) so that we can centre the spinner inside the Form, however, you could add the spinner wherever you wish.&#x20;

Note the most important part of this CSS example is the use of the Siteglide .form\_submitting class. Only when the class is present, we add the styling needed to display and animate the spinner. You can of course change the CSS in any way you like.

{% tabs %}
{% tab title="CSS" %}
```css
/* Set the Form as position relative so the absolute positioned spinner centres inside it */
form.form {
  position: relative;
}

/* Optional - blur the submitting Form */
/* Ignored by IE 11 */
form.form.form_submitting {
  filter: blur(1px);
}

/* Centre the Spinner Container */
.form_submitting #loadingSpinnerContainer {
  position: absolute;
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Hide the Spinner by default */
#loadingSpinner {
  opacity: 0%;
  display: none; 
}

/* While submitting, show the loading Spinner and run animation*/
.form_submitting #loadingSpinner {
  opacity: 100%;
  display: block;
  width: 120px;
  height: 120px;
  animation-name: spin;
  animation-iteration-count: infinite;
  animation-duration: 3s;
}

/* Define Animation */
@keyframes spin {
  from {
      transform: rotate(1deg);
  }
  80% {
      transform: rotate(360deg);
  }
  to {
      transform: rotate(360deg);
  }
}

```
{% tabs %}

{% tab title="HTML" %}
```html
{% form %}
  <!-- Main Form content here -->
  <div id="loadingSpinnerContainer">
    <svg id="loadingSpinner" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg"> 
      <defs>
        <linearGradient id="Gradient1">
          <stop class="stop1" offset="0%"/>
          <stop class="stop2" offset="30%" stop-opacity="0"/>
          <stop class="stop3" offset="70%" stop-opacity="0"/>
          <stop class="stop4" offset="100%"/>
        </linearGradient>
      </defs>
      <style type="text/css">
        <![CDATA[
          #spinnerRing { stroke: url(#Gradient1); stroke-width: 5; }
          .stop1 { stop-color: #1e94e6; }
          .stop2 { stop-color: #ffffff }
          .stop3 { stop-color: #ffffff }
          .stop4 { stop-color: #1e94e6; }
          #spinnerRing { fill: rgba(0,0,0,0);}
        ]]>
      </style>
      <circle id="spinnerRing" cx="50" cy="50" r="40"/>
    </svg>
  </div>
{% endform %}
```
{% endtab %}
{% endtabs %}

