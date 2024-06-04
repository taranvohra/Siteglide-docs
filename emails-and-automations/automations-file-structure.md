# 🌳 Automations File Structure

Below shows a simplified version of the Folder Structure. It will grow the more automations you add.

We recommend setting up Automations in the Siteglide Admin and then pulling to inspect and modify what you need to.

Individual Email and API call actions can be modified in the notifications folder.

The JSON files which control triggers and which actions to run are stored in the tables folder. Again it's easier to modify these in the Siteglide Admin.

"FIC" stands for "Form Create" - it is a shorthand for the trigger which can be expected to run the code in the file.&#x20;

```
└───marketplace_builder
    ├───notifications
    │   └───email_notifications
    │       └───forms
    │           └───form_1
    │               └───fic
    │                       0.liquid
    │                       1.liquid
    │
    └───views
        └───partials
            └───tables
                └───forms
                        1.liquid
      
```
