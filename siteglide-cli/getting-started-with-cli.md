# 📋 Steps to Install Siteglide CLI

{% hint style="info" %}
Siteglide CLI is a tool for the command line. \
\
Examples of command line apps will vary by operating system. For example, Windows uses cmd-prompt, powershell etc. \
\
Find a command line tool which works for you. You may need to learn basic commands like changing directory, but beyond that, we'll give you the commands you need. \
\
We recommend using a command-line tool integrated into a Code Editor like VSCode for a smooth experience, which will automatically open the command line in the correct directory and keep terminals next to the relevant project.
{% endhint %}

## Step 1) I'm Not Sure if I've Set Up Siteglide CLI Already?

In a Command Line, in any directory, type in:

```
siteglide-cli -v
```

If you already have siteglide-cli installed globally, this will tell you which version you have installed.

You can find out which is the latest version here: [https://www.npmjs.com/package/@siteglide/siteglide-cli](https://www.npmjs.com/package/@siteglide/siteglide-cli)

## Step 2) Install Node.js Dependencies

The CLI is distributed via Node Package Manager (NPM) and so you will need NodeJS installed on your machine. The easiest way to get this is to visit [https://nodejs.org/](https://nodejs.org/) and download the LTS version as this has better support.&#x20;

Open the download and follow the wizard with the default options to finish install.

Siteglide CLI requires a minimum of NodeJS version 10

## Step 3) Installing Globally on your Machine

You can use the following to install Siteglide CLI in any directory. The `-g` flag instructs your machine to make this command available in any directory (globally)- so you only need to do this on your machine once.

`npm i -g @siteglide/siteglide-cli`

When an update is released for the CLI, you can use the same command as above to install the updated version. Please note that the flags for commands below are not available on all versions of the CLI, updating to the latest version will allow you to use all of them.

### Installing on Windows

The following video will give you a complete walkthrough guide for setting up Siteglide CLI on a Windows machine. Feel free to skip ahead to the parts you find the most useful.

{% embed url="https://www.youtube.com/watch?v=mXnHqrHx0L4" %}

### Installing on Mac

The following video will give you a complete walkthrough guide for setting up Siteglide CLI on a Mac. Feel free to skip ahead to the parts you find the most useful.

The steps I follow in the video can be found [here](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally#manually-change-npms-default-directory). If you are using zsh as your shell then the commands here will have to be run against the `~/.zshrc` file, not `~/.profile`. ZSH is the default for Macs since macOS Catalina, to find out which shell you are using you can run `echo ${SHELL}` in terminal. If the `~/.profile` or `~/.zshrc` files do not already exist then you may need to create them first before running the export PATH command

{% embed url="https://www.youtube.com/watch?v=bKS3368YtvA" %}

## Next - Setup an Individual Site

That's it! Siteglide-CLI is installed on your machine. But next you'll want to set up a specific project folder to interact with one of your Siteglide Sites.
