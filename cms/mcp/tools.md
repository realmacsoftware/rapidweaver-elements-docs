---
description: Reference for the tools and resources exposed by the Elements CMS MCP server.
icon: list-check
---

# MCP Tools Reference

This page lists the tools your connected AI assistant can use through the Elements CMS MCP server. You do not need to call these tools directly. The assistant chooses them when you ask for things like listing posts, editing content, uploading media, or restoring a version.

Before using this reference, connect an MCP client with the [MCP Server](README.md) setup guide.

### How inputs work

Every tool receives a small JSON object. The assistant builds that object for you, but a few terms appear often:

* **Folder index** - each content folder and resource folder has a numeric index, starting at `0`. The assistant can discover these with `content_list_collections` or `resources_list`.
* **Subpath** - an optional subfolder inside a content or resource folder. Empty means the folder root.
* **Role restrictions** - every tool acts as the user bound to the token or OAuth connection. Owner-only and admin-only actions still require the matching role.

{% hint style="info" %}
`api_...` keys and `mcp_...` tokens are separate. The tools on this page use the MCP server, not the [JSON REST API](../json-api/README.md).
{% endhint %}

### Content

#### `content_list_collections`

Lists configured content collections, including each folder's index, label, path, and field schema.

* **Inputs:** none.
* **Example prompt:** _"What content collections does this site have?"_

#### `content_create_collection`

Creates and registers a new top-level content collection. If the directory does not exist, the CMS creates it recursively before registering the collection. When the destination is ambiguous, the assistant should confirm the server filesystem path before using this tool.

* **Required:** `label` string, `path` string.
* **Restriction:** admin role required.
* **Example prompt:** _"Create a new content collection called Case Studies next to my blog folder."_

#### `content_list_items`

Lists Markdown items inside a collection. Licensed installs can also drill into a subfolder.

* **Required:** `folder` integer.
* **Optional:** `subpath` string.
* **Example prompt:** _"Show me all posts in the blog folder."_

#### `content_read_item`

Reads a single Markdown item, including frontmatter and body.

* **Required:** `folder` integer, `file` string.
* **Optional:** `subpath` string.
* **Example prompt:** _"Read the full text of my latest press release."_

#### `content_create_item`

Creates a Markdown item in a collection. The filename is prefixed with today's date by default. If no slug is supplied, the slug is derived from the title.

* **Required:** `folder` integer, `fm` object.
* **Optional:** `subpath` string, `slug` string, `body` string, `date_prefix` boolean.
* **Example prompt:** _"Draft a new blog post titled 'Spring update' with tags 'news' and 'product'."_

#### `content_update_item`

Updates an existing Markdown item. New frontmatter fields merge over old ones, and omitted fields are preserved. If `body` is supplied, it replaces the Markdown body.

* **Required:** `folder` integer, `file` string.
* **Optional:** `subpath` string, `slug` string, `fm` object, `body` string.
* **Example prompt:** _"Set yesterday's post status to published."_

#### `content_delete_item`

Deletes a Markdown item and cleans up its version history.

* **Required:** `folder` integer, `file` string.
* **Optional:** `subpath` string.
* **Example prompt:** _"Delete the draft titled 'Scratch notes'."_

### Resources and Media

#### `resources_list`

Lists files inside a resource folder.

* **Required:** `folder` integer.
* **Optional:** `subpath` string.
* **Example prompt:** _"What is in my press-kit folder?"_

#### `resources_upload_request`

Mints a one-shot upload URL that expires after 120 seconds. This is the preferred upload path because file bytes do not pass through the conversation.

* **Required:** `folder` integer, `filename` string.
* **Optional:** `subpath` string, `media_only` boolean.
* **Example prompt:** _"Upload these three photos to the gallery folder."_

#### `resources_upload`

Uploads a tiny file inline as base64. Use this only for files under roughly 256 KB. For larger files, use `resources_upload_request`.

* **Required:** `folder` integer, `filename` string, `content_b64` string.
* **Optional:** `subpath` string.
* **Example prompt:** _"Save this SVG I just pasted as favicon.svg in the root resources folder."_

#### `media_upload`

Uploads a tiny image inline as base64 and validates that the content is an allowed image type. Use this only for images under roughly 256 KB.

* **Required:** `filename` string, `content_b64` string.
* **Optional:** `folder` integer, `subpath` string.
* **Example prompt:** _"Use this small logo for the site."_

#### `resources_move`

Moves a resource file to another subfolder and/or renames it. The destination subfolder must already exist. The file extension is preserved.

* **Required:** `folder` integer, `file` string.
* **Optional:** `subpath` string, `dest_subpath` string, `new_filename` string.
* **Example prompt:** _"Move hero.jpg from the homepage folder into the archive folder."_

#### `resources_rename`

Renames a resource file in place. The file extension is preserved.

* **Required:** `folder` integer, `file` string, `newName` string.
* **Optional:** `subpath` string.
* **Example prompt:** _"Rename all press photos to start with `press-`."_

#### `resources_delete`

Deletes a resource file. Use `content_delete_item` for Markdown posts.

* **Required:** `folder` integer, `file` string.
* **Optional:** `subpath` string.
* **Example prompt:** _"Delete the old logo from the resources folder."_

#### `resources_create_folder`

Creates a subfolder inside a resource folder. Folder names may contain letters, numbers, hyphens, and underscores.

* **Required:** `folder` integer, `name` string.
* **Optional:** `subpath` string.
* **Restriction:** requires MCP access.
* **Example prompt:** _"Create a subfolder called 'press-kit' inside resources."_

### Site Settings

#### `settings_get_theme`

Reads the site's theme settings.

* **Inputs:** none.
* **Example prompt:** _"What is the site's current accent colour?"_

#### `settings_update_theme`

Updates site theme settings.

* **Optional:** `site_name`, `preset` (`light`, `dark`, or `auto`), `accent_color`, `surface_color`, `font_heading`, `font_body`.
* **Restriction:** owner role required.
* **Example prompt:** _"Switch the site to dark mode and change the accent colour to teal."_

#### `settings_list_users`

Lists Online Editor users.

* **Inputs:** none.
* **Restriction:** admin role required.
* **Example prompt:** _"Who has admin access?"_

#### `settings_list_webhooks`

Lists configured webhooks.

* **Inputs:** none.
* **Restriction:** owner role required.
* **Example prompt:** _"What webhooks are set up on this site?"_

### Version History

Version history tools require active MCP access and use the same permissions as the Online Editor.

#### `versions_list`

Lists saved versions for an item.

* **Required:** `folder` integer, `file` string.
* **Optional:** `subpath` string.
* **Example prompt:** _"Show me the history of yesterday's blog post."_

#### `versions_read`

Reads a specific saved version.

* **Required:** `folder` integer, `file` string, `version` string.
* **Optional:** `subpath` string.
* **Example prompt:** _"What did that post look like before I edited it this morning?"_

#### `versions_restore`

Restores a previous version, overwriting the current item.

* **Required:** `folder` integer, `file` string, `version` string.
* **Optional:** `subpath` string.
* **Example prompt:** _"Roll yesterday's post back to the version from 9am."_

### MCP Resources

The MCP server also exposes read-only resources. Assistants can use these for context without making a tool call.

| Resource | Description |
| --- | --- |
| `cms://site` | Site name, theme basics, install counts, and the connected user's role. |
| `cms://collections` | All content collections with their field schemas. |
| `cms://collection/{index}` | Items in a specific collection, sorted by modified date. |
| `cms://item/{folder_index}/{filename}` | The raw Markdown for a specific item. |

Example prompt:

> _"Look at the available CMS resources and tell me what content this site contains."_
