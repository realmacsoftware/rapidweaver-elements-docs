---
description: Mount the browser-based CMS admin app on a page of your published site.
---

# Online Editor

The **Online Editor** component embeds the [Online CMS Editor](../../online-cms-editor/) into a page of your site, giving editors a browser-based interface for managing Markdown content and resources without opening Elements.

You only need to add this component once. Once your site is published, visiting the page where this component lives is how you and your team sign in to edit content.

### Where to place it

The Online Editor needs its own dedicated page. A common convention is to place it alongside the content it manages — for example, an `/admin` page nested inside the same folder as your blog:

* `mywebsite.com/blog/` — your blog index (a Collection).
* `mywebsite.com/blog/post/` — your post page (an Item).
* `mywebsite.com/blog/admin/` — the page hosting the Online Editor.

You can put it anywhere you like, but keeping it close to the content makes the relationship obvious.

{% hint style="warning" %}
**Don't add any other components to the admin page.** The Online Editor takes over the full page and assumes nothing else is competing for the layout. Mixing it with Headings, Navigation, or other components will produce unpredictable results.
{% endhint %}

{% hint style="warning" %}
The page hosting the Online Editor must be published to a server that meets the [System Requirements](../../getting-started/system-requirements.md) (PHP 8.1+, JavaScript enabled in the browser).
{% endhint %}

### First-time setup

Once your site is published, visit the admin page in your browser — for example `https://mywebsite.com/blog/admin/`.

On a fresh install you'll be guided through:

1. Creating an account with an email and password.
2. Choosing the workspace name (this is shown in the editor's chrome).
3. Confirming the content folder and resources folder the editor should read from.

After setup, the same URL becomes a sign-in page for any returning user.

### Resetting the installation

If you need to run first-time setup again, delete the Online Editor configuration file from the published site.

{% hint style="warning" %}
Deleting `config.php` removes the Online Editor setup, including the admin account, configured content folders, resource folders, and workspace settings. It does not delete your Markdown content or uploaded resources.
{% endhint %}

Before deleting anything, back up `config.php` if you might need the current settings later. Then connect to your server using FTP, SFTP, SSH, or your hosting file manager and find the Online Editor assets folder. The configuration file lives in the editor PHP folder:

```
components/shared/assets/editor/php/config.php
```

Delete `php/config.php`, reload your admin page, and complete first-time setup again.

### Free vs. Pro features

The free tier covers a single workspace with one content folder and one resources folder — enough for a blog or small site. Pro unlocks multiple users and groups, multiple content and resources folders, sub-folder support, version history, the Frontmatter UI Manager, webhooks, custom branding, the license/domain manager, the [AI Writing Assistant](../../online-cms-editor/ai-writing-assistant.md), MCP access, and the JSON API.

Pro is a one-time purchase through FastSpring and covers one top-level domain plus all of its subdomains. Existing Solo and Studio licenses purchased through Creem remain valid. See the [Online CMS Editor](../../online-cms-editor/) overview for the full feature list and [Legacy Licenses and Upgrading to Pro](../../online-cms-editor/upgrading-and-downgrading-plans.md) for legacy license guidance.

### Keeping content in sync with Elements

Anything you create or edit in the Online Editor lives on the server only. Elements pushes content out, but doesn't currently pull changes back in.

In practice that means:

* Files added or edited online won't appear in the CMS folder inside Elements.
* You can't manage online-only files from the Elements app.
* Republishing from Elements may overwrite changes made online.

If you have a team that does most of its editing in the browser, the safest workflow is to do _layout and design_ in Elements and _content edits_ online — and to coordinate before republishing.

### Troubleshooting

**The page renders but the editor doesn't load.**\
Check that JavaScript is enabled in the browser, and that the page contains _only_ the Online Editor component (no Navigation, Footer, or other layout components on the same page).

**I forgot the admin password.**\
Use the editor's **Forgot password?** flow if it is available on your sign-in page. If you need to discard the current editor account and run setup again, follow [Resetting the installation](online-editor.md#resetting-the-installation).
