---
description: Install requirements and verify the JSON REST API endpoint.
icon: plug
---

# Installation

{% hint style="warning" %}
**Pro / JSON API access is required.** Every route of the JSON API, including the status ping, RSS feeds, sitemap, search index, and public item reads, returns `402 Payment Required` unless the site has an active Pro license with JSON API access enabled.
{% endhint %}

### Prerequisites

* PHP 8.4 or later, matching the main [System Requirements](../getting-started/system-requirements.md).
* Elements CMS v2 installed and published on a web host that can serve the CMS bundle.
* An active license with JSON API access registered to the site's domain.

No extra build step is needed. The API ships with the published CMS bundle.

### Where the API lives

The API entry point is served by the site as:

```
https://example.test/api/
```

Most routes live under `/cms/` on that base URL. The base URL shown on the **API** page inside the Online Editor is always the right value to use.

### Verify it is reachable

From a terminal on any machine that can reach the site:

```sh
curl -i https://example.test/api/
```

Useful non-200 responses:

| Status                      | Meaning                                                              | Fix                                                                                                                                         |
| --------------------------- | -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `402 Payment Required`      | The API is reachable, but this domain does not have JSON API access. | Activate an existing Pro license or purchase Pro from **Workspace > License**. |
| `401 Unauthorized`          | The route needs authentication.                                      | Create and send an `api_...` key.                                                                                                           |
| `500 Internal Server Error` | The server could not run the API route.                              | Check PHP configuration and the server error log.                                                                                           |

### Request an API key

Keys are created inside the Online Editor by an owner:

1. Sign in to the Online Editor as an owner.
2. Open **API** in the sidebar. This page appears only when JSON API access is included in the plan.
3. Click **Create Key**, name it, and choose the user the key should act as.
4. Copy the plaintext key that is shown once.

The key starts with `api_`. Store it in an environment variable or secret store. Do not commit it to a repository.
