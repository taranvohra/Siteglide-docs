# ℹ️ Updating Modules

Here I will outline key tips and information in maintaing your existing module once it has been created.

## Maintaining Your Git Repo

When anyone (yourself or someone else) installs your module, it will automatically take a copy of anything currently within the master branch of your Git Repo.

If you would like to work on updates or new additions to your module, it is strongly recommended that you create a new branch in your repository so that it does not impact what is installed until your are ready.

![](../../assets/mwoDnyZkvcZVBbP7w-ADO\_custom-module-renamegit-branch-1.png)

Create a new branch and call `staging` for example. From now on, send your initial commits to staging while you are testing. When you are ready to release an update to your module, merge into the `master` branch in Git.

## Notifiying Users Of An Update

Once you have committed a new version to your `master` branch in Git, edit your module in Siteglide Portal to update the version number and let people know there is a new version available to install.

![](../../assets/KoZxLfmcroSdmkF1B7OMG\_custom-module-update-version-1.png)
