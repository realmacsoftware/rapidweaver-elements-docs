---
description: A guide fixing your Publishing Issues
---

# Fixing Issues

Can't get your website online or updated? Don't worry. 99% of the time the issue is due to incorrect setup of publishing details. Everything needs to be entered 100% correctly otherwise publishing fails.

{% hint style="danger" %}
### Mission Critical Publishing Issue? Use a Standalone FTP Client

The following is recommended if you're having issues publishing your site and you need to get an update online as soon as possible. After manually uploading your site we recommend you get in touch with us to help resolve the issue publishing with Elements.

We recommend entering your details into a third-party client to verify they work and are correct. [Transmit](https://www.google.com/url?sa=t\&rct=j\&q=\&esrc=s\&source=web\&cd=\&cad=rja\&uact=8\&ved=2ahUKEwiarpPjmtb3AhWEK0QIHSoZDxAQFnoECAUQAQ\&url=https%3A%2F%2Fpanic.com%2Ftransmit%2F\&usg=AOvVaw3fa_bRPF5Z5ggPXHa3-KBK) and [Cyberduck](https://cyberduck.io/) are both great FTP clients and can be downloaded freely for this test.\
\
If you're still having issues logging into your server with a third-party client it means your login credentials are incorrect. Please contact your hosting company to verify your details.\
\
If you successfully log in to your server with a third-party client, you can then export your site to a local folder with RapidWeaver, and then upload it directly using an FTP client as a temporary workaround.\

{% endhint %}

### Check your Credentials

**By far the most common cause of publishing issues is that the credentials entered are not accurate.** It’s incredibly important that you double-check the details you’ve entered.\
\
To view your configured publishing details, choose:\
\
File > Publishing Settings (Command-K).\
\
Check that all the fields are entered correctly: Server Address, Username, Password, Path, etc.\
\
Entering an incorrect Path is the most common cause of publishing problems in RapidWeaver. Some common site paths may include:

* /&#x20;
* httpdocs/&#x20;
* www/&#x20;
* public\_html/

You can always use the “Browse” button inside the publishing settings to pick the correct path on your server.

The list above is by no means an exhaustive list as paths vary greatly between different hosts, so if you’re still experiencing issues, please consult your web host’s online help to determine the Path required to upload to the correct folder. Sometimes, the Path may be known as the “Upload Folder”. You may also want to contact your web host directly and ensure that they have not made any recent changes to the server which may affect your settings and that you’ve not run out of webspace.

### Tweak Server Configurations

RapidWeaver has a number of options to configure publishing - particularly if you’re using FTPS uploading. Please check what your server is expecting, some hosting providers require specific settings.\
\
Due to the nature of how FTP works, RapidWeaver cannot reliably detect the correct settings that you should use. If in doubt email your hosting company.\
\
If you think it's all set up correctly, try this next:

### Concurrent Connection Limit

If your host limits the number of connections that can be made to your server, you can set RapidWeaver to use a smaller number of connections when publishing. If in doubt set this to 1.\
\
To do this, open RapidWeaver’s Preferences window, and adjust the slider for the Maximum Concurrent Uploads to 1 before attempting to publish your project once again.\
\
If that didn't help, it's time to try something completely different:

### Switch from FTP to SFTP

If you're having issues publishing via FTP, we recommend publishing via SFTP as this is often more reliable (and secure).

Contact your hosting company to check your SFTP details as they can often be slightly different to your FTP details.

### Re-add your publishing details

If you have verified your publishing credentials are correct in another FTP app and it's still not working inside RapidWeaver please delete your publishing destination, and re-add a new publishing destination. By doing this you ensure all the details are new and verified.\
\
If you're super technical and can log into your hosting cPanel, you could try setting up a new FTP accountant see if that works. If this means nothing to you, you can safely ignore this and move on to the next troubleshooting step.

### Check Server Space

This issue is surprisingly common, especially if you're publishing multiple websites to the same server. By default, RapidWeaver will backup your project file to the server, and this can easily build up over time and you can run out of server disk space.\
\
If you've run out of server disk space RapidWeaver will give the following error: “Couldn't upload to your FTP server” and if you click on the “i” to get more info it may say “Transferred a partial file” or “Operation was aborted by an application callback”.\
\
If you're seeing these errors, check how much space you're using on your server, and check how much you've allocated by logging into your hosting provider. You can safely delete some of the older RW backup files to make room for new uploads.\
\
If in doubt you can always email your hosting provider and ask how much space you're using and how much you have available.\
\
Once you have enough space, you should be able to resume updates to your website.

### Changes aren't visible on Website

Use the File menu’s Re-Publish All Files option to re-upload your site. It may be that some files are missing and were not uploaded. You may also want to remove the history and browsing data in your web browser. Sometimes web browsers can display older cached data.

{% hint style="info" %}
In Safari, this is found on the History menu > Clear History…, in Google Chrome it’s found on the Chrome menu > Clear Browsing Data….
{% endhint %}

Some hosts may require you to use a path that begins with a forward slash (which has a special meaning to a web server). Unless you explicitly state that your path should start with a forward slash, you should not attempt to use a path with a forward slash - otherwise, you may well run into publishing difficulties.

{% hint style="info" %}
Sometimes users create an index.html and index.php file with the latter being the most recent. Browsers will ALWAYS use the index.html file as primary. If you want the index.php file to be seen, you can either rename or remove that index.html file in that directory.&#x20;
{% endhint %}

### I've tried everything, but still need help

RapidWeaver can also be configured to produce a more in-depth report about publishing that the Realmac Software support team can use to identify potential problems.\
\
First of all open RapidWeaver’s preferences (Cmd,) and select the Publishing preferences pane. Make sure that the Enable Upload Logging option is checked.

<figure><img src="../../../.gitbook/assets/CleanShot 2025-07-11 at 2 .18.24@2x.png" alt=""><figcaption></figcaption></figure>

Please do the following step to send your publishing logs to us:

1. Quit RapidWeaver.
2. Re-open your project in RapidWeaver.
3. Attempt to republish your RapidWeaver project by choosing File>Re-Publish All Files.
4. If the publishing feature returns an error, hit the “Send Upload Logs” button.
5. It will then attempt to generate an email with the publishing logs, enter some details about your issue, and hit send!

#### Error Messages

Exporting If you’re seeing an error message when exporting your site, this may mean that there’s a problem with either an addon or a resource in your project. If an error message appears consistently when exporting a particular page, take a look at the page - are there any resources missing, or a particular addon that may be causing a problem?

### Contacting Support

When contacting Realmac Software, please include as much detail as possible. Please also use the Help menu’s Copy Support Logs.\
\
Please be sure to include the following details in your message:

* Who are you hosting your website with?
* Which version of RapidWeaver are you using? What version of macOS is running on your Mac?
* How large is your RapidWeaver project file?
* Which, if any, third-party addons are you using with your project? Please include any third-party themes.&#x20;
* Are you seeing an error message when publishing? Please include the full text of the error or, ideally, a screenshot.

We aim to reply to all messages within 2 business days. We know it's frustrating not being able to publish, but do remember we're only human and we do our best to help in what can be a very complex issue.

