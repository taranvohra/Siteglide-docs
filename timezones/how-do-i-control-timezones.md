## Siteglide Admin

Timezone is defined by the user's system setting.

If the user is in New York, all dates/times in Admin will show in their local New York time.
However, any updates to data (release\_date, custom dates, etc.) will be stored in the database as UTC no matter what.

This is possible because Admin runs off JavaScript, which is able to access the user's system settings and show them date/time in their local time.

***

## Front-end - Current, and forever default

Timezone is UTC always.

If the user is in New York, all dates/times front-end will still show in UTC.

This is because front-end runs off Liquid, which does not have access to the requesting user's system settings, so just runs off the default (UTC).

***

## Front-end - Custom - Hardcoded Timezone


Developers could hardcode a Timezone in their date formatting scripts.
For example, `{{this.release_date | to_time: "America/New_York"}}`

[Docs - to\_time](https://documentation.platformos.com/api-reference/liquid/platformos-filters#to_time)

[Docs - timezone names](https://docspring.com/docs/html_templates/liquid_timezones.html)&#x20;

***

## Front-end - Custom - User Settings

Similar to 'Hardcoded Timezone', but instead of hardcoded Timezone, developers could set up a Custom Field in their CRM for Timezone.

Then when that user logs in it will format all dates to that user's selected Timezone.

***


