# 💻 Reference

## Available Fields

In your `item.liquid` file, you can use the following dynamic fields:

* `{{this.id}}` - The Item's unique ID
* `{{this.name}}` - The Item's name
* `{{this.create_date}}` - The date this Item was created. Use Liquid Date Filters to format it.
* `{{this.last_edit_date}}` - The date this Item was last edited. Use Liquid Date Filters to format it.
* `{{this.file_name}}` - The Module automatically works out File Name from the File itself.
* `{{this.file_type}}` - The Module automatically works out File Type by its extension.
* `{{this.url}}` - This will output the temporary secure link. See more details in the section below.
* `{{this.weighting}}` - Optional Field used in sorting
* `{{this.release_date}}` - The date this Item was released. Use Liquid Date Filters to format it.
* `{{this.expiry_date}}` - The date this Item will expire. Use Liquid Date Filters to format it. Note- this is different from expiry see Liquid parameters.
* `{{this.category_array}}` - An array of categories that the Item is assigned to.
* `{{this.Description}}` - A description of the Download
* `{{this.size_in_kb}}` - The file size of the download in Kilobytes
* `{{this.size_in_mb}}` - The file size of the download in Megabytes-
* `{{this.size_in_gb}}` - The file size of the download in Gigabytes
