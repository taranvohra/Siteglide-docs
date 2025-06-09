# ℹ️ Data & UI Module Example

In this example we’re going walk through, step by step, how to create a Module with a Custom UI that could either be used as a private module for your agency or shared publicly in the marketplace to deliver turnkey site solutions to your clients and more.

It is recommended that you download our example [Custom UI Demo Module Repository from GitHub](https://github.com/Siteglide/Module_Siteglide_CustomUIDemo) so that you have all of the code and asset files available at each step of this guide and can easily follow along to and have your module end up looking exactly the same.

:::hint{type="info"} If developing a Custom UI then you will have to supply all elements of the Module, including but not limited to tables, GraphQL, data processing etc. :::

## Custom UI

Custom UI modules open up the ability for complete flexibiltiy within Siteglide Admin and allows for truly unique experiences for your customers.

![](../../assets/ezmAWQRErVj2S3TecVHcT_screen-shot-2022-03-18-at-133011.png)

A module with a Custom UI will securely load a page within a frame in Siteglide Admin. This page can be developed in any language that can run on a Siteglide site.

### Setting up your files

A Custom UI Modules will follow the same folder setup as other Modules, except when you come to build the UI itself to display in Siteglide Admin. The UI will be kept in the `private` folder of the module as we do not want it to be discoverable outside of the frame within Siteglide Admin.

Within our `private` folder we can store any files that Siteglide natively supports, such as GraphQL, Liquid, Assets etc. More information about folder structure can be found at [Top Level Folders](create-folder-structure.md#top-level-folders).

### Authentication

To ensure that the Custom UI is only being accessed by logging in users of Siteglide Admin, we require authentication to be added to each page that will be used within the Custom UI. This is stored in the YAML of the pages and is as follows:

```yaml
---
response_headers: >
  {
    "X-Frame-Options": null
  }
authorization_policies:
  - modules/siteglide_system/module_is_in_admin
---
//Page content here
```

The `response_headers` YML allows Siteglide Admin to view the content of the file when it is loaded. The `authorization_policies` YML will run a check to ensure that the user has an active session within Siteglide Admin, if not then it will display an error page.

As well as the YAML, any links within your Custom UI has to include a Liquid tag to apply the authencation string on the link. For example if you are linking from your Custom UI's index page to the add new item page, your link would be as follows:

```liquid
<a href="/add?{% raw %}
{% include "modules/siteglide_system/modules/auth" -%}
{% endraw %}">Add new item</a>

">Add new item</a>

```

This include will create a hash onto the end of the URL that is then used in the above authorization policy to decide whether to show the page. If the include is missing then following the link will throw an error within Siteglide Admin.

You can also control access to certain areas of a page with the `module_is_in_admin` function:

```liquid
{% raw %}
{%- function access_allowed = 'module_is_in_admin' -%}
{%- if access_allowed -%}
    <p>Content to show if loaded via Admin</p>
{%- endif -%}
{% endraw %}
```

### Module Details

Once your module is created, you will need to tell Siteglide Admin to load your Custom UI. You will need to take the slug of the Custom UI's homepage and enter that into your Module Detials within Portal. When editing the details about your module, there is a field called "Custom UI Path", entering in the slug there will change the menu item for your module to then load your Custom UI instead of the default Siteglide module UI. In our example the path for our Custom UI homepage is `module_72/module_iframe/index`
