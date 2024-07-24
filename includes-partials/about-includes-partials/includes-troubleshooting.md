# 🔧 Includes Troubleshooting

Common things to check when experiencing problems with includes:

* [ ] Check that your include's path is correct- this is the most common problem. Check the [reference ](../../includes-reference.md)for details.&#x20;
  * [ ] Have you accidentally included the file extension?
  * [ ] Have you started the path too early? Perhaps starting with "marketplace\_builder" or "views"?
* [ ] Check the syntax is correct, are you using commas ',' to separate parameters passed to the include and colons ':' to separate keys and values?
* [ ] For Siteglide features, generally arrays are passed into variables as a comma-separated string e.g. item\_ids: '1,2,3'- have you passed in as a Liquid array by mistake?
* [ ] If you assign a variable inside a partial with the same name as the partial's filename it can cause a problem. E.g. if you are inside a file called `marketplace_builder/views/partials/order.liquid` and you write the code `{% assign order = 'example' %}` this can cause a bug.

