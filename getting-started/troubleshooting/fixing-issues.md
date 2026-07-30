---
description: Diagnose and resolve problems publishing your website
---

# Publishing Issues

Can’t get your website online or updated? Publishing problems are often caused by incorrect connection details. Every setting must match the information provided by your hosting company.

{% hint style="danger" %}
### Urgent Publishing Issue? Use a Standalone FTP Client

If you need to get an update online urgently, export your website and upload it with a standalone FTP client. After uploading the site manually, contact us so we can help resolve the publishing issue in Elements.

Enter your connection details in a third-party client to verify that they are correct. [Transmit](https://www.google.com/url?sa=t\&rct=j\&q=\&esrc=s\&source=web\&cd=\&cad=rja\&uact=8\&ved=2ahUKEwiarpPjmtb3AhWEK0QIHSoZDxAQFnoECAUQAQ\&url=https%3A%2F%2Fpanic.com%2Ftransmit%2F\&usg=AOvVaw3fa_bRPF5Z5ggPXHa3-KBK) and [Cyberduck](https://cyberduck.io/) are both suitable for this test.\
\
If you cannot log in with a third-party client, your connection details are probably incorrect. Contact your hosting company to verify them.\
\
If you can log in successfully, export your site to a local folder and upload it with the FTP client as a temporary workaround.<br>
{% endhint %}

### Check Your Credentials

**By far the most common cause of publishing issues is that the credentials entered are not accurate.** It’s incredibly important that you double-check the details you’ve entered.\
\
To view your configured publishing details, choose **File › Publishing Settings** (Command-K).\
\
Check that all the fields are entered correctly: Server Address, Username, Password, Path, etc.\
\
An incorrect Path is a common cause of publishing problems. Common site paths include:

* /
* httpdocs/
* www/
* public\_html/

You can always use the “Browse” button inside the publishing settings to pick the correct path on your server.

Paths vary between hosts, so consult your host’s documentation to find the correct upload folder. You can also contact your host to check whether its server settings have changed and whether your account has enough storage space.

### Tweak Server Configurations

Elements provides several publishing options, particularly for FTPS. Check which settings your server requires, as some hosting providers use specific configurations.\
\
Elements cannot reliably detect every FTP setting. If you are unsure, contact your hosting company.\
\
If you think it's all set up correctly, try this next:

### Concurrent Connection Limit

If your host limits the number of connections that can be made to your server, you can set Elements to use fewer connections when publishing. If in doubt, set this to 1.\
\
To do this, open Elements Settings and set Maximum Concurrent Uploads to 1 before publishing your project again.\
\
If that didn't help, it's time to try something completely different:

### Switch from FTP to SFTP

If you're having issues publishing via FTP, we recommend publishing via SFTP as this is often more reliable (and secure).

Contact your hosting company to check your SFTP details as they can often be slightly different to your FTP details.

### Re-add Your Publishing Details

If your credentials work in another FTP app but not in Elements, delete the publishing destination and add it again. This ensures that all the saved details are current and verified.\
\
If you are comfortable using your hosting control panel, you could create a new FTP account and test it. Otherwise, move on to the next troubleshooting step.

### Check Server Space

This issue is common, especially when publishing multiple websites to the same server. Project backups can accumulate over time and use all the available server space.\
\
If the server is out of space, Elements may report “Couldn't upload to your FTP server”. More information may include “Transferred a partial file” or “Operation was aborted by an application callback”.\
\
If you see these errors, sign in to your hosting account and compare the available space with your current usage. You can delete older project backup files to make room for new uploads.\
\
If you are unsure, ask your hosting provider how much space you are using and how much remains available.\
\
Once you have enough space, you should be able to resume updates to your website.

### Changes Are Not Visible on the Website

Choose **File › Re-Publish All Files** to upload the entire site again. Some files may be missing from the server. You may also need to clear your browser history and website data because the browser could be displaying an older cached version.

{% hint style="info" %}
In Safari, choose **History › Clear History…**. In Google Chrome, choose **Chrome › Clear Browsing Data…**.
{% endhint %}

Some hosts require an upload path that begins with a forward slash. Only include one when your hosting company specifies it.

{% hint style="info" %}
Sometimes users create both `index.html` and `index.php`, with the latter being the most recent. Browsers will normally load `index.html` first. To use `index.php`, rename or remove the `index.html` file in that directory.
{% endhint %}

### I Have Tried Everything but Still Need Help

Elements can create a detailed publishing report that the Realmac Software support team can use to identify potential problems.\
\
Open Elements Settings, select Publishing and enable **Upload Logging**.

<figure><img src="../../.gitbook/assets/CleanShot 2025-07-11 at 2 .18.24@2x.png" alt="Publishing preferences with Enable upload logging switched on"><figcaption></figcaption></figure>

Follow these steps to send your publishing logs to us:

1. Quit Elements.
2. Reopen your project in Elements.
3. Choose **File › Re-Publish All Files**.
4. If publishing returns an error, click **Send Upload Logs**.
5. Add details about the issue to the generated email and send it.

#### Error Messages

If you see an error when exporting your site, there may be a problem with an add-on or resource in the project. If the error consistently occurs on a particular page, check it for missing resources or add-ons that may be causing the problem.

### Contacting Support

When contacting Realmac Software, please include as much detail as possible. Please also use the Help menu’s Copy Support Logs.\
\
Please be sure to include the following details in your message:

* Who are you hosting your website with?
* Which version of Elements are you using? Which version of macOS is running on your Mac?
* How large is your Elements project file?
* Which, if any, third-party add-ons are you using with your project? Please include any third-party themes.
* Are you seeing an error message when publishing? Please include the full text of the error or, ideally, a screenshot.

We aim to reply to all messages within two business days. We know it is frustrating when you cannot publish, and we will do our best to help resolve the issue.

{% include "../../.gitbook/includes/elements-website-hosting.md" %}
