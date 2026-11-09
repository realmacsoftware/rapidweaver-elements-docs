---
description: Advanced PHP patterns — runtime rendering, @raw tokens, caching, and requiresPhp
---

# Server-Side PHP Components

Most components finish their work before the site is published: hooks compute values, templates resolve, and what ships is static HTML. A server-side component keeps working *after* publish — its output is PHP that runs on the hosting server every time a visitor requests the page. That unlocks live data (a spreadsheet that updates without republishing), content that varies per visitor, and logic that must never run in the browser. This guide covers the patterns that make those components solid: where server-side code can live, what `requiresPhp` really does, how build-time directives and request-time PHP coexist in one file, protecting runtime tokens with `@raw`, caching remote data, and gating content behind a session.

{% hint style="success" %}
This guide dissects the **Table** component (`com.realmacsoftware.table`) from the open-source [Core Pack](../development-resources/open-source-components.md). Open its source alongside this page.
{% endhint %}

## Two Kinds of Server-Side Code

**A `.php` main template.** A component can use `templates/index.php` in place of `index.html` as its main template. The file is processed by the Elements template engine at publish like any other template, but the PHP inside it is deployed to the server and runs *when the published page is requested* — its output becomes part of the page itself. This is the right home for server-rendered markup: tables built from remote data, per-visitor content, anything where the page's HTML depends on request-time state. The [PHP Templates reference](../component/templates/php-templates.md) covers the mechanics — property insertion into PHP, the closure and heredoc patterns, and why edit mode needs a PHP-free branch.

**`templates/backend/` endpoints.** Files in the backend directory are *not* part of the page output. They deploy to a per-page backend folder and are called separately — typically via `fetch()` from your front-end JavaScript — to handle form submissions, AJAX requests, and API-style work. The [Backend reference](../component/templates/backend.md) documents the deployment structure, `node.backendPath`, and a complete contact-form example. This guide doesn't repeat that material; everything below is about the first kind — components whose page output *is* PHP — plus the patterns both kinds share.

## Declaring requiresPhp

A `.php` template only executes if the page that contains it is itself served as PHP. That's what the [`requiresPhp` key in `info.json`](../component/info.json.md) enforces: set it to `true` if your component outputs server-side PHP that needs to run on the hosting page, and the page containing the component is published with a `.php` filename — otherwise the PHP won't be executed. It defaults to `false`, and per the reference it's not needed for child components that only ever appear nested inside another component that already requires PHP.

The Table declares it like this:

```json
// info.json
{
    "identifier": "com.realmacsoftware.table",
    "title": "Table",
    "group": "Content",
    "icon": "icon",
    "requiresPhp": true,
    "helpURL": "../../elements/components/table.md"
}
```

The child-component rule matters most when you build a suite. Imagine a members-area suite: a *Members Area* parent with `requiresPhp: true`, and children — *Member Greeting*, *Logout Button* — designed to be dropped inside it. Only the parent needs the flag: any page holding the parent is already published as `.php`, so children nested inside it get a PHP-capable page for free. But the inherited requirement doesn't travel. If the *Logout Button* can also be placed standalone — say, in a site-wide navigation bar on a page with no *Members Area* — it must declare `requiresPhp: true` itself, or its PHP will ship inside an `.html` page and appear as literal source text.

## Worked Example: The Table's index.php

The Table renders CSV data — a local file or a remote URL — into a styled, sortable table *on the server*, so the published page always reflects the current spreadsheet. Its main template is `templates/index.php`, and it's the best available example of build-time Elements directives and request-time PHP sharing one file. (Its edit-mode branch, which swaps in example rows because PHP can't run in the editor, is covered in [PHP as the Main Template](../component/templates/php-templates.md#php-as-the-main-template-indexphp) — we'll focus on the published-page path.)

### Hooks Prepare Everything PHP Will Need

PHP can't reach into `rw.props`, so the hooks file resolves every setting to a plain string or JSON blob *before* the template is processed. Condensed from `hooks.source.js`:

```javascript
// hooks.source.js (condensed)
const transformHook = (rw) => {
    const {
        globalID,
        // CSV data source
        dataSource,
        csvFile,
        csvUrl,
        csvFirstRowIsHeader,
        // …some seventy styling props omitted…
    } = rw.props;

    const { mode } = rw.project;
    const { id } = rw.node;
    const edit = mode === "edit";

    // CSV data source
    const isCSVMode = dataSource === "csvFile" || dataSource === "csvUrl";
    let csvSource = "";
    if (dataSource === "csvFile") {
        csvSource = csvFile?.path || "";
    } else if (dataSource === "csvUrl") {
        csvSource = csvUrl || "";
    }
    const csvFirstRowHeader = csvFirstRowIsHeader === true || csvFirstRowIsHeader === "true";

    // …classes object, column metadata, and edit-mode example rows omitted…

    rw.setProps({
        id: globalID || id,
        classes,
        edit,
        alpineConfig: JSON.stringify(alpineConfig).replace(/"/g, "'"),
        csvColumnMeta: JSON.stringify(csvColumnMeta),
        // CSV mode
        isCSVMode,
        csvSource,
        csvFirstRowIsHeader: csvFirstRowHeader ? "true" : "false",
        // …edit-mode preview data omitted…
    });
};

exports.transformHook = transformHook;
```

Three details are deliberate. `csvSource` is normalised to a single string whichever source type the user picked, so the template needs no source-type logic. Booleans destined for PHP are serialised as the strings `"true"`/`"false"` — PHP will re-parse them, because a `{{property}}` interpolation is always text by the time PHP sees it. And structured data (`csvColumnMeta`) travels as a JSON string, to be decoded server-side from a heredoc.

### One File, Two Execution Phases

Here is the heart of the published-page branch, trimmed from `templates/index.php`:

```php
<!-- templates/index.php (published-page branch of CSV mode) -->
<div x-data="elementsTable('{{id}}', {{alpineConfig}})">

    @if(showSearch)
    <div>
        <input
            type="text"
            class="{{classes.searchInput}}"
            placeholder="{{searchPlaceholder}}"
            x-model="search"
            @input="onSearchInput()"
        />
    </div>
    @endif

    <?php
    $csvSource = '{{csvSource}}';
    $rawFirstRow = '{{csvFirstRowIsHeader}}';
    $firstRowIsHeader = in_array($rawFirstRow, ['true', '1', 'yes'], true);
    // … column metadata, fetching, and CSV parsing omitted …
    ?>

    <tbody>
        <?php foreach ($csvRows as $rowIdx => $row): ?>
        <tr class="{{classes.tr}}"
            x-ref="row<?php echo $rowIdx; ?>"
            x-show="isRowVisible($el)"
        >
            <!-- … cells rendered with per-column classes … -->
        </tr>
        <?php endforeach; ?>
    </tbody>
```

Read this as two passes over the same text:

1. **Publish time (Elements).** The template engine resolves everything it recognises: `@if(showSearch)` keeps or drops the search block, and every `{{…}}` becomes a literal value — `{{id}}`, `{{alpineConfig}}`, `{{classes.searchInput}}`, `{{csvSource}}`, `{{classes.tr}}`. The `<?php … ?>` blocks are just opaque text to Elements; they pass through untouched (as does Alpine's `@input`/`@click` shorthand, which isn't an Elements directive). The result — now pure PHP-plus-HTML with no directives left — is written into the published site with a `.php` filename, courtesy of `requiresPhp`.
2. **Request time (PHP).** Each time a visitor loads the page, the server executes what publish time produced. `$csvSource = '…';` now assigns the resolved URL, and the `foreach` stamps out one `<tr>` per CSV row.

The `foreach` loop is where the two phases visibly interlock: `{{classes.tr}}` was interpolated *once* at publish, so at request time PHP echoes that same literal class string on every iteration. Build-time values are frozen into the PHP source; request-time values flow through PHP variables. Once that distinction is comfortable, files like this stop looking exotic.

### Fetching the CSV at Request Time

When the source is a URL, the Table fetches it fresh on every request — this excerpt runs inside the `<?php` block elided above:

```php
// Fetch CSV content (try file_get_contents first, fall back to curl)
$csvContent = false;
if (!empty($csvSource)) {
    // Try file_get_contents first (works for local files and URLs if allow_url_fopen is on)
    $csvContent = @file_get_contents($csvSource);

    // Fall back to curl for remote URLs
    if ($csvContent === false && function_exists('curl_init') && preg_match('#^https?://#i', $csvSource)) {
        $ch = curl_init($csvSource);
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
        curl_setopt($ch, CURLOPT_FOLLOWLOCATION, true);
        curl_setopt($ch, CURLOPT_MAXREDIRS, 5);
        curl_setopt($ch, CURLOPT_TIMEOUT, 15);
        curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, true);
        curl_setopt($ch, CURLOPT_USERAGENT, 'Mozilla/5.0');
        $csvContent = curl_exec($ch);
        $httpCode = curl_getinfo($ch, CURLINFO_HTTP_CODE);
        curl_close($ch);
        if ($httpCode < 200 || $httpCode >= 400) {
            $csvContent = false;
        }
    }
}
$csvError = ($csvContent === false);
```

Two lessons here. First, hosting environments differ: `allow_url_fopen` is off on plenty of shared hosts, so the curl fallback isn't paranoia, it's compatibility. Second, failure is a first-class outcome — `$csvError` drives a friendly "Unable to load CSV data" table instead of a blank page or a PHP warning. (The full file also rewrites Google Sheets share URLs into their CSV-export form before fetching — worth reading in the source.) What the Table deliberately *doesn't* do is cache: every request pays for the fetch. For a table that's fine; for slower APIs, see [Caching Remote Data on the Server](#caching-remote-data-on-the-server) below.

## Runtime Token Substitution with @raw

The Table interleaves PHP echo statements with markup. An alternative pattern — common in data-driven components — is to keep a clean markup *sub-template* with `{{name}}`-style tokens, and have PHP fill the tokens in a loop with `str_replace` at request time. One template string, one substitution call per row, no PHP tangled through the markup.

The catch: `{{name}}` is exactly the syntax Elements resolves at publish. Left unprotected, Elements would try to find a property called `name` and replace it — your tokens are consumed at build, PHP's `str_replace` finds nothing to replace at request time, and every card renders blank. The fix is the [`@raw` directive](../component/language/raw.md): content between `@raw()` and `@endraw` skips template processing entirely and ships to the server as literal text. And note it's *every* literal occurrence of the token text that needs protecting — including the token list inside your PHP `str_replace` call, not just the markup.

Here's the pattern as a fresh component, `com.example.productlist`, which renders product cards from a remote JSON API at request time (its `info.json` sets `requiresPhp: true`):

```javascript
// hooks.js
exports.transformHook = (rw) => {
    const { mode } = rw.project;
    const { apiUrl, cacheMinutes } = rw.props;

    rw.setProps({
        edit: mode === "edit",
        apiUrl: apiUrl || "",
        cacheSeconds: (parseInt(cacheMinutes) || 15) * 60,
        classes: {
            grid: "grid gap-6 md:grid-cols-3",
            card: "rounded-lg border border-gray-200 p-4",
            image: "mb-3 w-full rounded",
            title: "text-lg font-semibold",
            price: "text-sm opacity-70",
        },
    });
};
```

```php
<!-- templates/index.php -->
@if(edit)
<!-- PHP can't run in the editor — show a placeholder card instead -->
<div class="{{classes.grid}}">
    <article class="{{classes.card}}">
        <h3 class="{{classes.title}}">Example Product</h3>
        <p class="{{classes.price}}">£19.00</p>
    </article>
</div>
@else
<?php
// Resolved by Elements at publish, before this file reaches the server
$apiUrl       = '{{apiUrl}}';
$cacheSeconds = {{cacheSeconds}};
$gridClasses  = '{{classes.grid}}';
$cardClasses  = '{{classes.card}}';
$imageClasses = '{{classes.image}}';
$titleClasses = '{{classes.title}}';
$priceClasses = '{{classes.price}}';
?>
@raw()
<?php
// Everything below runs at request time. The heredoc interpolates the
// PHP class variables; the {{token}} placeholders survive the publish
// step because this whole block sits inside @raw.
$cardTemplate = <<<CARD
<article class="$cardClasses">
    <img class="$imageClasses" src="{{image}}" alt="{{name}}">
    <h3 class="$titleClasses">{{name}}</h3>
    <p class="$priceClasses">{{price}}</p>
</article>
CARD;

$json = $fetchJsonCached($apiUrl, $cacheSeconds); // helper — next section
$products = json_decode($json !== false ? $json : '', true);
if (!is_array($products)) {
    $products = [];
}

echo '<div class="' . $gridClasses . '">';
foreach ($products as $product) {
    echo str_replace(
        ['{{name}}', '{{price}}', '{{image}}'],
        [
            htmlspecialchars($product['name'] ?? '', ENT_QUOTES, 'UTF-8'),
            htmlspecialchars($product['price'] ?? '', ENT_QUOTES, 'UTF-8'),
            htmlspecialchars($product['image'] ?? '', ENT_QUOTES, 'UTF-8'),
        ],
        $cardTemplate
    );
}
echo '</div>';
?>
@endraw
@endif
```

The split is the whole trick. Everything Elements should resolve — the API URL, the cache TTL, the class strings — is assigned to PHP variables *outside* the `@raw` block, so it's frozen into the deployed file at publish. Everything PHP owns — the card template with its `{{name}}`/`{{price}}`/`{{image}}` tokens, the fetch, the loop — sits *inside* `@raw`, so it reaches the server byte-for-byte intact. The heredoc bridges the two: PHP interpolates `$cardClasses` at request time, while the `{{…}}` tokens wait for `str_replace`. (If you'd rather keep Elements values inline in the raw markup instead of routing them through variables, `@raw` blocks can be exited and re-entered mid-stream — see [Combining with Elements Properties](../component/language/raw.md#combining-with-elements-properties).)

### Tailwind Can't See Request-Time Classes

One side effect of rendering markup at request time: Tailwind's JIT engine only compiles classes it finds in your template files at build or preview time. The classes above are safe — they're literal strings in `hooks.js` and the template — but any Tailwind class that first *appears* at request time (composed by PHP logic, or arriving from the API data) will have no CSS behind it. The documented workaround is to list those classes in an HTML comment in a template file so the JIT scan picks them up — see [Troubleshooting: Dynamic PHP Code and Tailwind Classes Generation](../getting-started/troubleshooting.md#dynamic-php-code-and-tailwind-classes-generation).

## Caching Remote Data on the Server

Fetching a remote API on every page view makes your page as slow — and as fragile — as the API. A small file cache with a TTL fixes both: fetch at most once every N minutes, and if the remote is down, serve the last good copy instead of an empty page. Here's the `$fetchJsonCached` helper the product list uses; paste it at the top of the same `@raw` PHP block, before the card template (it contains no `{{…}}` tokens, so `@raw` neither helps nor hurts it — placement inside is simply convenient):

```php
<?php
// Fetch remote JSON at most once per TTL; serve stale data on failure.
// A closure, not a named function, so two instances of the component
// on one page can't cause a "cannot redeclare" fatal error.
$fetchJsonCached = function ($url, $ttlSeconds) {
    $cacheFile = sys_get_temp_dir() . '/rw-cache-' . md5($url) . '.json';

    // Fresh enough? Serve the cached copy without touching the network.
    if (is_readable($cacheFile) && (time() - filemtime($cacheFile)) < $ttlSeconds) {
        return file_get_contents($cacheFile);
    }

    // Stale or missing — try the network.
    $context = stream_context_create(['http' => ['timeout' => 10]]);
    $body = @file_get_contents($url, false, $context);

    // Only accept responses that parse as JSON.
    if ($body !== false && json_decode($body) !== null) {
        @file_put_contents($cacheFile, $body, LOCK_EX);
        return $body;
    }

    // Fetch failed — a stale copy beats an empty page.
    if (is_readable($cacheFile)) {
        return file_get_contents($cacheFile);
    }

    return false;
};
?>
```

Details worth keeping: the cache lives in `sys_get_temp_dir()`, which is writable on virtually every host and outside the web root, so the raw cache file is never served publicly; the key is an `md5` of the URL, so two components fetching different feeds never collide; and a response is only cached if it actually parses as JSON, so one bad gateway page can't poison the cache. The closure-not-named-function rule is the same one the Table follows — root-level templates are processed once per instance, and named functions would be declared twice when two instances share a page. If your data outgrows a flat JSON file — thousands of rows, per-record lookups, concurrent writes — PHP's bundled SQLite via PDO is the natural next step, and the caching idea carries over unchanged.

## Session-Gated Content

Because a `.php` main template runs per request, it can also decide *whether to render at all*. The sketch below wraps a dropzone in a PHP session check on the published site, while leaving it always visible (and editable) in the editor — note how the `@if(!edit)` blocks emit only the PHP *wrapper* around the dropzone, so the dropzone itself appears exactly once in the template:

```php
<!-- templates/index.php -->
@if(!edit)
<?php if (session_status() === PHP_SESSION_NONE) { session_start(); } ?>
<?php if (!empty($_SESSION['{{sessionKey}}'])): ?>
@endif

@dropzone("protected", title: "Protected Content")

@if(!edit)
<?php else: ?>
<p class="{{classes.notice}}">This content is for members only.</p>
<a class="{{classes.link}}" href="{{loginPath}}">Log in</a>
<?php endif; ?>
@endif
```

At publish, the editor path drops the PHP entirely; the published path becomes a plain PHP `if`/`else` around the dropzone's rendered children. Two scope notes. `session_start()` must run before the page sends output, so a component like this belongs early in the page — or better, let the login endpoint own session creation and keep the template to reading `$_SESSION`. And the login itself — the form, password hashing, verification, setting the session flag — is a job for a `templates/backend/` endpoint, which is exactly the request/response flow the [Backend reference](../component/templates/backend.md) documents.

## Paths Cheat-Sheet

Server-side components juggle more paths than most. These are the documented members, from the [rw.node](../component/hooks.js/available-data/rw.node.md), [rw.page](../component/hooks.js/available-data/rw.page.md), and [rw.component](../component/hooks.js/available-data/rw.element.md) reference pages:

| Member                          | Documented meaning                   | Reach for it when…                                                                                                        |
| ------------------------------- | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------- |
| `rw.node.backendPath`           | Path to the node's backend folder    | your front-end `fetch()`es a `templates/backend/` endpoint — this is the per-page folder those files deploy into           |
| `rw.page.absolutePath`          | Full path to the page                | you need the location of the page itself, e.g. building a link or redirect back to it                                      |
| `rw.page.docRootPath`           | Path to document root                | server-side code needs to reach files elsewhere in the published site, relative to the site root                           |
| `rw.component.assetPath`        | Path to component-specific assets    | referencing files bundled with this component (images, scripts, styles)                                                    |
| `rw.component.siteAssetPath`    | Path to site-level component assets  | `require_once`-ing a shared PHP library deployed with the site — the pattern both PHP reference pages use                  |
| `rw.component.sharedAssetPath`  | Path to shared pack assets           | referencing files shared across the whole Element Pack                                                                     |

To use any of these in a template, pass them through from `hooks.js` — `rw.setProps({ node: rw.node, siteAssetPath: rw.component.siteAssetPath })` — as the [Backend reference](../component/templates/backend.md#using-nodebackendpath) shows; see [Passing Data to Templates](../component/hooks.js/passing-data-to-templates.md).

## A Note on Escaping

{% hint style="warning" %}
Everything that arrives at request time is untrusted — CSV cells, API JSON, query strings, session-adjacent input. Escape it at the point of output with `htmlspecialchars($value, ENT_QUOTES, 'UTF-8')`. The `ENT_QUOTES` flag matters whenever a value lands inside an HTML *attribute* (`src`, `alt`, `class`, `value`), where an unescaped quote lets data break out of the attribute. The Table is the model here: it escapes every CSV header, every cell, and every composed class string before echoing. Build-time property values resolved by Elements are your own configuration; request-time data never is.
{% endhint %}

## Related Documentation

* [PHP Templates](../component/templates/php-templates.md) — root-level PHP and `index.php` as the main template
* [Backend Directory](../component/templates/backend.md) — request handlers called via `fetch()`
* [@raw](../component/language/raw.md) — shipping literal `{{…}}` tokens through the build
* [info.json](../component/info.json.md) — `requiresPhp` and the component manifest
* [External Data Sources](./external-data-sources.md) — pulling remote data into components
* [Building Form Components](./building-form-components.md) — inputs, validation, and submission handling
* [Troubleshooting](../getting-started/troubleshooting.md) — the PHP + Tailwind JIT gotcha
