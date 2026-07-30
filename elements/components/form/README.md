---
description: Build forms that submit to email or a webhook
---

# Form

The Form component is the wrapper for fields, attachments, feedback, and submission controls. It validates its fields, then sends the submission through an SMTP email account or to a webhook.

{% hint style="danger" %}
Forms require a published server with **PHP 8.1 or newer**. They do not submit in the normal local preview.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=FlAvQC5neyA" %}

### How to Build a Form

You’ll find Form and its related components under **Forms** in the Components list.

1. Drag **Form** onto the page.
2. Add Input, Date Picker, Select, Checkbox, Radio, Attachment, and Label components inside the Form.
3. Add a **Submit** component inside the Form.
4. Drag a clickable component—normally a **Button**—into the Submit component’s drop zone.
5. Add Success and Error components, then place the feedback content you want to show inside them.
6. Choose Email or Webhook delivery and enter the required connection details.
7. Configure spam protection if needed.
8. Publish to a PHP-enabled server and test a complete submission.

{% hint style="warning" %}
The **Submit component does not display a button and cannot be clicked on its own**. It supplies submission behaviour to its drop zone. Add a Button, Image, or another clearly clickable component inside Submit so visitors have something to click.
{% endhint %}

### Form Components

All form controls must be inside the Form wrapper.

| Component | Purpose |
| --- | --- |
| [Attachment](attachment.md) | Accepts one or more uploaded files. |
| [Checkbox](checkbox.md) | Collects zero, one, or several choices. |
| [Date Picker](date-picker.md) | Collects a date and optional time. |
| [Error](error.md) | Displays custom content when form submission fails. |
| [Input](input.md) | Collects text, email, numbers, passwords, search terms, telephone numbers, URLs, or multi-line text. |
| [Label](label.md) | Associates visible descriptive text with a field. |
| [Radio](radio.md) | Lets visitors choose one option from a group. |
| [Select](select.md) | Presents a drop-down list of options. |
| [Submit](submit.md) | Turns a child Button or similar component into the form’s submission control. |
| [Success](success.md) | Displays custom content after a successful submission. |

### Compatibility Checklist

Before publishing:

* [ ] The Form and every field are on a page published through PHP.
* [ ] The server runs PHP 8.1 or newer.
* [ ] Every form field is nested inside the Form wrapper.
* [ ] Every field has a short, unique Name containing letters, numbers, hyphens, or underscores.
* [ ] The visitor email field is named exactly `email` when it should become the Reply-To address.
* [ ] Submit contains a Button or another visible, clickable child component.
* [ ] Success and Error contain useful feedback.
* [ ] Multiple is enabled when Attachment should accept several files.
* [ ] The SMTP or webhook configuration has been tested on the published server.

### Component Settings

#### Settings

**Type** is not responsive and defaults to Email.

* **Email** — Sends through the configured SMTP account.
* **Webhook** — Sends to the URL entered under Webhook URL.

Webhook reveals **Webhook URL**, which is blank until configured.

#### Email Authentication

Email delivery reveals:

* **Host** — SMTP hostname. The placeholder is `smtp.example.com`.
* **Port** — Defaults to `587`.
* **Encryption** — None, TLS, or SSL. TLS is the default.
* **Username** — SMTP account username, commonly the full email address.
* **Password** — SMTP account password or provider-specific app password.

Replace every example value before publishing.

Email delivery is powered by [PHPMailer](https://github.com/PHPMailer/PHPMailer).

{% hint style="info" %}
We recommend a webhook when you do not need direct SMTP delivery. Webhook services often provide clearer logs, retries, and integrations with databases, spreadsheets, CRMs, and automation tools.
{% endhint %}

#### Email Settings

* **From Name** — Name shown as the sender.
* **From Address** — Sender address. It should normally match the SMTP account and its domain.
* **Subject** — Defaults to “New Form Submission”.
* **To Name** — Recipient name.
* **To Address** — Address that receives the submission.

Use an authenticated address as From. Do not use the visitor’s address as From; use the `email` field for Reply-To.

#### Email Template

**Template Style** defaults to Default. Options are Default, Table, Simple, and Modern.

**Email Title** defaults to “New Form Submission”.

**Email Footer** is blank by default.

#### SSL Configuration

* **Verify Peer** — Enabled by default.
* **Verify Peer Name** — Enabled by default.
* **Allow Self-Signed** — Disabled by default.

{% hint style="warning" %}
Keep peer verification enabled and self-signed certificates disabled for production. Change these only when your hosting provider has confirmed that the SMTP server requires it and you understand the security trade-off.
{% endhint %}

#### Spam Protection

**Service** is not responsive and defaults to None.

* **None**
* **reCAPTCHA**
* **Turnstile**
* **hCaptcha**
* **Honey Pot**

Honey Pot adds hidden fields that help identify automated submissions and needs no external keys.

reCAPTCHA, Turnstile, and hCaptcha reveal:

* **Style** — Visible or Invisible. Invisible is the default.
* **Site Key**
* **Secret Key**

Obtain the keys from the selected provider and make sure they are authorised for the published domain.

#### Errors

Invalid fields default to Red 500 Background and Border colours. Their validation message defaults to Red 50 text.

These colours style invalid controls. Add the [Error component](error.md) when you also want a custom form-level error message.

#### Success

**On Success** is not responsive and defaults to Success Content.

* **Success Content** — Shows the content inside a Success component.
* **Redirect** — Reveals Link and sends the visitor to that destination.

**Reset** is enabled by default and clears the form fields after a successful submission.

### Reply-To Address

Name the visitor’s email Input exactly:

```text
email
```

The name is case-sensitive. Keep the authenticated account in From Address; the submitted `email` value becomes Reply-To.

### Webhooks

A webhook sends the submission to another service, such as a database, CRM, automation tool, or server endpoint. Services such as [Zapier](https://zapier.com/), [Make](https://www.make.com/en), and [Pipedream](https://pipedream.com) can use it to:

* Add leads to a database or spreadsheet.
* Send follow-up email.
* Notify a team.
* Create tickets or tasks.

Webhook attachments are limited to the first attached file. Email delivery supports multiple files when Attachment has Multiple enabled.

### PHP Server Check

Append `?apicheck` to the published URL of a page containing the Form:

```text
https://example.com/contact/?apicheck
```

The page reports whether the Forms API is reachable and shows the server’s PHP version.

### Testing Webhooks Locally

The normal Elements preview is not a PHP server. To test against a local server:

1. Install a local PHP environment such as [ServBay](https://www.servbay.com/).
2. Publish the Elements site to a local folder.
3. Point the local server at that folder.
4. Open the server URL in a browser and submit the form.

{% embed url="https://youtu.be/pR26NPw0Ip8?si=4aJyKiEJp5ntrPiD" %}

### Troubleshooting

#### The form does nothing when clicked

Confirm that a Button or other clickable component is inside Submit, and that Submit itself is inside Form. The empty Submit wrapper cannot be clicked.

#### The form works visually but sends nothing

Publish to a PHP-enabled server, run the PHP Server Check, and confirm that the server supports outbound SMTP or can reach the webhook URL.

#### SMTP authentication fails

Check Host, Port, Encryption, Username, and Password with the email provider. Remove accidental spaces. Make sure From Address is permitted by the authenticated account and that the SMTP certificate matches the Host.

Providers such as Fastmail may require an app password. See [Using Fastmail](using-fastmail.md).

If the settings look correct but delivery still fails, search the [Elements Forum](https://forums.realmacsoftware.com/) for advice about your email provider or hosting setup.

#### Required fields are not accepted

Make sure each field has a valid Name and that Checkbox, Radio, and Select options have non-empty values. Test the published form using the same path a visitor will follow.

#### Finding form logs

The published Forms API stores logs inside its `api/logs` directory. Files use a form-specific name and date; check the newest file created after the failed test.

### Accessibility

Use a visible Label for each field, preserve keyboard focus outlines, identify required fields in visible text, and make Error and Success messages understandable without relying on colour alone.

{% include "../../../.gitbook/includes/common-controls.md" %}
