---
description: Use the Elements CMS JSON REST API for headless frontends, apps, and scripts.
icon: code
---

# Overview

The Elements CMS Online Editor includes a token-authenticated JSON REST API for headless use. Your apps, mobile clients, static builds, and migration scripts can read and write CMS content over HTTPS with a simple `Authorization: Bearer api_...` header.

If you want Claude, Cursor, or another AI assistant to manage the CMS through conversation, use the [MCP Server](../mcp/) instead.

{% hint style="warning" %}
**Pro / JSON API access is required.** Every `/api/*` route, including public reads, requires an active Pro license for the site's domain with JSON API access enabled. Without one, every request returns `402 Payment Required`.
{% endhint %}

### Start here

* [Installation](installation.md) - prerequisites and how to verify the API is reachable.
* [Authentication and API Keys](authentication.md) - creating keys in the Online Editor, header format, and how API keys differ from MCP tokens.
* [Quickstart](quickstart.md) - a short walkthrough: list, create, update, and delete CMS content.

### Choose your path

| Building this                          | Start here                                                                                                                           |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Headless frontend, static site, or SPA | [Headless Frontend](https://github.com/realmacsoftware/rapidweaver-elements-docs-cms/blob/main/json-api/guides/headless-frontend.md) |
| Mobile or desktop client               | [Authentication](authentication.md), then [Items](reference/items.md)                                                                |
| Bulk migration script                  | [Content Migration](https://github.com/realmacsoftware/rapidweaver-elements-docs-cms/blob/main/json-api/guides/content-migration.md) |
| Upload integration                     | [Uploads](https://github.com/realmacsoftware/rapidweaver-elements-docs-cms/blob/main/json-api/guides/uploads.md)                     |
| Webhook receiver                       | [Webhooks](https://github.com/realmacsoftware/rapidweaver-elements-docs-cms/blob/main/json-api/guides/webhooks.md)                   |

### Reference

The route reference is split by surface area:

* [Reference Overview](reference/)
* [Collections](reference/collections.md)
* [Items](reference/items.md)
* [Resources](reference/resources.md)
* [Versions](reference/versions.md)
* [Settings](reference/settings.md)
* [Search and Feeds](reference/search-and-feeds.md)

### Errors and versioning

* [Errors](errors.md) - status codes, response shapes, and troubleshooting.
* [Changelog](changelog.md) - API versioning policy and notable changes.
