# 🔼 Siteglide CLI Migrate Command

[Static Site Import](https://www.siteglide.com/site-import) is an import tool which scrapes all front-end code of a Site that is currently live on a different platform to Siteglide. After this import, you can simply take this Site live immediately or take the time to integrate this Site with Siteglide's powerful and flexible features.

You can work with SiteGurus on this, every partner that signs up to their Site recieves 10 free credits.

You can also do this yourself using CLI and following instructions and the video below.

**Note:** If you're new to CLI, I highly suggest reading [Introducing Siteglide CLI](../../cli/introduction.md) first.

### Step 1 - Create A Site

Begin this process within your [Admin](https://admin.siteglide.com/#/portal), you'll need to create a Site, with your chosen [migration method](https://help.siteglide.com/article/232-migration-method-checklist) in mind, and if this Site is for a Client or for your own agency.

You can do this by following the instructions here: [Migrations - Creating A Site For Migrating](https://help.siteglide.com/article/244-migrations-creating-a-site-for-migrating), deciding if you'd like to use Studio for this Site.

### Step 2 - Connect to this newly created Site

Creating an environment for this Site enables you to migrate using our Static Site Import, as well as enables you to make changes on this Site in the future, using CLI.

You can do this by using the correct commands within: [Introducing Siteglide CLI](https://developers.siteglide.com/introducing-siteglide-cli); under the heading "Add" -

`siteglide-cli add <env> --email me@mydomain.com --url https://my_great_site.com`

Once you have entered this command, you will be prompted to enter your credentials to ensure you have the correct permissions to import to this Site.

CLI will then authorise your input, enabling you to proceed with running this import.

### Step 3 - Run Static Site Import

Now, it is time to run the Static Site Import.

You can do this by running the "Migrate" command within [Introducing Siteglide CLI](https://developers.siteglide.com/introducing-siteglide-cli):

`siteglide-cli migrate <env> --url <existing url>`

**Flags** - these can be added to the end of the above command:

`--url`: Existing sites URL, usually the homepage. This flag is mandatory`-n`: No Optimization, skips the CSS/JS and Image optimization`-a`: Automatically deploy the site after it has finished migrating

This will begin to scrape all front-end code from the Site that is currently on a different platform and import this onto your Site in Siteglide.

**Note:** The time this import will take will vary, depending on your internet speeds and the size of this Site. It is best to use this import with smaller Sites, and mainly static Sites.

### Step 4 - Successful Import

Once this import has been completed, CLI will provide you with a "Success" message.This tool will look to see how your Site can be improved and optimised by updating URLs; minifying code files; compressing any images.

This front-end code will proceed to be deployed to your Siteglide Site.

You can compare [Google Page Speed Scores](https://developers.google.com/speed/pagespeed/insights/) of your current Site and your new Siteglide Site to see the true benefits in this tool.

**Note:** The SEO score in Google Page Speed will likely drop as by default the imported site will be set to block Search Engine spidering until your domain is added.

### Step 5 - Integrate With Siteglide Features

After a successful import and deploy to your Siteglide Site, you can head to this Site within your Admin.

Upon looking at your Site within Admin, you will see that your Pages have been created for you to manage and edit. These Pages will contain head, header and footer scripts, as well as Page Content. This is something you can change by implementing [Page Templates](../../pages-and-page-templates/page-templates.md).

Your images will be showing on this Site, just as they are in your current Site.

**Note:** _Images have been uploaded to a folder called "/assets" and so are outside of the four main folders in File Manager. These will pull through into Pages correctly, but may not be currently visible within Admin._

After having completed this import, partners decide to go with one of two routes:

* Take this Site live as it is - and integrate with more Siteglide features later on, as the Client's budget allows.
* Integrate with Siteglide features now for even more benefits, then proceed to take this Site live.
