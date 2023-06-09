On Forms you can set the default redirect in the Form Builder view in Siteglide.

However, if you wish to make this redirect dynamic, you can instead include a hidden field on the Form and set the redirect value there.

```html
<input id="s_redirect" 
       value="/home" 
       type="hidden"
/>

```

This example will redirect the user to `/home` no matter what the redirect says in Siteglide Admin. You can alter this value with JavaScript should you wish to have a dynamic redirect.

