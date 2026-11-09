---
description: Script bulk create, update, and delete operations against CMS content.
icon: arrows-rotate
---

# Content Migration

Use the REST API for scripted bulk operations, such as importing posts from another CMS or backfilling a new frontmatter field across every item.

### Set up a dedicated key

Create a key bound to a user used only for migrations. If something goes wrong, you can revoke that key without affecting other integrations.

### Keep scripts idempotent

Re-running the same migration should not create duplicate items. The safest pattern is:

1. Read by slug.
2. If the item exists, `PATCH` it.
3. If it does not exist, `POST` to create it.
4. Store a custom frontmatter marker, such as `imported_from: wordpress-v1`, so partial runs are easy to resume.

```js
async function upsertPost(post) {
    const slug = post.slug;
    const read = await fetch(`${base}/cms/collections/blog/items/${slug}`, {
        headers: { Authorization: `Bearer ${key}` },
    });

    const body = {
        slug,
        fm: {
            title: post.title,
            status: post.status || 'draft',
            imported_from: 'wordpress-v1',
            ...post.frontmatter,
        },
        body: post.body || '',
    };

    if (read.status === 404) {
        await fetch(`${base}/cms/collections/blog/items`, {
            method: 'POST',
            headers: {
                Authorization: `Bearer ${key}`,
                'Content-Type': 'application/json',
            },
            body: JSON.stringify(body),
        });
    } else if (read.ok) {
        await fetch(`${base}/cms/collections/blog/items/${slug}`, {
            method: 'PATCH',
            headers: {
                Authorization: `Bearer ${key}`,
                'Content-Type': 'application/json',
            },
            body: JSON.stringify(body),
        });
    } else {
        throw new Error(`Read failed: ${read.status}`);
    }
}
```

### Throttle large imports

Version 1 does not impose per-key API rate limits, but your web server and PHP-FPM still have limits. Avoid firing hundreds of requests at once. Cap concurrency:

```js
import pLimit from 'p-limit';

const limit = pLimit(4);
await Promise.all(posts.map(post => limit(() => upsertPost(post))));
```

### Dry-run destructive changes

Before running destructively, print how many records your script would touch and show a sample. `DELETE` has no undo. Version history covers item content changes, but not deletes.

### Handle failures mid-run

Public read routes use the API envelope. Authenticated editor-bridged routes return either a JSON object or `{ "error": "..." }`, so check both HTTP status and body:

```js
const res = await fetch(url, { headers });
const body = await res.json();

if (!res.ok || body.error || body.success === false) {
    const reason = body.error || 'Request failed';
    failures.push({ post, reason, status: res.status });
}
```

If a script stops halfway through, run it again. Idempotent upserts should converge.

### Large uploads

For migrations that include media, send multipart uploads to `/cms/resources`. See [Uploads](uploads.md).
