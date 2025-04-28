---
description: Send form data via email or webhooks
---

# Form

The Form Component is a **powerful form solution** allowing you to send form submissions via your own email server or via a webhook.

### Server Requirements

The Form Component in Elements requires PHP 8.x or newer. **You must ensure all pages with a Form use a .php extension.**

### Available Form Components

The following Components must be placed inside of the "Form Component" wrapper to function correctly.

<table><thead><tr><th width="212">Form Component</th><th>Details</th></tr></thead><tbody><tr><td>Attachment</td><td></td></tr><tr><td>Checkbox</td><td></td></tr><tr><td>Error</td><td></td></tr><tr><td>Input</td><td></td></tr><tr><td>Label</td><td></td></tr><tr><td>Radio</td><td></td></tr><tr><td>Submit</td><td></td></tr><tr><td>Success</td><td></td></tr></tbody></table>

### Email

To recive emails via the Form Component you will need to enter your Email server details. Here’s a breakdown of what each field means and what you’ll need to configure to make it work properly:

<table><thead><tr><th width="212">Settings</th><th>Details</th></tr></thead><tbody><tr><td>Host</td><td>Email host address. e.g. mail.yourdomain.com</td></tr><tr><td>Port</td><td>The port number the email server uses for sending messages.<br>- 587: For TLS encryption (most common) <br>- 465: For SSL encryption.<br>- 25: For non-encrypted emails (not recommended).</td></tr><tr><td>Encryption</td><td>Choose the encryption method required by your email provider. None, TLS, SSL</td></tr><tr><td>Username</td><td>The email address or username for the SMTP account you’re using to send emails. e.g. admin@yourdomain.com.</td></tr><tr><td>Password</td><td>The password for your SMTP account.</td></tr></tbody></table>

### Webhooks

A webhook allows your form submissions to be sent directly to another service, like a database, CRM, or automation tool without needing to check emails or manually process the data. By sending form data to a webhook, you can trigger workflows in [Zapier](https://zapier.com/), [Make](https://www.make.com/en), or [Pipedream](https://pipedream.com), making it easy to do the following (and so much more):

• Add a new lead to Airtable or Google Sheets

• Send a follow-up email through Mailchimp or ConvertKit

• Notify your team in Slack or Discord

• Create support tickets in Zendesk or Trello

There's really no limit to what you can do with the new webhooks feature. Whether you’re building a customer support system, a lead capture form, or a dynamic survey that feeds into a database, webhooks unlock powerful automation and customization that email simply can’t match.

{% hint style="info" %}
**Webhooks and Attachments:** If you are using an attachment in your form, only the first attached file will be sent via the WebHook.
{% endhint %}

### Testing Webhooks Locally

Webhook submissions require a server environment, so once you **publish the page to a server**—either a remote server or a local one—you should find the submission works as expected.

If you want to test everything **locally**, you’ll need to set up a local web server on your Mac. We recommend [ServBay](https://www.servbay.com/) for this.

Here’s a quick guide:

1. **Install ServBay**
2. **Publish your Elements site** to a local folder
3. In ServBay, **create a new site** and point the root directory to your published folder
4. Open the site in your browser through ServBay for full local testing—including Forms and webhooks



