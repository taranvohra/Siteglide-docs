Company Information can be used to store key contact and branding information for your client while making it easy for them to manage. You can then use the liquid tags below to output this globally stored information anywhere on the site.

When your client needs to update some key information about their company, they need only do it once and it will update everywhere you have used these tags across their site.

*   `{{context.exports.company_information.properties.logo | asset_url}}`

*   `{{context.exports.company_information.properties.logo_white | asset_url}}`

*   `{{context.exports.company_information.properties.vat_number}}`

*   `{{context.exports.company_information.properties.company_name}}`

*   `{{context.exports.company_information.properties.phone_number}}`

*   `{{context.exports.company_information.properties.email_address}}`

*   `{{context.exports.company_information.properties.address_line_1}}`

*   `{{context.exports.company_information.properties.address_line_2}}`

*   `{{context.exports.company_information.properties.twitter_account}}`

*   `{{context.exports.company_information.properties.facebook_account}}`

*   `{{context.exports.company_information.properties.linkedin_account}}`

*   `{{context.exports.company_information.properties.instagram_account}}`

*   `{{context.exports.company_information.properties.active_campaign_id}}`

*   `{{context.exports.company_information.properties.google_analytics_id}}`

*   `{{context.exports.company_information.properties.google_plus_account}}`

*   `{{context.exports.company_information.properties.google_analytics_view_id}}`

*   `{{context.exports.company_information.properties.google_analytics_site_verification}}`

Social Field Example:

```liquid
{% raw %}
test2
{% comment %}Test{% endcomment %}
{% if context.exports.company_information.properties.twitter_account == blank -%}
  <a 
    title="Twitter"
    rel="nofollow"
    href="https://twitter.com/{{context.exports.company_information.properties.twitter_account}}"
    target="_blank"
  >
    <i class="fab fa-2x fa-twitter"></i>
  </a>
{% endif -%}
{% endraw %}
```

