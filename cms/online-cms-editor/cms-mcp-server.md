---
description: Elements CMS MCP Server
icon: mcp
---

# CMS MCP Server

{% hint style="info" %}
This is the documentation for the Elements CMS MCP server. The Elements Mac App has a separate MCP server. These are two distinct MCP servers, with their own set of tools.
{% endhint %}

Elements CMS includes an MCP server (Pro CMS license required), which is a bridge that lets an AI assistant like Claude or ChatGPT work directly with your site. Once it's connected, you can manage your content by simply describing what you want in plain language, and the assistant carries it out against your live install. Instead of clicking through an editor, you might say "write up a new post about the launch and tag it announcements," or "add an image to my latest post," and it happens directly in your site.

Think of it as giving an assistant a set of keys to your Elements site, but keys that only open specific doors. Everything the assistant can do maps to a defined action, and those actions respect the same roles and permissions your site already uses. Owner-only settings stay owner-only, admin tasks require an admin, and nothing happens that you couldn't have done yourself through the normal interface.

The following video will give you an overview of how useful the CMS MCP server can be.

{% embed url="https://youtu.be/dy_hvVQ6a38?si=sM9w4tiAiMyEKYht" %}

### How to Setup the MCP Server.

As the time of writing (July 2026), the following Mac applications have MCP support and can connect to the Elements CMS MCP server:

* Claude Code (Anthropic)
* Codex (OpenAI)
* Cursor (Anysphere, Inc)
* Gemini (Google, only available in the US on the Ultra plan)
* LM Studio

You can find the settings to connect to the the CMS MCP server under Workspace > AI > Connections in the admin area of the CMS Online Editor.

<figure><img src="../../.gitbook/assets/CleanShot 2026-07-16 at 11 .10.43@2x.png" alt=""><figcaption></figcaption></figure>

### How to Set Up the CMS MCP Server with Claude

If you're using the Claude desktop app, click **Download for Claude Desktop**. This generates a private connection token and packages it as a `.mcpb` file. Once it's downloaded, double-click the file to install it in Claude Desktop, no further configuration required. Claude will then have access to your site and you can start managing content by simply asking.

Each time you download, the Elements CMS creates a fresh token, which you'll see listed on the page. If you ever want to disconnect a particular install, revoke its token and that bundle stops working, without affecting any of your other connections.

{% embed url="https://youtu.be/2-yVxnqkXIA?si=1HbcmVsibLT54o1v" %}

### Connecting any other MCP client

Most other clients that support a custom MCP server can connect too.

The **Endpoint** is the base MCP URL for your site. Clients that support bearer tokens (such as MCP Inspector or curl) should use this URL together with the **Authorization header**, which takes the form `Authorization: Bearer mcp_…`. This is the recommended setup.

{% embed url="https://youtu.be/9e9VQNJittA?si=Oejm1wyNEdR01XEs" %}

{% hint style="warning" %}
**A note on Tokens:** Your connection token is the key to your site, so treat it like a password. Don't share it, and revoke any token you no longer use or suspect has been exposed. Because each connection has its own token, you stay in full control of what's connected and can cut off access at any time.
{% endhint %}

### Working with content

The heart of the online editor is your Markdown files. Your site is organised into collections, which are the groupings you already know: your blog, your portfolio, your notes, or whatever structure you've set up. The assistant can look through your collections, read any individual item including its frontmatter and body, and see how everything is arranged before making a change.

From there it can write new markdown files, update existing ones, and remove items you no longer want. When it creates something, it handles the housekeeping for you: generating a sensible filename, dating it, and deriving a URL slug from the title. When it updates an item, it merges your changes in rather than overwriting everything, so editing a title or a tag won't disturb the body of the post.

{% embed url="https://youtu.be/Y1m3106Lnk0?si=YACZZUIw8kUVzu3f" %}

### Images, files, and media

Alongside your writing, the CMS manages the resources your site depends on: images, downloads, and other files. The assistant can browse your resource folders, add new files, rename and move them, and delete the ones you're done with. This means a request like "upload these three photos and put them in the blog folder" is a single, natural instruction.

{% embed url="https://youtu.be/m5IeJeWpLa0?si=_-e1c_HpjpRQW4Jg" %}

### Site settings and appearance

The MCP server can also edit a handful of site-wide settings. The assistant can read and adjust your theme, including the site name, accent and surface colours, fonts, and whether the site runs light, dark, or automatic. For administrators there's visibility into who has access to the site and which webhooks are configured, so you can review the people and integrations connected to your install. These higher-level settings are gated to owners and admins, matching the trust levels Elements uses everywhere else.

Here's the full tool list exposed by the Elements CMS MCP server, grouped by area.

### Elements CMS MCP Tools

Everything the MCP server can do is exposed as a set of named tools. You won't normally call these by name yourself, the assistant selects the right one based on what you ask, but it's worth understanding the shape of what's available so you know the boundaries of what can be done and can phrase your requests with confidence.

The tools fall into four groups. Content tools handle your posts and pages, from listing and reading through to creating, updating, and deleting them. Resource and media tools manage the files your site relies on, such as images and downloads, including uploading, organising, and removing them. Version history tools let you review and roll back changes. Settings tools reach site-wide options like your admin theme, and give administrators visibility into users and webhooks.

#### Content

* `content_list_collections` — Lists the content collections (folders) configured for the site, returning each collection's index, label, path, and field schema.
* `content_list_items` — Lists the markdown items inside a collection, optionally drilling into a subfolder (subfolders on licensed installs only).
* `content_read_item` — Reads a single markdown item, including its frontmatter and body.
* `content_create_item` — Creates a new markdown item in a collection. The slug is derived from the title if not supplied, and the filename is date-prefixed by default.
* `content_update_item` — Updates an existing item. Submitted frontmatter fields are merged over the existing ones, and any omitted fields (including the body) are preserved.
* `content_delete_item` — Deletes a markdown item and cleans up its version history.
* `content_create_collection` — Registers a new top-level content collection, creating the directory if it doesn't exist. Requires an admin-role token.

#### Resources & media

* `resources_list` — Lists the files inside a resource folder.
* `resources_upload_request` — The preferred upload path. Mints a short-lived (120s) one-shot upload URL so the file is posted directly, never passing through the model — the only path that works for non-trivial file sizes.
* `resources_upload` — Inline base64 upload for tiny files only (under \~256 KB, e.g. favicons).
* `media_upload` — Inline base64 image upload for tiny images only (under \~256 KB), validating that the content is an allowed image type.
* `resources_create_folder` — Creates a subfolder inside a resource folder (requires a license).
* `resources_move` — Moves a resource file to a different subfolder and/or renames it, preserving the extension.
* `resources_rename` — Renames a resource file in place, preserving the extension.
* `resources_delete` — Deletes a binary resource/media file (as opposed to a markdown item).

#### Version history

* `versions_list` — Lists the saved versions for an item.
* `versions_read` — Reads a specific saved version of an item.
* `versions_restore` — Restores a previous version, overwriting the current one.

#### Settings

* `settings_get_theme` — Reads the site's theme settings.
* `settings_update_theme` — Updates theme settings such as site name, accent and surface colours, fonts, and light/dark/auto preset (owner only).
* `settings_list_users` — Lists admin users (admin role required).
* `settings_list_webhooks` — Lists configured webhooks (owner role required).
