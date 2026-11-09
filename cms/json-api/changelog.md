---
description: JSON REST API versioning policy and notable changes.
icon: clock-rotate-left
---

# Changelog

### Versioning policy

The API has a single implicit version exposed by the CMS install. Breaking changes to routes, request shapes, or response shapes will be called out in release notes and gated behind a new URL prefix, such as `/cms/v2/...`, rather than silently changing an existing route.

Non-breaking additions, such as new routes, optional query parameters, or response fields, may land without a version bump.

### Unreleased

**Added**

* Authenticated JSON REST API routes for common editor automation:
  * Items: `POST`, `PUT`, `PATCH`, and `DELETE` under `/cms/collections/{collection}/items`.
  * Raw item reads at `/cms/collections/{collection}/items/{slug}/raw`.
  * Resources: `GET`, `POST`, `PATCH`, and `DELETE` under `/cms/resources`.
  * Resource folders: `POST /cms/resources/folders`.
  * Versions under `/cms/collections/{collection}/items/{slug}/versions`.
  * Settings routes for theme, users, and webhooks.
* Online Editor **API** page for creating and revoking `api_...` keys.
* JSON API access check at the top of every `/api/*` route.
* Collection slugs accepted anywhere `{collection}` appears, alongside integer indexes.

**Changed**

* The `/api/*` entry point accepts cross-origin requests when they carry an `api_...` Bearer key.
* Unauthenticated public reads remain limited to same-server origins.

**Notes**

* `api_...` keys and `mcp_...` tokens are separate. See [Authentication and API Keys](authentication.md).
