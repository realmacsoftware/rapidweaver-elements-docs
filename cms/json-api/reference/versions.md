---
description: Read item version history and restore previous versions.
icon: clock
---

# Versions

Every write to an item can produce a version-history snapshot. These routes expose that history.

{% hint style="info" %}
Version history depends on the site's license limits. This is in addition to the whole-API JSON access gate.
{% endhint %}

{% hint style="warning" %}
The JSON API router declares read and restore routes with a `{version}` path segment, while the current editor handler expects that value internally as `timestamp`. Until that adapter is aligned, use the Online Editor for reading or restoring a specific historical version.
{% endhint %}

### `GET /cms/collections/{collection}/items/{slug}/versions`

List versions for an item, newest first.

| Field | Value |
| --- | --- |
| Auth | Required |
| Role | Any API key user |

Response:

```json
{
  "versions": [
    { "timestamp": 1713611100, "size": 1204 },
    { "timestamp": 1713607273, "size": 1100 }
  ],
  "current": {
    "modified": 1713612200,
    "size": 1280
  }
}
```

`timestamp` values are integer Unix timestamps.

### `GET /cms/collections/{collection}/items/{slug}/versions/{version}`

Read a single historical version's full content.

| Field | Value |
| --- | --- |
| Auth | Required |
| Role | Any API key user |

Pending adapter alignment for external JSON API clients.

### `POST /cms/collections/{collection}/items/{slug}/versions/{version}/restore`

Promote a historical version back to current. This writes a new version on top of history. It does not rewrite history.

| Field | Value |
| --- | --- |
| Auth | Required |
| Role | Any API key user |

Pending adapter alignment for external JSON API clients.
