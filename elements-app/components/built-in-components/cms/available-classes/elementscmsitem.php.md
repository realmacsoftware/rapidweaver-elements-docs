---
description: >-
  Represents a single CMS item loaded from a Markdown file with front matter.  
  Provides structured access to metadata, raw and rendered content, file paths,
  and relationships to other items.
---

# ElementsCMSItem.php

### Constructor

#### `__construct(ElementsCMS $cms, array $data = [])`

Creates a new CMS item.

* **$cms** (`ElementsCMS`): The CMS instance.
* **$data** (`array`): The data for the CMS item.

***

### Static Methods

#### `static load(ElementsCMS $cms, string $filepath): ?self`

Load a CMS item from a file.

* **$cms** (`ElementsCMS`): The CMS instance.
* **$filepath** (`string`): Path to the file.
* **Returns**: `ElementsCMSItem|null` – Loaded item or null if not found.

***

### Instance Methods

#### `setOptions(array $options): self`

Sets runtime options for the item.

* **$options** (`array`): Option key/value pairs.
* **Returns**: `$this` for method chaining.

#### `getOption(string $key, $default = null)`

Gets an option value by key.

* **$key** (`string`): Option name.
* **$default** (`mixed`): Default value if not found.
* **Returns**: Mixed option value.

#### `slug(): string`

Returns the item’s slug (URL-friendly identifier).

#### `title(): string`

Returns the item’s title.

#### `date(string $format = 'F j, Y'): string`

Returns the item's date in the given format.

* **$format** (`string`): Date format (default `'F j, Y'`).

#### `datePublished(string $format = 'F j, Y'): string`

Returns the item's published date.

#### `dateModified(string $format = 'F j, Y'): string`

Returns the item's last modified date.

#### `featured(): bool`

Checks if the item is marked as featured.

#### `status(): string`

Returns the item's status (e.g., published/draft).

#### `body(): string`

Returns the rendered HTML body content.

#### `rawBody(): string`

Returns the raw markdown body content.

#### `image(): ?string`

Returns the item's image URL, if available.

#### `excerpt(int $words = 30): string`

Returns an excerpt of the body, limited to the specified word count.

#### `meta(string $key, $default = null): mixed`

Fetches a value from the item's metadata/front-matter.

* **$key** (`string`): Meta key.
* **$default** (`mixed`): Default if key is missing.

#### `attach(string $key, $value): self`

Attach related data to the item (e.g., relations, computed properties).

#### `get(string $key, $default = null): mixed`

Returns any value from the item data or metadata.

#### `__call($method, $arguments)`

Allows dynamic method access to metadata fields.

#### `file(): string`

Returns the full path to the file.

#### `fileName(): string`

Returns the base filename (without extension).

#### `url(): string`

Returns the item’s URL.

#### `lastModified(string $format = 'F j, Y'): string`

Returns the file's last modified date.

#### `toArray(): array`

Returns all item data as an associative array.

#### `with(string ...$relations): self`

Declare relations (one-to-one or one-to-many) to eager-load.

#### `withOne(string ...$relations): self`

Declare one-to-one relations to eager-load.

#### `withMany(string ...$relations): self`

Declare one-to-many relations to eager-load.

#### `loadRelations(): self`

Loads all defined relations for the item.

***

### Usage Example

```php
$cms = new ElementsCMS(/* ... */);
$item = ElementsCMSItem::load($cms, 'posts/hello-world');

if ($item) {
    echo $item->title();           // Item title
    echo $item->body();            // Rendered body
    echo $item->datePublished();   // Published date
    $item->with('author', 'categories')->loadRelations();
}
```
