# 🧞 SiteBuilder Live Updates API

## Live Updates - An Introduction <a href="#live-updates-an-introduction" id="live-updates-an-introduction"></a>

### Introduction <a href="#introduction" id="introduction"></a>

The SiteBuilder Live Updates API helps you quickly build interactive, dynamic website layouts for Siteglide which live-update parts of their content when the user interacts with them.

<figure><img src="https://res.cloudinary.com/sitegurus/image/upload/f_auto/v1680276257/modules/module_86/admin/libraries/5/tables/table-1.png" alt=""><figcaption></figcaption></figure>

This allows you to use the convenience of server-side rendering with performance more akin to a JavaScript framework.

### How it works <a href="#how-it-works" id="how-it-works"></a>

When you want the server to live-update Liquid content, you normally need to create a new Page for each specific type of content and write JavaScript to send a GET request to fetch that content and insert it into the Page. This API provides a single ready-built API endpoint Page to make this process quicker. When we describe "adding parameters to the request" in this documentation, we mean adding query parameters to the GET requests' URL.

<figure><img src="https://res.cloudinary.com/sitegurus/image/upload/f_auto/v1684487550/modules/module_86/documentation/Live_updates_API_diagram.drawio_1.png" alt=""><figcaption></figcaption></figure>

See the URL Parameters Section for more details on choosing parameters to modify your content.

### Thinking about Security <a href="#thinking-about-security" id="thinking-about-security"></a>

When using a single page to deliver multiple types of content, how do we prevent malicious users requesting content they should not have access to?

When using the API, you'll get the server to generate a public key which contains encrypted information about the exact Liquid layout you are intending to use and live-update. This includes for example:

* The path of the Liquid Partial
* The WebApp or Module ID
* The user ID which might be used to filter the items based on ownership.

The same server handles the requests and it will only accept valid public keys from which it can extract that same information. That means sensitive parameters which are stored inside the public key cannot be simply modified by a user who does not have direct access to the server.

#### Secure Zones <a href="#secure-zones" id="secure-zones"></a>

PlatformOS cookies and user sessions are preserved by the requests, so secure zones will apply as normal within the Liquid files which are re-rendered. You will need to write code which respects secure zones logic as you normally would.

#### Mutating/ Editing Data <a href="#mutating-editing-data" id="mutating-editing-data"></a>

Note that this API currently uses GET requests only to fetch/read HTML and/or data. While it is possible for the agency developer to write server-side Liquid on the rendered layout which will write to the database, the API does not provide any of its own functionality for writing to the database (if you do need this kind of functionality- see Siteglide's [WebApp](/webapps/go-further-webapps/webapp-front-end-submit-forms-create.md) and [Module](/modules/go-further-modules/front-end-submit-modules.md) Forms). This is a very similar situation to visiting Siteglide pages via the browser.

#### Specialised Use Cases <a href="#specialised-use-cases" id="specialised-use-cases"></a>

Some parameters that we consider non-sensitive normally, like those which might be used to filter data could in some use cases be something you do not wish users to be able to modify. In this case, you can use our [Enforcing Filters](/sitebuilder/using-sitebuilder/live-updates-api/live-updates-example-enforcing-filters.md) Guide to solve this problem.

See the `collection` and `creator_id` [URL parameters](/sitebuilder/using-sitebuilder/live-updates-api/live-updates-reference.md#get-url-parameters) for security considerations regarding JSON data and filtering items by their owner respectively.