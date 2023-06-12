This article shows a different use-case for the skills you've already learned- using an XHR (sometimes called Ajax) request to run a query.

# Introduction

So far, we've written GraphQL queries which run on Page Load. This is powerful, but wouldn't it be even more useful if you could fetch data after Page load when a User interacts with a Site- e.g. changing page on a list without refreshing the Page? Using XHR (sometimes called Ajax) requests, you can run GraphQL at any time.&#x20;

![](https://downloads.intercomcdn.com/i/o/236017911/05ef09fa35ae1e4949279531/image.png)

This approach can take a little bit of time to set up, but can allow you to create much faster interactive experiences for your Users and opens up a huge range of possible solutions you can build.

We cannot document every way in which you can build this kind of Page, but we will show you the basics and let your imagination do the rest! If you need additional support on this topic beyond the scope of what is documented here, we recommend you speak to one of our [Experts](https://www.siteglide.com/partners) or browse the resources we link to at the end of the Article.&#x20;

# Glossary

*   An API - (Application Program Interface) is a form of communication between two services on the internet. Communication takes place between 2 or more endpoints.

*   An endpoint in its simplest form is a URL which allows an API access to a server or application. On Siteglide, we provide you with API endpoints we've built with our [public API](https://help.siteglide.com/collection/21-public-api-integrations), but now you've learned GraphQL, you also have the ability to build your own endpoints when you need them.

*   A method defines the role of the API + Endpoint e.g. a GET method is for "getting" or "fetching" data.

*   JSON (JavaScript Object Notation) is a common file format for exchanging data which is efficient and human-readable. We'll use it in some of our examples. (It's also the default format in which GraphQL results are outputted on the Page.)

# Steps for Building your First Liquid Endpoint Page powered by GraphQL

## Step 1) Create a Page to serve as an Endpoint

![](https://downloads.intercomcdn.com/i/o/235725952/1d4d8bea5fee6e5efd522102/image.png)

The first step is to create a Page on the Siteglide Admin which will become your API endpoint.&#x20;

The slug you choose will be the URL via which you'll eventually access the data. It's worth naming the Page and writing a slug which reflect the fact that this Page is not a public-facing Page and should not be editable by Clients.&#x20;
e.g.  `/api/webapp_1`

## Step 2) Use CLI to apply advanced settings to the Liquid Page

In this step, we'll be changing the settings of the Page in CLI, as there are available settings here that are not yet editable from Admin. You can learn more about pages in platformOS here: <https://documentation.platformos.com/developer-guide/pages/pages#content> and more about the [Siteglide-CLI here](https://developers.siteglide.com/introducing-siteglide-cli).

Using the Siteglide-CLI, pull down your Site's files to your machine and open them up in a Code Editor of your choice. Set up Siteglide-CLI sync so that changes you make will be pushed to the Site.

![](https://downloads.intercomcdn.com/i/o/235728435/228f0d8dafb3db030ac99c47/pullandsync.png)

Open up the Page you've created in a Code Editor of your choice.&#x20;

We'll be editing the yaml configuration at the top of the page. In my example, you can see the yaml settings between the triple dashes --- It's important when configuring yaml to use exactly 2 spaces instead of tabs for indenting. Your siteglide-cli sync command will alert you to any validation errors.&#x20;

```yaml
---
layout: templates/blank_page
max_deep_level: 2
metadata:
  name: API WebApp 1 GET endpoint
  enabled: true
  file_type: page
  last_edit: 1597241196376
redirect_to: ''
redirect_url: ''
---
```

### 2) a) Method

So far we've only learned to write GraphQL queries, so your endpoint will be handling GET requests. Set the method property of your page to get:

`method: get`

### 2) b) Format

Optionally, you can choose to change the format of your Page.&#x20;
If you like, instead of HTML, you can make your Page a different format, like JSON.&#x20;

`format: json`

Note that if you set your Page to a different format now, you'll need to append the URL with the extension later. e.g. a Page with the slug `my-slug` and format JSON can be accessed at the URL `/my-slug.json`.

### 2) c) Remove the Page Template

As your endpoint Page will not be accessed by either humans or search-engine bots, it's much better to remove the Page Template, allowing you to only return the data you need.&#x20;

`layout: ""`

### 2 d) Remove HTML

Unless you're using the HTML format from 2) b), you will need to remove any `&nbsp;` tags automatically added to the Page.

### 2) e) Remove from search engine results

Unlike the other steps, this is not a yaml property on the Page. However, it's included here as a quick sensible step you can take.&#x20;

You may wish to specify in your `robots.txt` file that pages with this URL should be ignored by search engines.&#x20;

### 2) f) Check yaml&#x20;

&#x20;My example looks like this:

```yaml
---
layout: ""
max_deep_level: 2
metadata:
  name: API WebApp 1 GET endpoint
  enabled: true
  file_type: page
  last_edit: 1597241196376
redirect_to: ''
redirect_url: ''
method: get
format: json
---
```

## Step 3) Add a GraphQL query with variables&#x20;

Add a query of your choice using the Liquid `graphql` tag from [tutorial 5](https://developers.siteglide.com/tutorial-5-using-liquid-to-run-graphql-queries-on-your-site) and variables from [tutorial 6.](https://developers.siteglide.com/tutorial-6-variables)

In this example, I'll use the following query to fetch data from webapp\_1 and change page with the `page` variable:

```graphql
query fetch_webapp_1_by_page($page: Int!, $per_page: Int!) {
  models(
    filter: {
      model_schema_name: { value: "webapp_1" }
    }
    page: $page
    per_page: $per_page
  ) {
    results {
      id
      properties
    }
  }
} 
```

I'll use the following Liquid to run this query when the endpoint Page is accessed:
`{%- graphql fetch_webapp_1_by_page = "fetch_webapp_1_by_page"-%}`

Note- I'll be using - before and after my closing Liquid tags to remove unnecessary whitespace from the results- this is optional.&#x20;

## Step 4) Add Liquid logic to handle incoming URL parameters

&#x20;In the example, we'll pass inputs into the endpoint Page using query parameters on the end of the URL, for example, I already have the URL for accessing the endpoint Page:
`/api/webapp-1.json`

:::hint{type="warning"}
## Remember

The ".json" extension should be replaced with the "format" you chose in step 2.&#x20;
:::

I'll be storing the page I want to request from the endpoint in query parameters like so:
`/api/webapp-1.json?page=2&per_page=1`

You can now use `context.params`\`to read the URL on the endpoint Page and dynamically access each query parameter. I'll store each in a variable before I feed these into the query, in case there is any type coercion to carry out first.

```html
{%- assign page = context.params.page -%}
{%- assign per_page = context.params.per_page -%}
```

## Step 5) Use Liquid to feed variables into the Query (and make sure they are the correct type)

Accessing these values via the above method tends to set them as String values in the variable. For this example we'll need to change the type to integer- as that's what the query expects. You can refresh your knowledge on changing the type of variable in Liquid in [tutorial 6.](https://developers.siteglide.com/tutorial-6-variables)

```html
{%- assign page = context.params.page | add: 0 -%}
{%- assign per_page = context.params.per_page | add: 0 -%}
```

We can then add them to the query.&#x20;

```html
{%- graphql fetch_webapp_1_by_page = "fetch_webapp_1_by_page",
  page: page,
  per_page: per_page
-%}
```

If the query expects variables to be Strings you can actually add them straight to the query without assigning as variables first:

```html
{%- graphql fetch_webapp_1_by_page = "fetch_webapp_1_by_page",
  page: context.params.page,
  per_page: context.params.per_page
-%}
```

## Step 6) Output results on the Endpoint Page - These will be the response body

Results are accessible via the variable name you defined in the `graphql` tag, but at this point we can decide on the format in which we'll display them.

### Option 6) a) HTML format

If you decided in step 2 that you didn't want to change the Page format, you should now build the required HTML structure you'd like to send back (this would probably be inserted as it is into a Page via JavaScript).

```html
{%- graphql fetch_webapp_1_by_page = "fetch_webapp_1_by_page",
  page: context.params.page,
  per_page: context.params.per_page
-%}

<div class="row">
  {%- for item in fetch_webapp_1_by_page.models.results -%}
    <div class="col">
      <h2>{{item.properties.name}}</h2>
    </div>
  {%- endfor -%}
</div>
```

### Option 6) b) JSON format

If you decided in step 2 to change the format of the Page, you'll need to use Liquid to output the content in this format.&#x20;

As GraphQL already outputs in JSON format, this is easy:

```html
{%- graphql fetch_webapp_1_by_page = "fetch_webapp_1_by_page",
  page: context.params.page,
  per_page: context.params.per_page
-%}

{{fetch_webapp_1_by_page}}
```

### Option 6) c) CSV format

For something like CSV, you'll need to use logic to output the data in the correct format -this is just an example and you may need to alter it for your use-case.&#x20;

We use `{%` rather than `{%-` in this example, because we want to preserve new lines to make sure each row of the CSV displays correctly.&#x20;

```html
{%- graphql fetch_webapp_1_by_page = "fetch_webapp_1_by_page",
  page: page,
  per_page: per_page
-%}
Name,ID,Description
{% for item in fetch_webapp_1_by_page.models.results %}{{item.properties.name}},{{item.id}},
{{item.properties.webapp_field_1_1}}
{% endfor %}
```

## Step 7) Test the endpoint Page&#x20;

In your browser, visit the endpoint Page URL and see if the data displays as expected. Test changing the query parameters to see it change the returned data.

A successful JSON endpoint will return valid JSON in the body, as in the example here (other formats should also be checked for valid formats).&#x20;

```json
{"models":{"results":[
    {"id":"220","properties":
    {"name":"We know guitar music"
     "slug":"we-know-guitar-music"
     "enabled":true
     "og_desc":null
     "og_type":null
     "og_title":null
     "meta_desc":null
     "weighting":null
     "meta_title":null
     "expiry_date":2145916800
     "release_date":1570797009
     "twitter_type":null
     "category_array":[]
     "webapp_field_1_1":"images/about/about-5.jpg"
     "webapp_field_1_2":"Man playing guitar"
     "webapp_field_1_3":"We know guitar music"
     "webapp_field_1_4":"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."}}]}}

```

Changing the URL parameters should allow you to return different responses:

![](https://downloads.intercomcdn.com/i/o/235744297/f001a8c7d5fbdb302d79adb8/image.png)

Common issues:

*   Your URL should include the relevant file extension e.g. `.json` for json format, `.csv` for CSV format. If you are using `HTML` format, no extension is needed. Below is an example of a 404 response from using the incorrect extension:

![](https://downloads.intercomcdn.com/i/o/235732298/b86fe18d0bb36978ca084b14/image.png)

*   Your URL should contain any query parameters you need for your query. E.g. in my example, `page` and `per_page` are mandatory. Below is an invalid response body resulting from missing URL parameters:

![](https://downloads.intercomcdn.com/i/o/235731724/dbc7b7cd91a0234b6efeb161/image.png)

Congratulations! You've built a working GET endpoint using GraphQL and Liquid!

The last two optional steps will expand upon your options for securing the Endpoint and using the data available.&#x20;

## Step 8) Optional - Security and Authorisation

Is your data sensitive and you want only logged in Users to access it?&#x20;
Is your data public and it doesn't need an additional authorisation step?&#x20;

This step shows you some different ways to make sure your data is secure, but you can skip it if your data is not sensitive or private.&#x20;

### Option 8) a) Using Secure Zones

Adding a Secure Zone to your endpoint Page is a simple way to protect it from Users and bots who should not be accessing it.&#x20;

A failed access will still generate a successful 2xx response code, because it will succeed in returning HTML body (the 404 message that displays to Users). This is only a problem if you're not using HTML format for your endpoint as it will cause any JavaScript which relies on parsing JSON to fail like so:

![](https://downloads.intercomcdn.com/i/o/236001797/0b94fcfa67f25f060e9bcc39/image.png)

In step 9, you'll need to find a way to adapt your JavaScript logic to handle this kind of error which does not rely on the response code, but instead checks the response for the HTML tag `<h1>401 - Unauthorised</h1>`. See step 9) a) i) and 9) a) ii) for examples of this logic.&#x20;

### Option 8) b) Using Authorization Policies

You can use Siteglide-CLI and platformOS to build an authorization policy that checks the request either comes from a trusted Site or from a trusted User. The benefit of this is that it allows you to return HTTP response codes.&#x20;

&#x20;As this is custom platformOS code, it won't be covered by our support. Learn more about authorization policies on the platformOS docs:  <https://documentation.platformos.com/developer-guide/authorization-policy/authorization-policy>

## Authorization Policy tips

These tips are intended as inspiration and do not constitute complete examples. They do not require sending a query parameter over in your URL, making them easier to keep secure.&#x20;

*   If the User has been logged in (to any Secure Zone), you can check this on the Endpoint Page Authorization policy.

```html
{%- if context.current_user.id -%}
  true
{%- endif -%}
```

*   To check that the request comes from an authorized Page/ Site, you can check this with context:

```html
{%- if context.headers.HTTP_REFERER contains "expected-URL" -%}
  true
{%- endif -%}
```

## Step 9) Optional - Get the Data and use it

On any of your other Pages, you can now send requests to your new endpoint and fetch data. For this you could use JavaScript.

*The JavaScript examples provided here are intended for inspiration only. Unfortunately, we cannot advise you on how to adapt these to suit individual projects. See the links at the bottom of this Article for more resources you can use to help plan and develop projects of this kind.*&#x20;

### Example 9) a) i) Logging Json Responses

This basic example will request data from the example earlier and console log the response.&#x20;

The if statement logic checks if a 2xx response code is received (meaning any authorization policies have passed) and that there is no HTML tag containing a 401 code from a Secure Zone check failure. See Step 8) for more details.&#x20;

```html
<script>
  var xReq = new XMLHttpRequest();
  xReq.onload = function () {
    const checkForSecureZone = /401 - Unauthorised/g;
    if (xReq.status >= 200 && xReq.status < 300 && xReq.response.search(checkForSecureZone) == -1 ) {   
      console.log(JSON.parse(xReq.responseText));
    } else {
      console.log('error', xReq.responseText);
    }
  };
  xReq.open('GET', '/api/webapp-1.json?page=1&per_page=1');
  xReq.send();
</script>
```

### Example 9) a) ii) Parsing JSON and manipulating the DOM

In this expanded example, we'll fetch the data and then append it to the HTML DOM.

**Add HTML and JavaScript**

*   An event listener targets the Form and watches for a click event

*   When the Form is submitted, the event triggers the function "getWebappOne".&#x20;

*   The if statement logic checks if a 2xx response code is received (meaning any authorization policies have passed) and that there is no HTML tag containing a 401 code from a Secure Zone check failure. See Step 8) for more details.&#x20;

*   The function requests the data from our new endpoint.&#x20;

*   It then loops over the Items and appends each WebApp Name to the HTML DOM.

:::codeblocktabs
```html
<section class="form form-01">
  <div class="container">
    <form>
      <h2>Get WebApp Names</h2>
      <div class="input-group">
        <label for="page">Page</label>
        <input id="page" type="number" step="1">
      </div>
      <div class="input-group">
        <label for="per_page">Per Page</label>
        <input id="per_page" type="number" step="1">
      </div>
      <button id="submit" class="btn btn-primary">Get WebApp 1</button>
    </form>
  </div>
</section>
<section class="form form-01">
  <div class="container">
    <h2>List of WebApps</h2>
    <div class="row" id="output"></div>
  </div>
</section>
```

```javascript
<script>
  var page = document.querySelector('#page');
  var per_page = document.querySelector("#per_page");
  var submit = document.querySelector("#submit");
  var output = document.querySelector("#output");
  
  function getWebappOne() {
    event.preventDefault();
    var xReq = new XMLHttpRequest();
    xReq.onload = function () {
      const checkForSecureZone = /401 - Unauthorised/g;
      if (xReq.status >= 200 && xReq.status < 300 && xReq.response.search(checkForSecureZone) == -1 ) {
        output.innerHTML = "";
        var jsonParsed = JSON.parse(xReq.response).models.results;
        for(i=0;i<jsonParsed.length;i++) {
          console.log(jsonParsed[i].properties.name)
          output.insertAdjacentHTML('beforeend', '<div class="col">'+jsonParsed[i].properties.name+'</div>');
        }
      } else {
        console.log('error', xReq.responseText);
      }
    }
    xReq.open('GET', '/api/webapp-1.json?page='+page.value+'&per_page='+per_page.value);
    xReq.send();
  };
  
  submit.addEventListener('click', getWebappOne);
  
</script>
```
:::

### Example 9) b) Requesting Data From an HTML Page

&#x20;In the previous two examples, we've used an endpoint with a JSON format endpoint.

You may find it easier to build HTML on the endpoint and when it arrives in the destination Page, output it as it is.&#x20;

**Build HTML on the Endpoint Page**

```html
{%- graphql fetch_webapp_1_by_page = "fetch_webapp_1_by_page",
  page: page,
  per_page: per_page
-%}
<div class="row"> 
  {% for this in fetch_webapp_1_by_page.models.results %}
    <div class="col-4">
       <h3>{{this.properties.name}}</h3>
    </div>
  {% endfor %}
</div>
```

**Fetch HTML on the Front End Page**

```html
<div class="webapp_1">
</div>

<script>
  var xReq = new XMLHttpRequest();
  xReq.onload = function () {
    if (xReq.status >= 200 && xReq.status < 300) {
      document.querySelector(".webapp_1").innerHTML = "";
      document.querySelector(".webapp_1").insertAdjacentHTML('beforeend', xReq.responseText);
    } else {
      console.log(xReq.responseText);
    }
  };
  xReq.open('GET', '/api/webapp-1?page=1&per_page=1');
  xReq.send();
</script>
```

# A Footnote

Your Liquid endpoint Page will be acting as an extra Layer between your request and platformOS' own GraphQL endpoint. This extra layer is important because it allows you to run your own logic and security checks, before pOS deliver the data.&#x20;

# Related Articles

*   The [Siteglide Support Policy](https://help.siteglide.com/article/62-siteglide-support-policy) explains how you can get support with planning projects and writing custom code.&#x20;

*   MDN have comprehensive documentation on the XML HTTP Request and how to use it in your Front End JavaScript Code: <https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest>

*   Those developers who prefer to use jQuery when writing JavaScript can read more about Ajax Requests here: <https://api.jquery.com/jquery.ajax/>&#x20;

*   platformOS's documentation on Pages includes lots of information about setting up Pages using the yaml configuration: <https://documentation.platformos.com/developer-guide/pages/pages>

