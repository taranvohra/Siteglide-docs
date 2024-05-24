# 🔧 Troubleshooting Siteglide CLI

### Debug Mode

Sometimes Siteglide support may ask you to run the CLI in "debug mode". This provides more output into your terminal so that we can use it to aid in supporting you. To do this, you need to prefix the command you are running with some extra information. This prefix differs slightly on macOS, Linux and Windows, for example if you were to want to sync to a site with debug mode on:

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
