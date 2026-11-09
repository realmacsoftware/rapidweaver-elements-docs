---
description: Add a moderated comments thread to your CMS items.
hidden: true
---

# Comments

The **Comments** component adds a comments section to your CMS items, with a built-in submission form, server-side storage, and a moderation queue. It's designed to drop straight into a blog post page without any third-party services or accounts.

Comments are moderated by default — submissions don't appear publicly until they've been approved.

{% hint style="success" %}
The Comments component must be placed **inside an** [**Item**](item.md) **component**. It needs the current item's slug to know which thread to load and where to file new submissions.
{% endhint %}

### What gets rendered

The component outputs three things, in order:

1. **A heading** with the approved comment count (optional).
2. **The list of approved comments** for this item, oldest first, with author name and timestamp.
3. **A submission form** with fields for name, email, and comment body, plus a hidden honeypot for basic spam protection.

When there are no approved comments yet, the list area shows a friendly "No comments yet" message above the form.

### Settings

Open the inspector for the Comments component to configure:

* **Comments Heading** — the heading shown above the thread. Default: `Comments`. Leave empty to hide both the heading and the empty-state message.
* **Form Heading** — the heading shown above the submission form. Default: `Leave a Comment`. Leave empty to hide it.
* **Success Message** — the confirmation shown after a submission is accepted. Default: `Thank you! Your comment is awaiting approval.`
* **Show Comment Count** — toggles a numeric `(n)` next to the heading. Default: on.

The Advanced group exposes the usual **Classes** and **ID** fields if you need to attach custom styling or anchor links.

### Where comments are stored

Submissions are written to a file alongside your CMS content on the server. The component looks the file up by the parent Item's collection path and slug, so as long as the comments live under the same collection folder they'll travel with the post.

There is no database. Comments are plain data on disk, just like the rest of your CMS content.

### Moderation

Every submission lands in a pending state. To approve, edit, or delete comments, open the [Online CMS Editor](../../online-cms-editor/) and use its moderation views. Approved comments appear on the published page on the next request.

{% hint style="info" %}
The submission form includes a hidden honeypot field and a load-time stamp to filter out the most obvious bot traffic. It is not a substitute for moderation — review every comment before approving it.
{% endhint %}

### Styling

The component renders semantic HTML with stable class names so you can target it directly in your project's CSS or Tailwind classes:

* `.cms-comments` — the outer wrapper.
* `.cms-comments-heading` and `.cms-comments-count` — heading and count.
* `.cms-comments-list` and `.cms-comment` — the thread.
* `.cms-comment-meta`, `.cms-comment-author`, `.cms-comment-date`, `.cms-comment-body` — per-comment parts.
* `.cms-comments-form-wrapper`, `.cms-comments-form`, `.cms-comments-field`, `.cms-comments-submit`, `.cms-comments-message` — the form.
* `.cms-comments-message-success` and `.cms-comments-message-error` — submission feedback states.

If you'd prefer to keep all your typography styling in a single place, applying a Tailwind class like `prose` (or your equivalent) to the parent Item often gets you a long way for free.

### In-edit preview

Inside Elements, the Comments component renders a small placeholder explaining that comments will only appear on the published page. This is intentional — the component depends on a real server with the CMS API installed, so the live thread can't be shown during editing.

### Common issues

**"No item found" appears instead of the thread.**\
The Comments component isn't inside an Item. Move it into the Item component (typically the After drop zone, below the post body).

**Submissions appear successful but never show up publicly.**\
That's expected — comments wait for approval. Sign into the [Online CMS Editor](../../online-cms-editor/) to moderate them.

**The form submits but reports a generic error.**\
Check that the page extension is `.php`, and that the server meets the [System Requirements](../../getting-started/system-requirements.md). The form posts to the CMS API endpoint, which won't be present on a plain HTML host.
