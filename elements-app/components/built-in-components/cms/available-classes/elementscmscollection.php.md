---
description: >-
  A PHP class for managing a collection of CMS items in the Elements CMS. It
  provides rich methods for filtering, ordering, pagination, and custom logic
  using Laravel Collections behind the scenes.
---

# ElementsCMSCollection.php

### Overview

`ElementsCMSCollection` acts as a controller layer over a directory of Markdown content items. You can query, sort, and filter data just like working with a database or API — but it's all file-based.

This class is automatically used when querying collections like blog posts, case studies, or products using the Elements CMS API.

***

### Constructor

#### `__construct(ElementsCMS $cms, string $path, array $options = [])`

Creates a new CMS collection instance.

**Parameters:**

* **`$cms`**: The main CMS instance.
* **`$path`**: The subdirectory (collection path) inside the content directory.
* **`$options`** _(optional)_: Configuration flags (e.g. `expectDates`, default ordering, etc).

***

### Public Methods

#### `get() : LaravelCollection`

Returns the filtered, ordered Laravel collection of items.

***

#### `first() : ?ElementsCMSItem`

Returns the first matching item (after filtering and sorting).

***

#### `count() : int`

Returns the number of items in the filtered collection.

***

#### `paginate(int $perPage, int $currentPage = 1) : array`

Returns a paginated subset of items and pagination metadata.

**Returns:**

```php
[
  'items' => LaravelCollection,
  'pagination' => [
    'total' => int,
    'current_page' => int,
    'per_page' => int,
    'last_page' => int,
    'from' => int,
    'to' => int
  ]
]
```

***

#### `filter(string $field, string|array $value) : self`

Filters the collection where the specified field matches the given value.

* Accepts a single value or array of values.
* Multiple `filter()` calls stack.

***

#### `customFilter(callable $callback) : self`

Applies a custom filter to the collection using a closure.

```php
$collection->customFilter(function ($item) {
    return $item->published === true;
});
```

***

#### `orderBy(string $field, string $direction = 'desc') : self`

Sorts items by a specific front matter field (`asc` or `desc`).

***

#### `with(string ...$relations) : self`

Preloads related collections or fields for each item.

```php
$collection->with('author', 'categories');
```

***

### Internal Methods (Advanced)

#### `load() : LaravelCollection`

Used internally to load items from disk before filters, ordering, and pagination.

***

#### `applyFilters(LaravelCollection $items) : LaravelCollection`

Applies all defined filters (including `filter()` and `customFilter()`).

***

#### `applyOrdering(LaravelCollection $items) : LaravelCollection`

Applies ordering based on the specified field and direction.

***

### Usage Example

```php
$posts = $cms->collection('posts')
    ->filter('tags', 'design')
    ->orderBy('date', 'desc')
    ->paginate(10, $_GET['page'] ?? 1);
```

***

### Related Classes

* `ElementsCMSItem` – Represents individual CMS items.
* `ElementsCMS` – Root controller for all content access.
