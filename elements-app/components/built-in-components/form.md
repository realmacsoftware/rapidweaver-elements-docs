---
description: Send form data via email or webhooks
---

# Form

The Form Component is a flexible and powerful solution for sending form submissions either to your own email server or via a webhook.

### Server Requirements

The Form Component in Elements **requires PHP 8.1 or newer**.

#### PHP Server Check&#x20;

We recommend PHP 8.4 or later for best performance, but the minimum supported version is 8.1.

To check which PHP version your server is using, simply append `?apicheck` to the URL of any page containing a Form. For example:

`my-website.com/contact/?apicheck`&#x20;

### ✅ Form Compatibility & Gotchas Checklist

Before going live with your form, make sure you’ve covered the following essentials. These common issues can prevent form submissions from working correctly, so it’s worth double-checking everything below:

* [ ] **Forms must be published to a live server.** They won’t function when previewed locally.
* [ ] **Your web server must be running PHP 8.1 or newer.** We recommend PHP 8.4 or later where possible.
* [ ] **Sending multiple attachments?** Be sure to enable the “**multiple**” toggle in the Attachment Component settings.
* [ ] **Using the reply-to feature?** The field name for your email input must be exactly email (all lowercase) for Elements to set the reply-to address properly.
* [ ] **Avoid special characters in field names.** Stick to letters, numbers, and hyphens. Avoid spaces, symbols, or punctuation in form field names as they may not be parsed correctly on the server.
* [ ] **Use the Error and Success components.** These components are optional. However, without them, users won’t see feedback after submitting the form. Include both for a complete user experience.

### Form Components

To function correctly, the following Components must be placed inside a Form Component wrapper.

<table><thead><tr><th width="212">Form Component</th><th>Details</th></tr></thead><tbody><tr><td>Attachment</td><td>Allows users to attach files to a form submission. You can limit attachments by file type or size. Multiple files are supported when sending forms via email, though Webhooks are limited to a single file.</td></tr><tr><td>Checkbox</td><td>Collects one or more yes/no values. Commonly used for terms and conditions, opt-ins, or preferences. Often paired with a Label for clarity and accessibility.</td></tr><tr><td>Error</td><td>Displays an error message when the form fails to submit. Useful for alerting users to missing fields or validation issues.</td></tr><tr><td>Input</td><td>A single-line text field for collecting user input such as names, email addresses, or numbers. Supports placeholder text and validation options.</td></tr><tr><td>Label</td><td>Describes the purpose of a form field. Helps improve accessibility and is typically used alongside Input, Checkbox, or Radio components.</td></tr><tr><td>Radio</td><td>Lets users choose a single option from a predefined list.</td></tr><tr><td>Submit</td><td>Triggers the form submission. You can place a Button, Image, or other interactive element inside this component to send the form.</td></tr><tr><td>Success</td><td>Displays a success message when the form has been submitted successfully.</td></tr></tbody></table>

### Form Setup

To recive emails via the Form Component you will need to enter your Email server details. Here’s a breakdown of what each field means and what you’ll need to configure to make it work properly.

<table><thead><tr><th width="212">Authentication Settings</th><th>Details</th></tr></thead><tbody><tr><td>Host</td><td>Email host address. e.g. mail.yourdomain.com</td></tr><tr><td>Port</td><td>The port number the email server uses for sending messages.<br>- 587: For TLS encryption (most common) <br>- 465: For SSL encryption.<br>- 25: For non-encrypted emails (not recommended).</td></tr><tr><td>Encryption</td><td>Choose the encryption method required by your email provider. None, TLS, SSL</td></tr><tr><td>Username</td><td>The email address or username for the SMTP account you’re using to send emails. e.g. admin@yourdomain.com.</td></tr><tr><td>Password</td><td>The password for your SMTP account.</td></tr></tbody></table>

<table><thead><tr><th width="212">Email Settings</th><th>Details</th></tr></thead><tbody><tr><td>From Name</td><td>Set as needed (e.g. Jonny Appleseed)</td></tr><tr><td>From Address</td><td>Should match the Username for the account. This is usually the main issue if messages don’t send.</td></tr><tr><td>Subject</td><td>The subject of the email you'll receive. e.g. "Website Feedback"</td></tr><tr><td>To Name</td><td>The name the email will be addressed to. e.g. "Team Realmac"</td></tr><tr><td>To Address</td><td>The email address the form submission will be sent to. e.g. "support@realmacsoftware.com"</td></tr></tbody></table>

### Reply-to Address

In order for Elements to correctly set the “reply-to” header in the outgoing email, the form field name must be set to email, all lowercase.

## Form Webhooks

A webhook allows your form submissions to be sent directly to another service, like a database, CRM, or automation tool without needing to check emails or manually process the data. By sending form data to a webhook, you can trigger workflows in [Zapier](https://zapier.com/), [Make](https://www.make.com/en), or [Pipedream](https://pipedream.com), making it easy to do the following (and so much more):

• Add a new lead to Airtable or Google Sheets

• Send a follow-up email through Mailchimp or ConvertKit

• Notify your team in Slack or Discord

• Create support tickets in Zendesk or Trello

There's really no limit to what you can do with the new webhooks feature. Whether you’re building a customer support system, a lead capture form, or a dynamic survey that feeds into a database, webhooks unlock powerful automation and customization that email simply can’t match.

### Webhooks and Attachments

If you are using an attachment in your form, only the first attached file will be sent via the WebHook. Multiple files are supported when sending forms via email.

Most webhook endpoints expect a single file attachment, typically for straightforward processing, like saving it to cloud storage or forwarding it via email. Supporting multiple files would require a more complex multipart or array-based structure, which many webhook endpoints don’t handle out of the box.

### Testing Webhooks Locally

Webhook submissions require a server environment, so once you **publish the page to a server**—either a remote server or a local one—you should find the submission works as expected.

If you want to test everything **locally**, you’ll need to set up a local web server on your Mac. We recommend [ServBay](https://www.servbay.com/) for this.

Here’s a quick guide:

1. **Install ServBay**
2. **Publish your Elements site** to a local folder
3. In ServBay, **create a new site** and point the root directory to your published folder
4. Open the site in your browser through ServBay for full local testing—including Forms and webhooks

{% embed url="https://youtu.be/pR26NPw0Ip8?si=4aJyKiEJp5ntrPiD" %}



