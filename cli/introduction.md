---
title: Introducing Siteglide CLI
slug: '-A-M-'
createdAt: 2021-01-22T14:08:27.000Z
updatedAt: 2023-03-03T08:09:21.000Z
---

# 💡 About Siteglide CLI

Siteglide CLI (Command Line Interface) is a tool that enables you to work on your project from your local IDE or Code Editor; it has similar behaviours to FTP (File Transfer Protocol), in that you can sync up and pull down changes from your website.&#x20;

The benefit of using a CLI instead of an FTP is that it's designed specially for Siteglide's file structure and contains additional useful tools and features. You will be required to use some terminal commands to use this feature.

## Who is it for?

Developers will be at home with the Siteglide CLI. It allows them to work faster than they can using the User Interface of the website. It also allows them to access the full suite of time-saving extensions and search tools in IDEs like [VSCode](https://code.visualstudio.com/) and [Atom](https://atom-editor.cc/).&#x20;

But it's not just for Developers! Designers, SEO specialists and Agency Leaders may also find benefits to learning and using Siteglide CLI - allowing them to see an overview over their entire project and quickly find the files they're looking for.&#x20;

## How to Navigate Around?

Check the "File Structure" in each documentation topic, and this will help you find your way around the folders and files.



###

***

### Debug Mode

Somtimes Siteglide support may ask you to run the CLI in "debug mode". This provides more output into your terminal so that we can use it to aid in supporting you. To do this, you need to prefix the command you are running with some extra information. This prefix differs slightly on macOS, Linux and Windows, for example if you were to want to sync to a site with debug mode on:

{% tabs %}
{% tab title="cli" %}
```linux
DEBUG=true siteglide-cli sync production
```
{% endtab %}

{% tab title="macos" %}
```macos
DEBUG=true siteglide-cli sync production
```
{% endtab %}

{% tab title="windows command prompt" %}
```windows
set DEBUG=true && siteglide-cli sync production
```
{% endtab %}

{% tab title="windows powershell" %}
```
$env:DEBUG='true'; siteglide-cli sync production
```
{% endtab %}
{% endtabs %}

Note, for macOS and Linux, debugging will be turned on for that one command that you prefix. For Windows, debugging will be turned on for as long as Command Prompt or Powershell is open. Closing Command Prompt or Powershell and re-opening it will turn debug mode off.

### Changelog

To see the latest changes to the CLI, we have our changelog [here](https://developers.siteglide.com/cli-changelog)
