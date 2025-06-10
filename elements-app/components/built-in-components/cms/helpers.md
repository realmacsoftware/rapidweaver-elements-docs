# Helpers

### cms()

You can include the `cms.php` file for access to a `cms()` method.

```php
// Important: you must ensure the cms() function hasn't 
// already been declared before including the file.
if (!function_exists('cms')) {
    require_once __DIR__ . '/{{cmsPath}}/cms.php';
}

$cms = cms("base_path");

// Collection of Items
$currentPage = 1;
$itemsPerPage = 10;
$articles = $cms->collection('articles')
    ->orderBy('date_published', 'asc')
    ->paginate($currentPage, $itemsPerPage);

// Single Items
$collectionPath = 'articles';
$itemSlug = 'hello-world';
$detailPage = '/articles/';
$item = $cms->item($collectionPath, $itemSlug, ['detailPage' => $detailPage]);
```
