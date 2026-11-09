---
description: Common Elements CMS issues, grouped by what you're seeing.
icon: screwdriver-wrench
---

# Troubleshooting

Most CMS issues come down to a small set of root causes — a wrong page extension, a missing PHP extension, a filename casing mismatch, or a misconfigured `.htaccess`. This page walks through the symptoms you're likely to see, grouped by where they show up.

{% hint style="danger" %}
Elements CMS [requires PHP 8.4](../system-requirements.md) or newer to be installed on your server. You'll need to **ensure your page extension is set to .php** on any pages you wish to access CMS data from.
{% endhint %}

### Page-level issues

#### The page is blank, or shows raw PHP source

The page extension is set to `.html` instead of `.php`. The CMS runs as PHP code embedded in the page, and the server only executes that code if the page extension tells it to.

Open the page settings inside Elements and change the extension to `.php`. Re-publish, and the page should render normally.

#### A PHP error message appears on the page

Same root cause as above — the page extension is `.html`. When the rewrite or the framework executes the file as raw text, parts of the embedded code leak through. Fixing the extension fixes the error.

If the error persists with a `.php` extension, check that your server's PHP version is 8.1 or newer. Older PHP versions will fail on syntax the CMS uses.

#### A 500 Internal Server Error after publishing

Common causes, in order of likelihood:

1. **PHP version too old.** Confirm your server is running PHP 8.1 or newer. Many shared hosts default to an older version even if a newer one is available — you usually have to opt in via the control panel.
2. **Missing PHP extension.** The CMS setup checks for `json`, `session`, `curl`, and `mbstring`. Some hosts ship a stripped-down PHP build without everything enabled.
3. **The Online Editor config directory is not writable.** Setup needs to save its PHP configuration file on the server.
4. **`.htaccess` syntax error.** If you've recently edited `.htaccess`, comment out your changes and reload — if the error goes away, your rewrite rules are the cause.

The clearest diagnostic is your server's PHP error log. Most control panels expose it; if not, check `/error_log` next to the failing page.

### Content issues

#### The Collection or Item shows nothing on the live site

* Check the **Folder** setting on the component — it must point at a real folder containing `.md` files.
* Check the **Status** filter on the Collection (default: `Published`). If your posts have `status: draft` in their frontmatter, they won't appear.
* Check the **Date** filter (default: `In the past`). Future-dated posts are filtered out unless you switch this to `All dates`.

#### The Item page renders but no item content shows

The slug in the URL doesn't match any file in the configured folder. Verify:

* The Item component's **Folder** points at the correct collection.
* The Markdown filename matches the slug exactly — lowercase, hyphenated, no spaces.
* The visit URL really is `…/post/my-slug` and not `…/post/?item=my-slug` with the wrong slug.

#### Frontmatter values are missing or look wrong

YAML is sensitive to indentation and special characters. Open the Markdown file and check:

* Frontmatter is delimited by `---` on its own line, both above and below the block.
* Strings containing `:`, `@`, `#`, `{}`, or starting with a number are quoted.
* Indentation uses spaces, not tabs.

A quick test: copy the frontmatter into an online YAML validator. If it errors there, it'll error in the CMS.

### Image and resource issues

#### Images show in Preview but not when Published

Filename casing is the most common cause. Elements automatically lowercases filenames during publish to make them web-safe, but if your Markdown references the file with mixed-case (`File-Name.jpg`), the link won't resolve on a case-sensitive Linux server.

Fix it everywhere:

* Rename the resource to lowercase in the Resources area in Elements.
* Update every reference in your Markdown files to match.

See [Embedding Media](../../cms/markdown/embedding-media.md) for the full naming rules.

#### Images uploaded via the Online Editor don't appear in Elements

This is expected — the Online Editor pushes to the server but doesn't sync back into Elements. Files added online won't show in Elements' Resources view.

If you need a file to be visible in both places, upload it from Elements first, publish, and treat the published version as source of truth.

### URL and routing issues

#### Pretty URL pages 404

Most often `mod_rewrite` isn't enabled on your server, or `AllowOverride` is too restrictive for your `.htaccess` to be read. Ask your host to confirm both are enabled.

If `.htaccess` _is_ being read but pretty URLs still 404, double-check the regex in the rewrite rules matches your folder name exactly. See [Pretty URLs](../../cms/pretty-urls.md).

#### Every page load goes through a redirect

The **Pretty URLs** toggle is off on the component generating the links — links are written in the old `?item=slug` form, and the 301 rule is rewriting them to the clean form on every click. Switch the toggle on inside the inspector for the [Collection](../../cms/components/collection.md), [Search](../../cms/components/search.md), or [Tag List](../../cms/components/tag-list.md).

#### CSS or JavaScript breaks after enabling pretty URLs

Your project template is missing the `<base href>` tag, or it's set incorrectly. Set it to `/` if your site is published at the domain root, or `/yourfolder/` for subfolder publishing. See [Pretty URLs](../../cms/pretty-urls.md).

### RSS and sitemap issues

#### The RSS feed doesn't update

The CMS caches the generated RSS file. Force a rebuild by appending `?regenerate_rss=1` to the URL of the page where the Collection lives.

#### The sitemap doesn't update

Same pattern — append `?regenerate_sitemap=1` to the page's URL to force a regeneration.

### Online Editor issues

#### The admin page renders but the editor doesn't load

Check that:

* JavaScript is enabled in the browser.
* The page contains _only_ the Online Editor component, with no Navigation, Footer, or other layout components on the same page.
* Your server meets the [System Requirements](../system-requirements.md).

#### I need to reset the Online Editor installation

To run first-time setup again, delete the Online Editor's `config.php` file from the published site. Back it up first if you might need the current admin account, content folder, resource folder, or workspace settings.

The file lives in the following location:

```
/rw/elements/com.elementsplatform.cms/editor/php/config.php
```

Connect to your server using FTP, SFTP, SSH, or your hosting file manager, delete `php/config.php`, then reload the admin page and complete setup again.

{% hint style="warning" %}
Deleting `config.php` removes the Online Editor setup/configuration, including the admin account and configured folders. It does not delete Markdown content or uploaded resources.
{% endhint %}

See [Resetting the installation](../../cms/components/online-editor.md#resetting-the-installation) for the full Online Editor reset notes.

### Performance and logs

#### Pages feel slow on the first load

The CMS generates RSS, sitemap, and search index files lazily. The first request after a publish does the work; subsequent requests are served from cache. If a particular page consistently feels slow, check the [Log Manager](log-manager.md) for repeated errors that might be retried on every request.

#### Log files are growing quickly

Use the [Log Manager](log-manager.md) to inspect and trim logs. For high-traffic sites, set up a weekly cron job — the same page documents the command and an example crontab entry.

### Still stuck?

If your issue isn't covered here, the most useful diagnostic is almost always the PHP error log on the server. Most control panels expose it directly; if not, look for an `error_log` file next to the failing page or in your account's home directory. The first few lines of a relevant error will usually point straight at the problem.
