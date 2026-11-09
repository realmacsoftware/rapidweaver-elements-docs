---
description: Read and update selected Online Editor settings.
icon: gear
---

# Settings

These routes read and narrowly write site-level configuration.

### Theme

#### `GET /cms/settings/theme`

Read the current theme: preset, accent color, fonts, custom palette, surface color, site name, and logo URLs.

| Field | Value                      |
| ----- | -------------------------- |
| Auth  | Required                   |
| Role  | Owner                      |
| Plan  | Theme customization access |

Response:

```json
{
  "theme": {
    "preset": "light",
    "accent_color": "#2563eb",
    "font_heading": "Inter",
    "font_body": "Inter",
    "custom_palette": null,
    "surface_color": null,
    "site_name": "Example",
    "logo": "/assets/logo.svg",
    "logo_dark": "/assets/logo-dark.svg"
  }
}
```

#### `PUT /cms/settings/theme`

Update the theme.

| Field | Value                      |
| ----- | -------------------------- |
| Auth  | Required                   |
| Role  | Owner                      |
| Plan  | Theme customization access |

Body: any subset of the fields returned by `GET /cms/settings/theme`. Omitted fields are left unchanged.

### Users

#### `GET /cms/settings/users`

List users on the site.

| Field | Value    |
| ----- | -------- |
| Auth  | Required |
| Role  | Admin    |

Response:

```json
{
  "users": [
    { "email": "ben@example.test", "role": "owner" },
    { "email": "sam@example.test", "role": "editor" }
  ]
}
```

User management is not exposed on the REST API yet. Use the Online Editor to create users, change roles, and delete users.

### Webhooks

#### `GET /cms/settings/webhooks`

List configured webhook subscriptions.

| Field | Value           |
| ----- | --------------- |
| Auth  | Required        |
| Role  | Owner           |
| Plan  | Webhooks access |

Response:

```json
{
  "webhooks": [
    {
      "id": "wh_...",
      "url": "https://hooks.example.test/cms",
      "events": ["file.created", "file.updated"],
      "enabled": true,
      "created_at": "2026-04-20T10:00:00+00:00"
    }
  ]
}
```

Webhook create, update, and delete are not exposed on the REST API yet. Use the Online Editor. To consume webhook payloads, see [Webhooks](https://github.com/realmacsoftware/rapidweaver-elements-docs-cms/blob/main/json-api/guides/webhooks.md).
