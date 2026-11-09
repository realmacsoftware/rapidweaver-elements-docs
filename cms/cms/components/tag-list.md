---
description: Display every tag used in a Collection, with optional post counts.
hidden: true
---

# Tag List

The **Tag List** component renders every tag found in a CMS collection as a list of links, optionally with the number of posts that use each tag. Combined with a tag page that filters posts by tag, it's the building block for a "Browse by topic" sidebar or a tag cloud.

Unlike a Collection, the Tag List doesn't render posts — it renders the _set of tags_ used across them. Each entry links to the tag page you've configured, with the tag's slug appended to the URL.

### How tags are collected

The component scans every Markdown file in the chosen collection folder and gathers the `tags` value from each frontmatter block. Tags are deduplicated case-insensitively, so `Design`, `design`, and `DESIGN` all collapse to one entry.

If you have a dedicated `tags/` folder alongside your posts (with one Markdown file per tag), the related-data lookup automatically pulls in any extra metadata you've defined there — for example, a description or a cover image. See [Template Data](../template-data.md) for how the related lookups work.

### Settings

The inspector for the Tag List component is grouped into three panels.

#### Settings group

* **Folder** — the CMS folder containing the posts whose tags should be aggregated. Tags are read from each post's frontmatter.
* **Tag Page** — the page that displays posts filtered by tag. Each tag entry links here, with the tag slug appended.
* **Pretty URLs** — when enabled, tag links are written as `/tag/design` instead of `/tag/?item=design`. Requires an `.htaccess` rule. See [Pretty URLs](../pretty-urls.md).
* **Show Count** — toggles a numeric `(n)` showing how many posts use each tag. Default: on.
* **Hide Empty Tags** — when **Show Count** is on, hides tags that exist in your `tags/` folder but aren't used by any published post. Useful while you're still drafting content.

#### Columns & Rows group

* **Gap** — horizontal and vertical spacing between tag entries.
* **Columns** — lay tags out in a grid of 1–12 columns. Set to 1 for a vertical list, higher values for a chip-style cloud.

#### Advanced group

The usual **Classes** and **ID** fields for custom styling and anchor links.

### Designing the tag template

The Tag List has a single drop zone called **Tag**. Anything you place there is rendered once per tag, with the current tag's data exposed through `{{tag.*}}` references:

* `{{tag.name}}` — the tag's name (matches whatever is in the post frontmatter, with case preserved from the first occurrence).
* `{{tag.url}}` — the link to the tag page, already accounting for Pretty URLs.
* `{{tag.count}}` — the number of published posts using this tag (only populated when **Show Count** is enabled).

If you have a `tags/` folder with per-tag Markdown files, any frontmatter you've defined on those files is also accessible — for example `{{tag.description}}` or `{{tag.image.src}}`.

A common layout is a Link component bound to `{{tag.url}}`, containing a Heading bound to `{{tag.name}}` and a small Text component bound to `{{tag.count}}`.

### Filtering with `Hide Empty Tags`

When you have a curated `tags/` folder, some tags may not yet appear in any published post — perhaps you've drafted the tag's metadata before writing the first post. By default those still show up with a count of zero. Toggle **Hide Empty Tags** to suppress them.

This setting only kicks in when **Show Count** is on, because it relies on the per-tag count to know which entries to drop.

### Common issues

**No tags appear, even though my posts have tags.**\
Confirm the **Folder** setting points at the correct collection. The Tag List reads `tags:` from the frontmatter of every Markdown file in that folder.

**The tag links go to a 404.**\
Either the **Tag Page** isn't set, or Pretty URLs is enabled without the matching `.htaccess` rule. See [Pretty URLs](../pretty-urls.md).

**A tag appears multiple times with different casings.**\
Tags are deduplicated case-insensitively, so this shouldn't happen. If it does, look for non-printing characters in the frontmatter (a stray space or curly quote) — those will read as different strings.
