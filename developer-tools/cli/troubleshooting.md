# ❔ Troubleshooting

## Not Sure if You've Set Up Siteglide CLI Already?

In a Command Line, in any directory, type in:

```
siteglide-cli -v
```

If you already have siteglide-cli installed globally, this will tell you which version you have installed.

You can find out which is the latest version here: [https://www.npmjs.com/package/@siteglide/siteglide-cli](https://www.npmjs.com/package/@siteglide/siteglide-cli)

## Have You Installed the Dependencies?

The CLI is distributed via Node Package Manager (NPM) and so you will need NodeJS installed on your machine. The easiest way to get this is to visit [https://nodejs.org/](https://nodejs.org/) and download the LTS version as this has better support.

Open the download and follow the wizard with the default options to finish install.

Siteglide CLI requires a minimum of NodeJS version 10

## Have you Installed the CLI Globally on your Machine?

You can use the following to install Siteglide CLI in any directory. The `-g` flag instructs your machine to make this command available in any directory (globally)- so you only need to do this on your machine once.

`npm i -g @siteglide/siteglide-cli`

When an update is released for the CLI, you can use the same command as above to install the updated version. Please note that the flags for commands below are not available on all versions of the CLI, updating to the latest version will allow you to use all of them.

## Issues Installing on Windows?

The following video will give you a complete walkthrough guide for setting up Siteglide CLI on a Windows machine. Feel free to skip ahead to the parts you find the most useful.

{% embed url="https://www.youtube.com/watch?v=mXnHqrHx0L4" %}

## Issues Installing on a Mac?

The following video will give you a complete walkthrough guide for setting up Siteglide CLI on a Mac. Feel free to skip ahead to the parts you find the most useful.

The steps followed in the video can be found [here](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally#manually-change-npms-default-directory). If you are using zsh as your shell then the commands here will have to be run against the `~/.zshrc` file, not `~/.profile`. ZSH is the default for Macs since macOS Catalina, to find out which shell you are using you can run `echo ${SHELL}` in terminal. If the `~/.profile` or `~/.zshrc` files do not already exist then you may need to create them first before running the export PATH command

{% embed url="https://www.youtube.com/watch?v=bKS3368YtvA" %}

## Struggling to Connect to a Site?

Read our in-depth guide:

{% content-ref url="site-setup.md" %}
[site-setup.md](site-setup.md)
{% endcontent-ref %}

## Debug Mode

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
