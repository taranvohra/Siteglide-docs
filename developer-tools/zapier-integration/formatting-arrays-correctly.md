# ℹ️ Formatting arrays correctly

## Background

When working with [Zapier](/developer-tools/zapier-integration/README.md), adding data to arrays needs some extra JavaScript to convert the data. Zapier calls arrays "Line Items" and formats them like so, `[123,456,789]` whereas Siteglide API expects a JavaScript formatted array such as, `["123","456","789"]`

To convert these two data types, use the screenshots and code below. In this example we are getting a pre-existing user and their Secure Zones, then adding in a new item.

## Zapier Setup

![Finding an individual user and retrieving their data](<../../.gitbook/assets/archbee\_uploads/-AMxd0CRDYGkCslIGDgoD\_Screen Shot 2021-01-07 at 21.05.08.png>)

![Finding an individual user and retrieving their data](../../.gitbook/assets/archbee\_uploads/-AM)

![Pass that data into a "Run Javascript" action and run the following JavaScript](<../../.gitbook/assets/archbee\_uploads/-AMxd0CRDYGkCslIGDgoD\_Screen Shot 2021-01-07 at 21.05.08.png>)

```javascript
let data = inputData.sz.split(','); //Where sz is the name of the input data you picked above
let array = [];

data.forEach(item => array.push(item));
array.push("178375") //The ID of your secure zone

output = {output: JSON.stringify(array)};
```

![Pass the output of the "Run Javascript" action into the "Update User" action](<../../.gitbook/assets/archbee\_uploads/z3nHyi\_3lNBW4Mbcl5b2n\_Screen Shot 2021-01-07 at 21.10.16.png>)

The above javascript code and flow can be used for anywhere that you need to add an item to Line Items within Zapier
