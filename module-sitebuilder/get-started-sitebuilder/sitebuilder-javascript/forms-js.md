# 🔹 Forms JS

The forms JavaScript is a lightweight script which includes a small function for handling checkbox valiadation.

Essentially, it handles instances where there is one checkbox field in the Siteglide Admin with multiple options; the field is required, but only one of the options needs to be checked ideally before the form is submitted. The script dynamically adds and removes the required HTML attribute from the checkboxes to achieve this effect.

Most validation scripts are included directly in the forms layouts to allow easier customisation, but the checkbox validation script has been abstracted because it is quite specialised.

### Normally included in: <a href="#normally-included-in" id="normally-included-in"></a>

Page Templates

### Script Code <a href="#script-code" id="script-code"></a>

```liquid
<script async id="sitegurus_forms_javascript_api" src="{{'modules/module_86/js/sitegurus_forms_javascript_api.js' | asset_url}}" charset="utf-8"></script>
```
