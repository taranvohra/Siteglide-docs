# ℹ️ Email Automations and Email Templates with Siteglide CLI

We recommend for now creating Automations in the Siteglide Admin so that the triggers are correctly attached to the Form.

After this, you can pull with Siteglide CLI and modify the files, for convenience, should you wish.

Each automation Email body has an important section of YAML settings at the top. You can make any of these Liquid multiline if you want to use Liquid logic to determine them dynamically.

```liquid
{% raw %}
---
bcc: ''
cc: ''
from: Siteglide Demo Site Template <no-reply@siteglide.com>
layout: templates/2
name: form_1_autoresponder
reply_to: Siteglide Demo Site Template <no-reply@siteglide.com>
subject: We can't wait to Deliver
to: "{{ form.properties.email }}"
trigger_condition: 'true'
---
<!-- Email body -->
{% endraw %}
```

* Use to, bcc, cc, reply\_to and from for setting which email addresses should be used for each of these.
* Subject does what you'd expect
* Layout sets which [email-templates.md](email-templates.md "mention") you want to use
* Trigger condition of `true` will allow the Email to send, `false` will disable it.

### Multiline example:

\
Check how the `to` line is made multiline to allow Liquid Logic- the two spaces indent is important. When you pull, you may find the syntax changes to a default.

```liquid
{% raw %}
---
bcc: ''
cc: ''
from: Siteglide Demo Site Template <no-reply@siteglide.com>
layout: templates/2
name: form_1_workflow
reply_to: Siteglide Demo Site Template <no-reply@siteglide.com>
subject: We can't wait to Deliver
to: >
  {% if form.properties.form_field_1_1 == "office_a" %}office_a@office.com{% else %}office_b@office.com{% endif %}
trigger_condition: 'true'
---
{% endraw %}
```

## Email Templates

When using CLI, make sure email templates are given the file\_type, id and type metadata settings:

```liquid
{% raw %}
---
metadata:
  id: 2
  type: email
  file_type: template
  is_default: false
---
{% endraw %}
```

The ID must match the file name and be unique in your codebase.
