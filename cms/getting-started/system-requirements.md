---
description: Basic requirements for running Elements CMS on your server
icon: desktop
---

# System Requirements

### Server Requirements

Elements CMS runs on standard PHP hosting and does not require a database server.

* The Elements CMS **requires PHP 8.4** or newer to be installed on your server, including the following PHP extensions:
  * **json**
  * **session**
  * **curl**
  * **mbstring**
  * **Sodium**
* The bundled Composer dependencies must be present. These are included with the CMS pack when it is published.
* The Online Editor's PHP config directory must be writable so setup can save its configuration.
* The PHP installation should be 'as usual'. If it is reduced or modified in any way, the CMS may not function properly.
* Windows web servers are not officially supported.

{% hint style="danger" %}
Elements CMS [requires PHP 8.4](system-requirements.md) or newer to be installed on your server. You'll need to **ensure your page extension is set to .php** on any pages you wish to access CMS data from.
{% endhint %}

#### Online CMS Editor Requirements

* The Online CMS Editor **requires PHP 8.4** or newer to be installed on your server.
* The Online Editor setup checks for the `json`, `session`, `curl`, and `mbstring` PHP extensions.
* The Online Editor config directory must be writable.
* Also requires JavaScript to be enabled in your browser.

#### Check your PHP environment

To quickly check your PHP environment, create a new file on your server called `phpinfo.php` and add the following line:

```php
<?php phpinfo(); ?>
```

Upload it to your site and visit it in your browser (for example https://yoursite.com/phpinfo.php). This will display a detailed page showing the PHP version, loaded extensions, and configuration settings.

Remember to delete the file once you’ve checked, as it exposes sensitive server information.

#### PHP Page extension

Ensure the page extension is set to .php on all pages you wish to access CMS data from. If you leave your page extension as .html, the CMS will not function.
