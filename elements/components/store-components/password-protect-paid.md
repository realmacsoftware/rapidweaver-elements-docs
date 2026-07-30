# Password Protect (Paid)

{% hint style="success" %}
The Password Protect pack is only available as a **paid product via the Element Store.**
{% endhint %}

Lock down sensitive pages and sections with these dedicated components, Add secure, password protection anywhere on your site without touching a single line of code.

The Page Password component protects an entire page by intercepting the render pipeline and showing a clean password form until the visitor is authenticated. The Section Password component works inside your layouts, hiding specific blocks of content and only revealing the dropzone once the correct password is entered. Nothing leaks through to the browser.

If you need a simple, reliable way to lock down content in Elements, this pack does the job.

#### Setup

Any page that uses the Password Protect component must be set to PHP. If it isn’t, you’ll hit an error as soon as you publish your site to your server, like this:

{% code overflow="wrap" %}
```php
false, ‘message’ => $errorMessageText ]); exit; } } // Re-check authentication (may have been restored from cookie) $isAuthenticated_rwA34124B0_12C5_4DC0_9CE9_AB223CC1141C = password_protect_is_authenticated(‘password_protect_shenjin’); // Capture the protected content for AJAX response ob_start(); ?>
```
{% endcode %}

To fix this error, you'll need to remove the .html file(s) from your server, and change the page extension in your project to .php

#### Password Protect Introduction Video

Dan and Ben discuss the new Password Protect Pack for Elements, showcasing its features, security measures, and customisation options. They delve into the user experience, including advanced login features like biometric authentication, and highlight the importance of security in web design.

{% embed url="https://www.youtube.com/watch?v=OrB7npyl13E&pp=2AbIAQ%3D%3D" %}
