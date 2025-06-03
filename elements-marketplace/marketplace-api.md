---
description: Access the latest Elements Addons, directly from the source.
icon: rss
---

# Marketplace API

The Elements Marketplace API provides a simple, read-only JSON endpoint for fetching all available Addons. Use this to power in-app listings, build third-party tools, or stay up to date with the latest components, templates, and integrations available for Elements.

```
https://marketplace.realmacsoftware.com/api/elements/addons
```

#### Response

Returns a JSON array of Addons, each including metadata such as

* id
* name
* type (e.g. component, template, stack)
* author
* description
* price
* url
* version
* image (thumbnail)
* tags

#### &#x20;Example Use Cases

* Display the latest Addons inside your own app or tool
* Filter or search Addons by type or tag
* Create a curated feed or integration on your website
