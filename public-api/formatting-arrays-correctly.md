Background

When working with [Zapier](https://help.siteglide.com/article/292-zapier-getting-started), adding data to arrays needs some extra JavaScript to convert the data. Zapier calls arrays "Line Items" and formats them like so, `[123,456,789]` whereas Siteglide API expects a JavaScript formatted array such as, `["123","456","789"]`

To convert these two data types, use the screenshots and code below.  In this example we are getting a pre-existing user and their Secure Zones, then adding in a new item.

## Zapier Setup

![Finding an individual user and retrieving their data](./../.gitbook/assets/archbee_uploads/-AMxd0CRDYGkCslIGDgoD_Screen%20Shot%202021-01-07%20at%2021.05.08.png) 


![Pass that data into a "Run Javascript" action and run the following JavaScript](./../.gitbook/assets/archbee_uploads/25cf_DyWZf2jAkaFVBRcj_Screen%20Shot%202021-01-07%20at%2021.04.53.png) 


```javascript
let data = inputData.sz.split(','); //Where sz is the name of the input data you picked above
let array = [];

data.forEach(item => array.push(item));
array.push("178375") //The ID of your secure zone

output = {output: JSON.stringify(array)};
```

![Pass the output of the "Run Javascript" action into the "Update User" action](./../.gitbook/assets/archbee_uploads/z3nHyi_3lNBW4Mbcl5b2n_Screen%20Shot%202021-01-07%20at%2021.10.16.png)

The above javascript code and flow can be used for anywhere that you need to add an item to Line Items within Zapier

