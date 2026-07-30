---
description: Let visitors attach files to a form submission
---

# Attachment

Attachment adds a drag-and-drop file field to a Form. It can accept one or several files, restrict file categories, enforce a per-file size limit, and show removable previews.

### How to Use Attachment

You’ll find Attachment under **Forms** in the Components list.

1. Place Attachment inside a [Form](README.md).
2. Enter a short, unique Name.
3. Choose whether it accepts Multiple files.
4. Select the accepted file category and maximum size.
5. Edit the drop-zone and button text on the canvas.
6. Publish and test with files that should pass and fail.

### Component Settings

#### Settings

**Required** is off by default.

{% hint style="warning" %}
In the current release, Attachment’s Required setting is not applied to the published file input. Do not rely on it to prevent an empty submission.
{% endhint %}

**Name** identifies the uploaded field. It is blank by default. Use letters, numbers, hyphens, or underscores.

**Multiple** is off by default. Enable it to accept more than one file.

**Accept** is not responsive and defaults to All File Types. Options are:

* All File Types
* Images
* Videos
* Audio
* Documents
* Zip

Documents include common PDF, Word, Excel, and PowerPoint formats. Zip includes ZIP and 7z-compatible archive types.

**Max File Size** is measured in megabytes per file and defaults to 2.

{% hint style="warning" %}
Webhook submissions send only the first attached file. Multiple attachments are supported with Email delivery.
{% endhint %}

#### Content Layout

**Alignment** offers Start, Centre, or End and defaults to Centre.

**Gap** defaults to theme spacing 4.

**Button Color** defaults to Brand 500.

#### File Previews

**Preview in Edit → Enabled** is on by default and shows a sample preview while designing.

Preview styling defaults:

* **Thumbnail** — Theme spacing 10.
* **Background** — Surface 50.
* **Close** — Red 500.
* **Border Color** — Surface 50.

Set Border Width and Radius using their Theme Studio controls.

### Accessibility

Keep the Select Files text descriptive, state accepted formats and maximum size near the field, and do not communicate upload errors through colour alone.

### Troubleshooting

#### A file is rejected

Check Accept and Max File Size. The browser supplies the file’s MIME type, which must match the selected category.

#### Only one file is retained

Enable Multiple and use Email delivery when every selected file must be sent.

### Related Components

* [Form](README.md) — Configures delivery and validation.
* [Error](error.md) — Displays form-level failure feedback.
* [Submit](submit.md) — Provides the clickable submission control.

{% include "../../../.gitbook/includes/common-controls (1).md" %}
