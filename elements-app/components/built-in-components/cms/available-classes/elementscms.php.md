---
description: >-
  The ElementsCMS class is a PHP-based content management system that provides
  functionality for managing CMS collections and items. It serves as the main
  entry point for interacting with content stored
---

# ElementsCMS.php

### Overview

The ElementsCMS class manages the base path for content storage and provides methods to create collections, load items, and manage configuration options.

### Constructor

#### `__construct(string $basePath, array $options = [])`

Creates a new instance of ElementsCMS.Parameters:

* `$basePath (string)`: The base path for the CMS content storage
* `$options (array, optional)`: Additional configuration options for the CMS

```php
$cms = new ElementsCMS('/path/to/content', ['debug' => true]);
```

### Static Methods

#### `make(string $basePath, array $options = []): ElementsCMS`

Static factory method that creates a new instance of ElementsCMS.Parameters:

* $basePath (string): The base path for the CMS content storage
* $options (array, optional): Additional configuration options for the CMS

Returns: ElementsCMS instanceExample:phpApply to ElementsCMS....$cms = ElementsCMS::make('/path/to/content', \['theme' => 'default']);

### Configuration Methods

#### `basePath(): string`

**Returns**: The base path as a string

```php
$path = $cms->basePath(); // Returns '/path/to/content'
```

#### `options(): array`

**Returns**: Array of all options

```php
$allOptions = $cms->options();
```

#### `option(string $key, $default = null): mixed`

**Returns**: The option value or default value

Parameters:

* `$key (string)`: The option key to retrieve
* `$default (mixed, optional)`: Default value returned if the option is not set

```php
$debug = $cms->option('debug', false);
$theme = $cms->option('theme', 'default');
setOption(string $key, $value): void
```

#### `setOption(string $key, $value): void`

Sets an option value.

* $key (string): The option key to set
* $value (mixed): The value to set

```php
$cms->setOption('debug', true);
$cms->setOption('cache_enabled', false);
```

### Content Management Methods

#### `collection(string $path, array $options = []): ElementsCMSCollection`

Creates a new collection instance.Parameters:

* $path (string): The path for the collection (relative to base path)
* $options (array, optional): Additional options for the collection

Returns: ElementsCMSCollection instance

```php
$articles = $cms->collection('articles', ['sort' => 'date']);
$projects = $cms->collection('projects');
```

#### `item(string $collectionPath, string $slug): ?ElementsCMSItem`

Loads a specific item from a collection.Parameters:

* `$collectionPath (string)`: The path of the collection
* `$slug (string)`: The slug/filename of the item (without .md extension)

**Returns**: ElementsCMSItem instance or null if not found

```php
$blogPost = $cms->item('blog', 'my-first-post');
$aboutPage = $cms->item('pages', 'about');
```

### Usage Examples

#### Basic Setup

```php
<?php
require_once '/path/to/ElementsCMS.php';

$cms = ElementsCMS::make(
    '/var/www/content',
    ['debug' => true, 'cache_ttl' => 3600]
);
```

#### Working with Collections

```php
// Create a blog collection
$blog = $cms->collection('blog', ['sort' => 'date_desc']);

// Create a pages collection
$pages = $cms->collection('pages');
```

#### Loading Individual Items

```php
// Load a specific blog post
$post = $cms->item('blog', 'introduction-to-cms');

// Load a page
$homepage = $cms->item('pages', 'home');
```

#### Managing Configuration

```php
// Get configuration
$debugMode = $cms->option('debug', false);
$cacheEnabled = $cms->option('cache_enabled', true);

// Set configuration
$cms->setOption('theme', 'custom');
$cms->setOption('max_items_per_page', 10);
```

### Dependencies

This class requires the following files:

* ElementsCMSCollection.php
* ElementsCMSItem.php

Make sure these files are available in the same directory as the ElementsCMS class.

### File Structure

The CMS expects content to be organized in the following structure:

* cms-base-path/
  * collection-name/
    * item-slug.md
    * another-item.md
  * another-collection/
    * item1.md
    * item2.md

**Items must be in Markdown files (.md extension) within collection directories.**
