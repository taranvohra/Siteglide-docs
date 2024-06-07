---
title: Introducing Siteglide CLI
slug: '-A-M-'
createdAt: 2021-01-22T14:08:27.000Z
updatedAt: 2023-03-03T08:09:21.000Z
---

# 💡 About Siteglide CLI

Siteglide CLI (Command Line Interface) is a tool that enables you to work on your project from your local IDE or Code Editor; it has similar behaviours to FTP (File Transfer Protocol), in that you can sync up and pull down changes from your website.&#x20;

{% embed url="https://www.youtube.com/watch?t=705s&v=GG3-d5ovJo8" %}

## Who is it for?

Developers will be at home with the Siteglide CLI. It allows them to work faster than they can using the User Interface of the website. It also allows them to access the full suite of time-saving extensions and search tools in IDEs like [VSCode](https://code.visualstudio.com/) and [Atom](https://atom-editor.cc/).&#x20;

But it's not just for Developers! Designers, SEO specialists and Agency Leaders may also find benefits to learning and using Siteglide CLI - allowing them to see an overview over their entire project and quickly find the files they're looking for.&#x20;

## How to Navigate Around?

Check the "File Structure" in each documentation topic, and this will help you find your way around the folders and files.

## Why is there no FTP?

### The Short Answer

With a CLI, we have full control over its functionality. This means we can make it work better for Agencies building sites on Siteglide.

### The Long Answer

There are several reasons why we think a CLI is better for Siteglide projects than an FTP. We'll start with the most important one.

#### We can't use an FTP

Siteglide is built upon the good work done by our friends at platformOS, which in turn runs on AWS (Amazon Web Services). FTP is not supported by some of the AWS services we use e.g. Cloud Storage, so we are unable to use it.

#### Validation

With CLI, we can validate code sent to the site. This is especially useful if you are syncing Liquid or GraphQL code where there are fewer 3rd party tools for linting. If there is a problem we can pick up automatically- the sync will fail and an error message will try to help you find the problem.

#### Version Control

With Siteglide CLI we can keep track of the Code pushed to the Site from Admin and from local machines and make sure the Site always contains the most up to date pushes. It gives us scope to improve this functionality in the future.

#### Developer Tools

Other CLI commands like siteglide-cli graphql  and `siteglide-cli logs` provide developers with advanced tools that would not be available with an FTP.

### Changelog

To see the latest changes to the CLI, we have our changelog [here](https://developers.siteglide.com/cli-changelog)
