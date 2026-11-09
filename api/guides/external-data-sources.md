---
description: Feed components from CSV files, remote URLs, and other external data
---

# External Data Sources

Most components render content the user typed into RapidWeaver. Some of the most useful ones render content that lives somewhere else entirely — a spreadsheet exported as CSV, a Google Sheet the client edits, a JSON API that changes hourly. For these components the hard design question isn't *how* to parse the data; it's *where* the ingestion should happen. Pick the wrong place and you either freeze live data at publish time or ship a component that renders nothing without JavaScript. This guide maps the options, then walks through how the core Table component wires up all of its data-source modes.

{% hint style="success" %}
This guide dissects the **Table** component (`com.realmacsoftware.table`) from the open-source [Core Pack](../development-resources/open-source-components.md). Open its source alongside this page.
{% endhint %}

## Choosing an Ingestion Point

Component code runs in three different places, and each one is a possible ingestion point with different reach:

| Ingestion point | Where it runs | What it can reach | Choose it when |
| --- | --- | --- | --- |
| **Build time** — `hooks.js` | Inside RapidWeaver, on every canvas render and at publish | Only what the project already knows, through the `rw` object: `rw.props`, `rw.collections`, resources, `rw.pages` | The data ships with the project — inspector values, collection items, or a dropped file whose *path* you need |
| **Request time** — PHP in `templates/index.php` or `templates/backend/` | On the web server, every time a visitor requests the page | The server's filesystem and remote URLs | The data changes independently of publishing, and you want it delivered as plain HTML — no JavaScript required, visible to search engines |
| **View time** — `fetch` in the browser | In the visitor's browser, after the page loads | Any endpoint that permits cross-origin requests | The data should be as fresh as the current page view, or the fetch depends on visitor interaction |

The build-time row deserves emphasis, because it's the one developers most often get wrong: **hooks cannot fetch over the network.** The hooks runtime is a closed sandbox — no `require`, no `import`, no `fetch`. A hook can transform anything the `rw` object hands it, and nothing else. The core Table is the proof: even in its CSV URL mode, the hook never touches the URL. It passes the string through as a prop and lets PHP do the fetching at request time. That's not a workaround — it's the right design. Data ingested at build time would be frozen into the published HTML until the next publish, which defeats the point of a remote source.

So the division of labour for every external-data component looks the same: **the hook decides and normalises, the template ingests.** The hook reads the inspector, works out which source is active, and reduces it to simple strings and booleans; the PHP or browser code downstream does the actual I/O.

## Worked Example: Table's Three Modes

Table supports three data sources behind a single select control: rows edited manually on the canvas, a CSV file dropped into the project, or a remote CSV URL.

### One Select, Three Sources

The inspector side is a `select` plus two source controls that swap in and out with `visible` bindings — a `resource` dropwell for the file mode, a plain `text` field for the URL mode:

```json
// properties.config.json (Settings group, trimmed)
[
    {
        "title": "Data Source",
        "id": "dataSource",
        "responsive": false,
        "select": {
            "default": "manual",
            "items": [
                { "title": "Manual", "value": "manual" },
                { "title": "CSV File", "value": "csvFile" },
                { "title": "CSV URL", "value": "csvUrl" }
            ]
        }
    },
    {
        "title": "CSV File",
        "id": "csvFile",
        "visible": "dataSource == 'csvFile'",
        "resource": {}
    },
    {
        "title": "CSV URL",
        "id": "csvUrl",
        "visible": "dataSource == 'csvUrl'",
        "responsive": false,
        "text": {
            "default": "",
            "subtitle": "Any URL that returns CSV data, or a Google Sheets link"
        }
    },
    {
        "title": "Enable",
        "id": "csvFirstRowIsHeader",
        "visible": "dataSource != 'manual'",
        "responsive": false,
        "switch": { "default": true }
    }
]
```

Note what stays constant across modes: the columns [collection](../component/collections/README.md). In manual mode each collection item *is* a column of editable cells; in the CSV modes the same items restyle the incoming data positionally — the config even tells the user so: "Each column item controls the matching CSV column by position (1st item → 1st column)." External data replaces the *content*, not the user's styling decisions.

### The Hook Routes, It Doesn't Fetch

The hook's entire contribution to CSV mode is normalisation. A [resource control](../component/properties.json/ui-controls/resource.md) delivers an object, so the file mode reads `.path`; the URL mode is already a string. Both collapse into one `csvSource` prop, alongside booleans the template can branch on:

```javascript
// hooks.source.js
const transformHook = (rw) => {
    const { dataSource, csvFile, csvUrl, csvFirstRowIsHeader } = rw.props;
    // …

    // CSV data source
    const isCSVMode = dataSource === "csvFile" || dataSource === "csvUrl";
    let csvSource = "";
    if (dataSource === "csvFile") {
        csvSource = csvFile?.path || "";
    } else if (dataSource === "csvUrl") {
        csvSource = csvUrl || "";
    }
    const csvFirstRowHeader = csvFirstRowIsHeader === true || csvFirstRowIsHeader === "true";

    // …
    rw.setProps({
        // …
        isCSVMode,
        isCSVFile: dataSource === "csvFile",
        isCSVUrl: dataSource === "csvUrl",
        csvSource,
        csvFirstRowIsHeader: csvFirstRowHeader ? "true" : "false",
    });
};

exports.transformHook = transformHook;
```

Two details are worth copying. Remember that template `@if` takes a single condition, so compound decisions like "is either CSV mode active" are computed here, once, and passed down as booleans. And `csvFirstRowIsHeader` is deliberately re-emitted as the *string* `"true"` or `"false"` — it's about to be interpolated into PHP source code, where a bare boolean would be fragile.

### The Fetch Happens in PHP, at Request Time

Table's main template is `templates/index.php` rather than `index.html`, which means the component's `info.json` must declare [`requiresPhp`](../component/templates/php-templates.md#declare-requiresphp-in-infojson) so the page publishes with a `.php` extension. Inside the published (non-edit) branch, the interpolated `csvSource` is finally used — and this is where the network I/O actually lives:

```php
<!-- templates/index.php (published CSV branch, trimmed) -->
<?php
$csvSource = '{{csvSource}}';
$rawFirstRow = '{{csvFirstRowIsHeader}}';
$firstRowIsHeader = in_array($rawFirstRow, ['true', '1', 'yes'], true);

// … Google Sheets share links are rewritten to their CSV-export form here …

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
?>
```

The same code path serves both CSV modes: for a file resource, `csvSource` is a local path and `file_get_contents` reads it straight off the published site's disk; for a URL, it's an HTTP fetch with a hardened curl fallback (redirect limit, timeout, TLS verification, status-code check). When everything fails, `$csvError` flips and the template renders a single friendly "Unable to load CSV data" row instead of a broken page — an error state your component should always have, because the remote end *will* be down someday.

There's a convenience layer worth noting even though it's elided above: before fetching, Table detects `docs.google.com/spreadsheets` share links and rewrites them into the sheet's CSV export URL, so users can paste the link they already have. Meeting users at the URL they actually possess is a small amount of code for a large usability win.

Also notice the cost model: this fetch happens on **every page request**, and the visitor waits up to the 15-second timeout if the origin is slow. For high-traffic pages or slow APIs, cache the response server-side — the pattern is covered in [Server-Side PHP Components](server-side-php-components.md).

### The Canvas Never Sees the Real Data

PHP doesn't execute in the RapidWeaver editor, so on the canvas the CSV branch renders a fabricated preview instead: the hook builds `column_a`-style headers and five sample rows sized to the user's column collection, and the template's `@if(edit)` branch renders them through the *same* class props as the live table, under a dimmed "Example data" caption. The full excerpt and the rules that make preview data trustworthy are in [Designing the Edit-Mode Experience](edit-mode-experience.md#preview-datasets) — read that section before shipping any external-data component.

## Parsing CSV Honestly

CSV looks trivial and isn't: fields can be quoted, quoted fields can contain delimiters and quotes, the first row may or may not be data — and the delimiter itself depends on where the file was made. US/UK spreadsheet apps export comma-separated files, but most EU locales use the comma as the decimal separator, so Numbers and Excel there export *semicolon*-separated files; tab-separated exports exist too. Table leans on PHP's built-in `str_getcsv` rather than a hand-rolled `explode`, and sniffs the delimiter before parsing:

```php
<!-- templates/index.php (continued) -->
<?php
// EU-locale Numbers/Excel exports separate fields with semicolons (and
// TSVs with tabs), so sniff the delimiter instead of assuming commas.
// A candidate wins outright when it splits every sampled row into the
// same number of fields (more than one). Semicolon and tab are checked
// before comma: a file that consistently splits on them is never a plain
// comma CSV, while EU decimal commas ("10,5") can fake a comma split.
$tableDetectDelimiter = function ($lines) {
    $sample = [];
    foreach ($lines as $line) {
        if (trim($line) !== '') {
            $sample[] = $line;
            if (count($sample) === 10) {
                break;
            }
        }
    }
    $fallback = ',';
    $fallbackFields = 0;
    foreach ([';', "\t", ','] as $candidate) {
        $counts = [];
        foreach ($sample as $line) {
            $counts[] = count(str_getcsv($line, $candidate, '"', '\\'));
        }
        if (!empty($counts) && $counts[0] > 1 && count(array_unique($counts)) === 1) {
            return $candidate;
        }
        if (array_sum($counts) > $fallbackFields) {
            $fallbackFields = array_sum($counts);
            $fallback = $candidate;
        }
    }
    return $fallback;
};

if (!$csvError) {
    // Excel's "CSV UTF-8" export prepends a BOM that would otherwise
    // leak into the first header cell
    if (strncmp($csvContent, "\xEF\xBB\xBF", 3) === 0) {
        $csvContent = substr($csvContent, 3);
    }

    // Parse CSV content
    $allRows = [];
    $lines = preg_split('/\r\n|\r|\n/', $csvContent);
    $delimiter = $tableDetectDelimiter($lines);
    foreach ($lines as $line) {
        $parsed = str_getcsv($line, $delimiter, '"', '\\');
        if ($parsed !== [null]) {
            $allRows[] = $parsed;
        }
    }

    if ($firstRowIsHeader && count($allRows) > 0) {
        $csvHeaders = array_shift($allRows);
    }
    $csvRows = $allRows;
}
?>
```

What this buys and what it costs:

* **Delimiters are detected, not assumed.** The sniffer samples up to ten non-empty lines and asks, for each candidate, whether it splits every sampled line into the same number of fields (more than one). Real spreadsheet exports are rectangular, so the true delimiter passes this test and text noise doesn't: a stray semicolon in one cell of a comma CSV fails the consistency check. Semicolon and tab are tried before comma because the reverse ordering loses on EU numeric data — in a file like `1,5;2,3`, decimal commas produce a perfectly consistent comma split too, and only the priority order picks the right one. When nothing is consistent (a ragged file), the candidate that yields the most fields overall wins, defaulting to comma.
* **Quoted fields work.** Within a line, `str_getcsv` correctly handles `"Smith, Jane"` as one field — and once the delimiter is known, the same holds for `"x; y"` in a semicolon file — including escaped quotes, the cases that break naive `explode(",", $line)` parsers.
* **Blank lines are dropped.** `str_getcsv` returns `[null]` for an empty line; the `!== [null]` check filters them out instead of rendering ghost rows.
* **Line endings and BOMs are normalised.** Splitting on `/\r\n|\r|\n/` keeps Windows Excel's CRLF endings from smuggling a `\r` into the last cell of every row, and stripping the UTF-8 byte-order mark keeps Excel's "CSV UTF-8" export from polluting the first header cell.
* **Headers are a consumer decision.** The data itself doesn't say whether row one is a header, so Table asks the user (the `csvFirstRowIsHeader` switch) and simply `array_shift`s the first row into `$csvHeaders` when they say yes.
* **The known limit: multi-line fields.** Splitting into lines first means a newline *inside* a quoted field breaks that record across two rows. That trade-off is fine for typical spreadsheet exports; if your component must survive full RFC 4180 data, parse the whole stream with `fgetcsv` instead of splitting lines up front.

## Remote JSON in the Browser

When the data should be as live as the page view itself — scores, stock, availability — fetch it in the visitor's browser instead. Here's a complete minimal pattern: an Alpine factory that fetches JSON on `init` and drives explicit loading and error states, with the script registered once via a portal:

```html
<!-- templates/index.html -->
<div class="{{classes.wrapper}}" x-data="newsFeed('{{feedUrl}}')">
    <template x-if="loading">
        <p>Loading&hellip;</p>
    </template>
    <template x-if="error">
        <p x-text="error"></p>
    </template>
    <template x-for="item in items">
        <article>
            <h3 x-text="item.title"></h3>
            <p x-text="item.summary"></p>
        </article>
    </template>
</div>

@portal(bodyEnd, includeOnce: true, id: "com.example.newsfeed.alpine")
<script>
    document.addEventListener("alpine:init", () => {
        Alpine.data("newsFeed", (url) => ({
            items: [],
            loading: true,
            error: null,
            async init() {
                try {
                    const response = await fetch(url);
                    if (!response.ok) {
                        throw new Error("HTTP " + response.status);
                    }
                    this.items = await response.json();
                } catch (e) {
                    this.error = "Couldn't load the feed right now.";
                } finally {
                    this.loading = false;
                }
            },
        }));
    });
</script>
@endportal
```

All three states are always in the markup and Alpine swaps between them, so the component is never blank while the request is in flight and never silent when it fails. Note that the fetched strings only ever reach the page through `x-text` — more on that below. And because Alpine never initialises on the editing canvas, pair this with a labelled sample layout inside an `@if(edit)` branch, exactly as Table does for CSV.

{% hint style="info" %}
Browser fetches are subject to **CORS**: the remote server must send `Access-Control-Allow-Origin` headers that permit the visitor's origin, and you don't control that from your component. If an API doesn't allow cross-origin reads, move the ingestion to request time — fetch it in PHP (where CORS doesn't apply) and render or relay it from your own domain. [Server-Side PHP Components](server-side-php-components.md) shows that variant, including response caching.
{% endhint %}

## Keeping the Canvas Useful

Whatever the ingestion point, edit mode never has the real data — so give it convincing fake data, clearly labelled, in a bounded amount. Table generates exactly five sample rows regardless of how large the real CSV might be, matches their column count to the user's collection, and captions them "Example data — CSV file will be loaded on the published site." A handful of rows is enough to make every styling control visibly do something; an unbounded preview would just make the canvas slow and scrolly. The full set of edit-mode patterns — placeholders, preview datasets, gating heavy behaviour — lives in [Designing the Edit-Mode Experience](edit-mode-experience.md).

## Treat External Data as Untrusted

External data is input from the internet, and it ends up inside your HTML. Table escapes every value it outputs — headers, cells, even the assembled class strings go through `htmlspecialchars` (`<?php echo htmlspecialchars($cell); ?>`). Hold your components to the same line.

{% hint style="warning" %}
**Escape external data at every output point.** A CSV cell or JSON field can contain `<script>` just as easily as a price. In PHP, wrap every echoed value in `htmlspecialchars()` — including values placed inside attributes, where a stray quote breaks out of the attribute context. In the browser, render fetched strings with `x-text` (or `textContent`), never `x-html` or `innerHTML`, and never interpolate fetched values into attribute strings by concatenation. If you must render remote HTML, sanitise it first; "it's our own feed" is not a sanitiser.
{% endhint %}

## Related Documentation

* [Server-Side PHP Components](server-side-php-components.md) — fetching, relaying, and caching remote data in PHP
* [Designing the Edit-Mode Experience](edit-mode-experience.md) — preview datasets and canvas behaviour
* [PHP Templates](../component/templates/php-templates.md) — `index.php` as a main template, `requiresPhp`, heredoc data passing
* [Backend](../component/templates/backend.md) — server-side request handlers in `templates/backend/`
* [Collections](../component/collections/README.md) — the structured datasets behind Table's columns
* [Resource](../component/properties.json/ui-controls/resource.md) — the file dropwell control and its `.path` property
