---
description: Get started with our CLI
---

# 🚀 Quickstart

{% hint style="info" %}
If unsure please read more about CLI first:
{% endhint %}

{% content-ref url="about.md" %}
[about.md](about.md)
{% endcontent-ref %}

## Step 1: Install the Siteglide CLI

The Siteglide CLI can be installed from NPM using:

```
npm i -g @siteglide/siteglide-cli
```

{% hint style="info" %}
If you hit any issues please check our Troubleshooting guide:
{% endhint %}

{% content-ref url="troubleshooting.md" %}
[troubleshooting.md](troubleshooting.md)
{% endcontent-ref %}

## Step 2: Connect to a Site

Setup a local folder and use the site specific command to connect directly to your site (you can find this on the site details page in Portal):

```
siteglide-cli add --email me@mydomain.com --url https://my_great_site.com
```

{% hint style="info" %}
Need some help? Read our full Site Setup Guide:
{% endhint %}

{% content-ref url="site-setup.md" %}
[site-setup.md](site-setup.md)
{% endcontent-ref %}

## Step 3: Start Building!

You should now be ready to start work, you'll likely want to pull down the files from the server:

```
siteglide-cli pull <env>
```

Check out our Reference article for a full list of useful Commands:

{% content-ref url="reference.md" %}
[reference.md](reference.md)
{% endcontent-ref %}
