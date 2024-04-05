---
description: Add your own branding to the Siteglide Admin
---

# Agency Whitelabelling

​In small phases, we're giving you more opportunities to get your brand noticed on our Platform.

Whitelabelling enables your Agency to re-brand the Siteglide portal by replacing our logo with your own. Re-branding the platform in this way means you are able to provide a more consistent, branded and streamlined service to your clients and maintain a single point of contact with them.

Over time we will continue increasing coverage of the whitelabling capabilities to include things like domain name, among others.

## Admin Logo

To re-brand your Portal and Admin, head over to the [Agency Details](https://help.siteglide.com/article/36-agency-getting-started) page, [upload your logo](https://help.siteglide.com/article/36-agency-getting-started) and enable "whitelabelling".

## Login

Below is an Endpoint and example snippets of code you can use to enable your Clients to login to Admin directly from your own Agency website.

You'll need the code below as a minimum. You can then add your own HTML/CSS/JS designs and branding on top.

### HTML and JavaScript

{% tabs %}
{% tab title="HTML" %}
```liquid
{% raw %}
<script src="{{ 'js/s_login.js' | asset_url }}"></script>
<form onsubmit="s_login(this)">
	Email <input type="text" name="email" />
	Password <input type="password" name="password" />
	<input type="submit" value="Login" />
</form>
{% endraw %}
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
function s_login(el){
	event.preventDefault();
	let form = el.closest('form');
	let data = {
		email: form.querySelector('[name="email"]').value,
		password: form.querySelector('[name="password"]').value
	};
	var xReq = new XMLHttpRequest();
	xReq.open("POST", "https://api.siteglide.co.uk/api/public/general/sessions/login");
	xReq.setRequestHeader("content-type", "application/json");
	xReq.onreadystatechange = function(){
		if(xReq.readyState === 4){
			let response = JSON.parse(xReq.response);
			if(response.error){
				alert(response.error);
			}else if(response.session){
				window.location.href = 'https://admin.siteglide.com/#/public/login?s='+response.session;
			}
		}
	}
	xReq.send(JSON.stringify(data));
}
```
{% endtab %}
{% endtabs %}
