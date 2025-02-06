---
hidden: true
---

# Admin Menu Editor

With this feature you can change what shows in the left hand menu in Admin when viewing a Site.

The data is a JSON structure, and here's an example of the key/value pairs supported:

| Key         | Value                                                                                                                                                       | Example                               |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------- |
| name        | The name of your menu item                                                                                                                                  | CMS                                   |
| icon        | The icon to show, chosen from [FontAwesome v5 Regular icons](https://fontawesome.com/v5/search?o=r\&s=regular)                                              | browser                               |
| path        | The path/URL of your item. You can either use a relative path to stay within Siteglide, or an external HTTPS link                                           | cms                                   |
| new\_tab    | Should the link open in a new tab?                                                                                                                          | false                                 |
| children    | An array of child menu items, following the same JSON structure                                                                                             | \[{"name": "Pages", "path": "pages"}] |
| role\_allow | The ID of the only User Roles that this will show for. This is the quickest way to only show a link to specific User Roles.                                 | 1 (Administrator)                     |
| role\_deny  | The ID of the User Roles this will not show for. This is the quickest way to stop showing a link to specific User Roles.                                    | 3 (Client Restricted)                 |
| permission  | The key of the only Permissions that this will show for. You can use this to show a link to anyone with this Permission, regardless of specific User Roles. | cms.pages.view                        |
| hidden      | This is an internal field, that hides menu items unless they meet certain requirements. It's not currently supported for custom Admin Menus.                | false                                 |
| key         | This is an internal field for identifying certain menu items. It's not relevant for custom Admin Menus                                                      | cms                                   |

You can insert values for `role_deny`, `role_allow`, and `permission` using the dropdowns in the top right of the editor.

You can reset your menu to the default Siteglide menu using the 'Reset' button in the bottom bar.
