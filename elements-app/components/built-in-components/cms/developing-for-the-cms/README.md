---
description: >-
  The Elements CMS is a powerful content management system designed for
  RapidWeaver elements, providing a flexible and efficient way to manage content
  through markdown files with YAML front matter.
---

# Developing for the CMS

### Table of Contents

* [Getting Started](./#getting-started)
* [Core Concepts](./#core-concepts)
* [Working with Collections](./#working-with-collections)
* [Working with Items](./#items)
* [Search Functionality](./#search-functionality)
* [Related Items](./#related-items)
* [RSS and Sitemap Generation](./#rss-and-sitemap-generation)

### Getting Started

To initialize the CMS in your PHP code:

```php
require_once 'path/to/cms.php';

// Initialize CMS with base path and options
$cms = cms('/path/to/content', [
    'detailPageUrl' => 'https://example.com/posts',
    'prettyUrls' => true
]);
```

### Core Concepts

#### Collections

Collections are groups of content items stored in markdown files. Each collection is stored in a directory, with each item represented by a markdown file.

#### Items

Items are individual content pieces stored as markdown files with YAML front matter. The filename format can be either:

* `YYYY-MM-DD-slug.md` (for dated content)
* `slug.md` (for undated content)

Example item structure:

```markdown
---
title: My Post Title
date: 2024-03-20
author: John Doe
tags: [news, technology]
categories: [blog]
featured: true
status: published
image:
    type: remote
    src: https://example.com/image.jpg
    alt: Image description
    width: 800
    height: 600
---

Content goes here...
```

### Working with Collections

#### Basic Collection Operations

```php
// Get a collection
$collection = $cms->collection('blog');

// Filter collection
$filtered = $collection->filter([
    'status' => 'published',
    'featured' => true
]);

// Order collection
$ordered = $collection->orderBy('date', 'desc');

// Paginate results
$paginated = $collection->paginate(1, 10);
```

#### Advanced Filtering

```php
// Date-based filtering
$collection->whereDate('date', '>=', '2024-01-01');

// Custom filtering
$collection->filterWith(function($item) {
    return $item->featured() && $item->status() === 'published';
});
```

### Working with Items

#### Loading and Accessing Items

```php
// Load a specific item
$item = $cms->item('blog/my-post');

// Access item properties
$title = $item->title();
$date = $item->date('F j, Y');
$body = $item->body();
$excerpt = $item->excerpt(30);
$image = $item->image();
$url = $item->url();

// Access custom metadata
$customField = $item->meta('custom_field');
```

#### Item Relationships

```php
// Load item with relationships
$item = $cms->item('blog/my-post')
    ->with('author', 'categories')
    ->withOne('featured_image')
    ->loadRelations();

// Access relationships
$author = $item->author;
$categories = $item->categories;
$featuredImage = $item->featured_image;
```

### Search Functionality

The CMS includes a powerful search system that can be used in two ways:

#### PHP Search

```php
// Search within a collection
$results = $collection->search('search term');

// Search with template rendering
$results = $collection->search('search term', 'template.twig');
```

#### AJAX Search Endpoint

The CMS provides a search endpoint at `search.php` that accepts the following parameters:

* `q`: Search query
* `collectionPath`: Path to the collection
* `detailPageUrl`: URL for detail pages
* `prettyUrls`: Whether to use pretty URLs
* `basePath`: Base path for content
* `template`: Twig template for rendering results

Example AJAX call:

```javascript
fetch(
    "search.php?q=search+term&collectionPath=blog&detailPageUrl=/posts&prettyUrls=true&basePath=/content&template=search-result.twig"
)
    .then((response) => response.json())
    .then((results) => {
        // Handle results
    });
```

### Related Items

The CMS provides a fluent interface for finding related items:

```php
$related = $item->related()
    ->byTags()
    ->limit(5)
    ->excludeSelf()
    ->get();

// Or find by multiple criteria
$related = $item->related()
    ->by(['tags', 'author', 'categories'])
    ->in('blog')
    ->limit(3)
    ->get();
```

### RSS and Sitemap Generation

#### RSS Feed

```php
$rss = $collection->toRss(
    'My Blog',
    'Latest posts from my blog',
    'https://example.com/blog'
);
```

#### XML Sitemap

```php
$sitemap = $collection->toSitemap(
    'https://example.com',
    'weekly',
    0.8
);
```

### Best Practices

1. **File Organization**
   * Keep collections in separate directories
   * Use consistent naming conventions for files
   * Include all necessary metadata in front matter
2. **Performance**
   * Use caching when appropriate
   * Implement pagination for large collections
   * Optimize search queries
3. **Content Structure**
   * Use consistent front matter fields
   * Include required metadata (title, date, status)
   * Properly format markdown content
4. **Security**
   * Validate user input
   * Sanitize output
   * Use proper file permissions

### Dependencies

The CMS requires the following PHP packages:

* Symfony YAML
* CommonMark
* Illuminate Collections
* Twig (for template rendering)

### Error Handling

The CMS includes built-in error handling for common scenarios:

* Invalid file paths
* Missing required metadata
* Malformed YAML front matter
* Search index issues

### Support

For issues, feature requests, or contributions, please refer to the project's issue tracker or documentation repository.
