---
description: Send form data via email or webhooks
---

# Form

The Form Component is a flexible and powerful solution for sending form submissions either to your own email server or via a webhook.

### Recommendation

We recommend using a Webhook to handle email delivery or data collection. It’s significantly more reliable and easier to set up than configuring SMTP manually, which can often lead to issues with authentication, server compatability, spam filters, or SSL mismatches.

### Server Requirements

The Form Component in Elements **requires PHP 8.1 or newer**. You can run the built-in [PHP Server check](./#php-server-check) to ensure your server meets this requirment.

### ✅ Form Compatibility Checklist

Before going live with your form, make sure you’ve covered the following essentials. These common issues can prevent form submissions from working correctly, so it’s worth double-checking everything below:

* [ ] **Forms must be published to a live server.** They won’t function when previewed locally.
* [ ] **Your web server must be running PHP 8.1 or newer.** We recommend PHP 8.4 or later where possible. Ensure you have run the built-in [PHP Server check](./#php-server-check).
* [ ] **Make sure your SMTP Settings Match Your Domain**. It’s important that your SMTP settings match your domain configuration.
* [ ] **Sending multiple attachments?** Be sure to enable the “**multiple**” toggle in the Attachment Component settings.
* [ ] **Using the reply-to feature?** The field name for your email input must be exactly email (all lowercase) for Elements to set the reply-to address properly.
* [ ] **Avoid special characters in field names.** Stick to letters, numbers, and hyphens. Avoid spaces, symbols, or punctuation in form field names as they may not be parsed correctly on the server.
* [ ] **Use the Error and Success components.** These components are optional. However, without them, users won’t see feedback after submitting the form. Include both for a complete user experience.

### ⚠️ Troubleshooting Email Sending Issues

If you've published your form, and are still having issues, please run through this troubleshooting guide to help resolve common issues:

1. Run the [PHP Server check ](./#php-server-check)to ensure version on your server meets the minimum requirements.
2. Check your hosting provider’s documentation to ensure outbound SMTP is supported.
3. Ensure you have entered the correct details for the Form Setup, this is worth triple checking as this is the most common cause of why a form is not delivering email.
4. In some cases, your email provider will block sending if the From address doesn’t match your SMTP account. Make sure: The From Email matches the SMTP Username. The To Email is valid and not blacklisted or blocked by spam filters.
5. Review your form logs to see detailed error messages, this can be found at the following location on your server: `rw/elements/com.realmac.corepack/api/logs` the file name will look something like this `form_rw904107B7_1234_4FDC_9B97_1D9A663C1B17-2025-07-24.log` — Note the date on the end of the file, this is helpful for ensure you're checking the correct log file.
6. If you are sure all your details are correct, and you have verifed them with your email hosting provider, please [post your issue on our forum ](https://forums.realmacsoftware.com/)and we'll help you troubleshoot further.

### ✅ Match Your SMTP Settings to Your Domain

When using a custom SMTP server to send form submissions, it’s important that your SMTP settings match your domain configuration.

Here’s what to check:

* **Email Address:** Make sure the “From” address you’re using belongs to the same domain your site is hosted on (e.g. form@yourdomain.com if your site is hosted at yourdomain.com).
* **SMTP Server:** Use the correct hostname for your mail server. This should match the SSL certificate used by the server (e.g. mail.yourdomain.com, not just localhost or an IP).
* **TLS/SSL Certificate:** Your mail server must have a valid certificate that matches the SMTP server hostname. If there’s a mismatch, some providers (especially Gmail) will reject the connection.
* **Authentication:** Use the correct username and password for your SMTP account.

### ⚠️ A note on sending and receiving email

&#x20;You need to use your own email address as the “From” address because the mail server will only send messages that come from an address it recognises.

If we used the visitor’s email there, the message might get blocked. The usual way around this is to keep your own address as the sender, and then set the visitor’s email as the **Reply-To**.

That way the form email always gets delivered, and when you hit reply it goes straight back to them — this is how Forms work in Elements.

### ✅ PHP Server Check&#x20;

We recommend PHP 8.4 or later for best performance, but the minimum supported version is 8.1.

To check is the Elements API is running as expected on your server, simply append ?apicheck to the URL of any page containing a Form.

`my-website.com/contact/?apicheck`&#x20;

### ⚠️  Form Logs

To help diagnose issues with your Form, Elements generates detailed log files on your server.

#### Log Location

The logs folder is located at the root of your web server, alongside other top-level folders like index.html, images, or css.

&#x20;`rw/elements/com.realmac.corepack/api/logs`&#x20;

#### Example Log Name

The date at the end of the filename makes it easy to identify the most recent log. Make sure you’re checking the correct file based on when the issue occurred.

&#x20;`form_rw904107B7_1234_4FDC_9B97_1D9A663C1B17-2025-07-24.log`&#x20;



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



