---
description: >-
  A collection class for managing CMS items, providing methods for filtering,
  ordering, pagination, and searching.
---

# ElementsCMSCollection

### Constructor

#### `__construct(ElementsCMS $cms, string $path, array $options = [])`

Creates a new collection instance.

* **$cms** (`ElementsCMS`): The CMS instance.
* **$path** (`string`): Path to the collection (folder).
* **$options** (`array`): Additional options for the collection.

***

### Instance Methods

#### `with(string ...$relations): self`

Add relations to be eager-loaded for all items in the collection.

* **$relations** (`string ...`): One or more relation names.
* **Returns**: `$this` (for chaining)

#### `filter(array $criteria = []): self`

Filter items in the collection by key/value pairs.

* **$criteria** (`array`): Associative array of criteria (e.g., `['status' => 'published']`)
* **Returns**: `$this` (for chaining)

#### `filterWith(callable $callback): self`

Filter items in the collection using a custom callback.

* **$callback** (`callable`): Function that receives an item and returns `true` to keep, `false` to exclude.
* **Returns**: `$this` (for chaining)

#### `orderBy(string $field, string $direction = 'desc'): self`

Order the collection by a specified field.

* **$field** (`string`): Field name to order by.
* **$direction** (`string`): `'asc'` or `'desc'` (default: `'desc'`)
* **Returns**: `$this` (for chaining)

#### `whereDate(string $field, string $operator, string $date): self`

Filter items by date field using a comparison operator.

* **$field** (`string`): Date field to compare (e.g., `'published_date'`)
* **$operator** (`string`): Comparison operator (e.g., `'>='`, `'=='`, `'<'`)
* **$date** (`string`): Date value for comparison.
* **Returns**: `$this` (for chaining)

#### `paginate(int $page = 1, int $perPage = 10): array`

Paginate the collection.

* **$page** (`int`): Page number (default: `1`)
* **$perPage** (`int`): Items per page (default: `10`)
* **Returns**: `array` — Paginated results, typically including `items`, `total`, `page`, `per_page`, etc.

#### `getCollection(): LaravelCollection`

Returns the underlying Laravel collection of items.

* **Returns**: `Illuminate\Support\Collection` of `ElementsCMSItem` objects.

#### `findBySlug(string $slug): ?ElementsCMSItem`

Find an item in the collection by its slug.

* **$slug** (`string`): The slug to search for.
* **Returns**: `ElementsCMSItem|null`

#### `search(string $query): array`

Search the collection items by query string.

* **$query** (`string`): The search term.
* **Returns**: `array` — Array of matching `ElementsCMSItem` objects.

***

### Usage Example

```php
$collection = new ElementsCMSCollection($cms, 'posts', [
    'expectDates' => true
]);

// Filter, order, and paginate items
$results = $collection
    ->filter(['status' => 'published'])
    ->orderBy('published_date', 'desc')
    ->paginate(1, 10);

// Find a specific item by slug
$item = $collection->findBySlug('hello-world');

// Search items
$matches = $collection->search('static site generator');
```
