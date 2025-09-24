---
description: Setup your publishing destinations via a URL scheme
---

# URL Scheme

Magic publishing links provide a quick way to automatically configure a publishing destination within a Elements Project. Most of the settings can be configured, reducing user error and making setup a simple one click solution.

To create a magic link, use the `elementsapp://` url scheme with `createPublishingDestination` followed by query parameters for the settings.

**Magic link format**

```
elementsapp://createPublishingDestination?[options]
```

**Example link**

{% code fullWidth="false" %}
```
elementsapp://createPublishingDestination?name=Chillidog%20Hosting&method=SFTP&server=123.123.123.123:8080&path=/my/cool/site&username=my-user-name&website=https://www.magic.com
```
{% endcode %}

**Options**\
The available options are as follows

* method: SFTP, FTP, FTPS
* server: IP address or url of server, including the port
* path: Publishing path
* username: Username
* website: Website address of published content

Please note that Password is not supported for security reasons.
