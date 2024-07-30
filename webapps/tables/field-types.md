# Field Types available

A list of field types available on Siteglide and the corresponding platformOS data type applicable to them

| Name                     | Siteglide Type    | platformOS Type |
| ------------------------ | ----------------- | --------------- |
| Text (String)            | input\_text       | string          |
| Text (Multiline)         | textarea          | string          |
| Checkbox                 | input\_checkbox   | array           |
| Radio Button             | input\_radio      | string          |
| Dropdown (Single Item)   | select            | string          |
| Dropdown (Multi Item)    | select\_multi     | array           |
| Datasource (Single Item) | datasource&#xD;   | integer         |
| Datasource (Multi Item)  | datasource\_multi | array           |
| Image (Single)           | image&#xD;        | string          |
| Image (Array)            | image\_array      | array           |
| File                     | file&#xD;         | string          |
| Folder                   | folder            | string          |
| Date                     | date&#xD;         | integer         |
| Number (Integer)         | number\_integer   | integer         |
| Number (Float)           | number\_float     | float           |
| Boolean                  | boolean           | boolean         |
| Custom Array             | array\_custom     | array           |

# Where are these field types available to use as Custom Fields?

*   **Modules** - All field types

*   **WebApps** - All field types

*   **eCommerce Products** - All field types

*   **CRM Users** - All field types

*   **Forms** - All field types *except Custom Array*

*   **Custom Field Sets** - All field types *except Custom Array*

# Form Configuration metadata options

All field types have the following metadata options:

| Name     | Type    | Notes                                                                                             |
| -------- | ------- | ------------------------------------------------------------------------------------------------- |
| name     | string  | The field name to be shown in Siteglide Admin UI                                                  |
| type     | string  | The field type in the 'Siteglide Type' column above                                               |
| live     | boolean | Determines whether or not the field is shown or used anywhere                                     |
| hidden   | boolean | Determines whether or not the field is shown in Siteglide Admin UI                                |
| order    | integer | The position the field is shown in Siteglide Admin UI and Import CSVs                             |
| editable | boolean | Determines whether you can edit this metadata in the Siteglide Admin UI builder views             |
| required | boolean | Determines whether it is required to fill in this field in Siteglide Admin UI and front-end forms | 


Some other metadata options are available to specific field types:

| Name           | Type    | Available for                                                 | Notes                                                                                                                                   |
| -------------- | ------- | ------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| rich\_text     | boolean | textarea                                                      | Determines whether the Rich Text editor appears in Siteglide Admin UI for this field                                                    |
| options        | string  | input\_checkbox&#xA;input\_radio&#xA;select&#xA;select\_multi | A comma separated string of options to be displayed for this field in Siteglide Admin UI                                                |
| datasource\_id | string  | datasource&#xA;datasource\_multi                              | The ID of the model you want options to show from for this field in Siteglide Admin UI. This includes the type, for example `webapp_1`. |
| num\_min       | string  | number\_integer&#xA;number\_float                             | The minimum value this number field will allow the user to select.                                                                      |
| num\_max       | string  | number\_integer&#xA;number\_float                             | The maximum value this number field will allow the user to select.                                                                      |
| num\_step      | string  | number\_integer&#xA;number\_float                             | The amount the number will change by using the number scroller in Siteglide Admin UI.                                                   |
| num\_precision | string  | number\_integer&#xA;number\_float                             | The amount of decimal places shown in Siteglide Admin UI.                                                                               | 

 

 


