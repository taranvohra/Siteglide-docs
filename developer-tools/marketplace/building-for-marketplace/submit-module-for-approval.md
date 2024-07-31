# Submit Module For Approval

## Preparing GitHub Repository

Before submitting your Module for approval, you should check that your GitHub Repository is ready.

See the following checklist to confirm it is ready for submission:

*   [ ] You’ve got all your files (assets, logic, layouts etc.) in the correct folders (private, or public)
*   [ ] Your module folder is named in the correct format of `<module_name>`
*   [ ] You have not included a `marketplace_builder` folder
*   [ ] You’ve prepared your `setup.json` file if a model is required for this Module and the Module ID in `setup.json` matches the Vanity ID in Siteglide Admin
*   [ ] You’ve prepared your `ignore-on-update.json` file
*   [ ] You’ve prepared your `install-process.json` file if this is required for your module
*   [ ] Your Module is in a branch named `master` in your GitHub Repository. This is the only branch Siteglide will read from. Note that Github may name your branch `main` by default.  If that happens you can change that [here](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-branches-in-your-repository/renaming-a-branch)

![](/assets/ESJa5xqr3TYHZYlOEta___custom-module-renamegit-branch-1.png)

## Sending your Module to Siteglide

Now that you have created your module, you will need to update the Module item that you made in Admin earlier.

![](/assets/HJwIcwqluHIpKDEhHw7qm_custom-moduile-sending-to-siteglide-1.png)

You will need to edit the item with the following information:

*   **Menu Name** -  If applicable, the name to show in the left hand menu when viewing a Site Admin: Modules > My Module.

*   **GitHub Repo Account** - The name of the GitHub account that your Module’s repository is in.

*   **GitHub Repo Name** - The name of the GitHub repository that your Module’s code is in

*   **Installation Notes** - Any notes on installation - appears in ! icon in ‘action’ column on the Module installation page.

*   **Changelog**- A link to your Module’s changelog documentation, this will display within the Marketplace and next to the “Install” button.

*   **Public** - Do you want this Module to be visible within the marketplace?

You can also find these notes in the tooltips on each field.

Once you have clicked "Save" with the above fields populated, your module will be submitted to the Siteglide team for review.

## After Submitting your Module

Once you’ve submitted your Module for approval you’ll need to give us access to see the Module. This is needed for the initial approval, but also for ongoing access to be able to install the latest version of the Module.


To provide us with access you need to invite Siteglide API (<api@siteglide.com>) as a collaborator for the GitHub Repository. You can do this in your [repository settings](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-user-account/managing-access-to-your-personal-repositories/inviting-collaborators-to-a-personal-repository).

![](/assets/7cS_BUKVvH3MEvfYyR_p-_custom-module-git-collab-1.png)

After accepting the invitation we will review your module. This includes reading the code, installing the module onto a site and testing some of its functionality.  We will create a ticket within our [Support Tickets](https://admin.siteglide.com/#/portal/tickets) area so that you are kept up to date with progress.  Once your Module is approved by us then we will allow it to be shown within the [Siteglide Marketplace](https://admin.siteglide.com/#/portal/community/marketplace) so any user can see and install the Module on their sites

