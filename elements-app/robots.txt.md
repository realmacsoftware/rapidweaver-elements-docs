---
description: How to add a robots.txt file to your Elewments Project
---

# Robots.txt

A robots.txt file tells search engine crawlers which parts of your website they can or can’t access. It sits at the root of your domain (e.g. https://example.com/robots.txt).

{% hint style="info" %}
A robots.txt file is a _request_, not a guarantee. Well-behaved bots obey it, but malicious ones may ignore it. It also does not prevent indexing of pages if they’re linked to elsewhere, use noindex meta tags for that.
{% endhint %}

### To add a robots.txt file in Elements:

1. Right-click in the Page List area of your project window and choose New File.
2. A new file named untitled.html will appear — rename it to robots.txt.
3. Double-click the file to edit its contents, and add any robots.txt directives you need.

This file will be published to the root of your website, making it accessible to search engines at https://yourdomain.com/robots.txt.

### Example robots.txt file:

You can use this on your own site, just don’t forget to change the domain name to ensure you're pointing to your own sitemap.

```
User-agent: *
Allow: /

Sitemap: https://example.com/sitemap.xml
```



