---
description: Add an old-skool favicon to your website
icon: icons
---

# favicon

While Elements has support for all of the popular favicons, it doesn't generate a favicon.ico file. This icon is important if you want your logo to appear in Google Search Results.

First you'll need to convert your logo into a `favicon.ico` file, to do this you can use a free [online png to .ico conversion tool](https://favicon.io/favicon-converter/).

Once you have your  `favicon.ico` file, you'll need to upload it to root of your web server, and add the following line of code to the template of your project:

`<link rel="icon" href="/favicon.ico" type="image/x-icon">`

This can be done via the Project Settings window inside of the Template:

<figure><img src="../../.gitbook/assets/CleanShot 2025-11-26 at 10 .08.16@2x.png" alt=""><figcaption></figcaption></figure>

Once all these changes have been made you should re-publish your website to ensure all of the pages get updated with the new favicon.ico link.
