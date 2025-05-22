---
description: Learn how to setup pretty URLs for your CMS Collections.
---

# Pretty URLs

## <sub>Clean URL Redirection & Routing with .htaccess</sub>

This guide explains how to use Apache’s .htaccess to:

1. **Redirect** URLs like /post/?slug=some-post to /post/some-post/
2. **Internally rewrite** /post/some-post/ to /post/index.php?slug=some-post
3. Support both **single-route** and **multi-route** setups

### Option 1: Single Route (e.g. /post/ only)

Use this if you’re only applying the redirect/rewrite logic to one route like `/post/`

#### .htaccess Example:

```apacheconf
RewriteEngine On

# 1. Redirect /post/?slug=some-post to /post/some-post/
RewriteCond %{THE_REQUEST} \s/post/\?slug=([^&\s]+) [NC]
RewriteRule ^post/$ /post/%1/ [R=301,L]

# 2. Internally rewrite /post/some-post/ to /post/index.php?slug=some-post
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^post/([^/]+)/?$ /post/index.php?slug=$1 [L,QSA]
```

#### How it works:

**Redirect Rule (Human-Friendly URLs)**

* Matches incoming requests like `/post/?slug=some-post`
* `%{THE_REQUEST}` ensures it only triggers on direct browser requests, not rewrites
* Redirects to: `/post/some-post/` using captured value `%1`

**Rewrite Rule (Internal Routing)**

* Matches URLs like `/post/some-post/`
* Internally rewrites to `index.php?slug=some-post`
* Uses `!-f` and `!-d` checks to avoid rewriting actual files or directories
* QSA preserves any additional query parameters (like UTM tags)



### Option 2: Multi-Route Support (e.g. /post/, /notes/, /blog/, etc.)

Use this if you want the same functionality across multiple sections without duplicating rules.

#### .htaccess Example:

```apacheconf
RewriteEngine On

# 1. Redirect /section/?slug=some-slug → /section/some-slug/
RewriteCond %{THE_REQUEST} \s/([^/?]+)/\?slug=([^&\s]+) [NC]
RewriteRule ^ %1/%2/ [R=301,L]

# 2. Internally rewrite /section/some-slug/ → /section/index.php?slug=some-slug
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^([^/]+)/([^/]+)/?$ /$1/index.php?slug=$2 [L,QSA]
```

#### How it works:

**Redirect Rule (Dynamic Section Matching)**

* Matches `/something/?slug=some-slug`
* `([^/?]+)` captures the section name (e.g., post, notes)
* `([^&\s]+)` captures the slug
* Redirects to `/section/slug/`

**Rewrite Rule (Flexible Routing)**

* Matches `/section/slug/`
* Internally rewrites to `/section/index.php?slug=slug`
* Works for any folder that uses index.php to handle dynamic slugs

#### Example Requests:

| **Request**             | **Redirected To**  | **Internally Rewritten To**      |
| ----------------------- | ------------------ | -------------------------------- |
| /post/?slug=week-1      | /post/week-1/      | /post/index.php?slug=week-1      |
| /notes/?slug=update     | /notes/update/     | /notes/index.php?slug=update     |
| /blog/?slug=first-entry | /blog/first-entry/ | /blog/index.php?slug=first-entry |

### Notes and Best Practices

* Place .htaccess in your site root, unless you’re scoping it to a subfolder.
* Make sure mod\_rewrite is enabled on your Apache server.
* Use \[R=301,L] for permanent redirects (cached by browsers).
* The QSA flag (Query String Append) ensures extra parameters aren’t lost.
* Ensure your index.php files handle $\_GET\['slug'] properly.

### Debugging Tips

* If you see errors like `AH00124: Request exceeded the limit of 10 internal redirects`, it likely means you are rewriting the same request repeatedly.
* Use `RewriteCond %{REQUEST_FILENAME} !-f` and `!-d` to prevent rewriting actual files or folders.
