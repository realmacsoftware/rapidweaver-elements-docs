---
description: Using PHP files in the templates directory
---

# PHP Templates

PHP files can be placed in the `templates/` directory and are processed through the Elements template engine before being deployed. This allows you to combine Elements template directives with PHP code for server-side functionality.

## Overview

PHP template files provide:

* **Server-side processing** - Execute PHP code on the server
* **Property insertion** - Use component properties in PHP code
* **Template directives** - Combine Elements Language with PHP
* **Backend deployment** - PHP files are deployed to the published site

{% hint style="info" %}
For most server-side functionality, you should use the [Backend directory](backend.md) which is specifically designed for PHP files that need to be deployed to the server's backend directory.
{% endhint %}

## File Location

```
com.yourcompany.component/
├── templates/
│   ├── index.html         # Main template (or index.php — see below)
│   ├── handler.php        # Root-level PHP template
│   └── backend/           # Server-side request handlers
│       └── process.php
```

## When to Use PHP Templates

### Root-Level PHP

Root-level PHP templates are processed and included in the page output.

**Use root-level PHP when:**

* You need to generate HTML with server-side logic during page rendering
* The PHP output should be part of the page's normal HTML flow

A component can even use `index.php` **in place of** `index.html` as its main template. This is how the core Table component renders CSV files server-side — see [PHP as the Main Template](#php-as-the-main-template-indexphp) below.

### Backend PHP (Recommended)

Most PHP files should be in the `templates/backend/` directory:

```
templates/
└── backend/
    ├── submit.php        # Form submission handler
    ├── api.php           # API endpoint
    └── process.php       # Data processing
```

**Use backend PHP for:**

* Form processing
* API endpoints
* Database operations
* Server-side data manipulation
* AJAX request handlers

See the [Backend directory documentation](backend.md) for detailed information about backend PHP files.

## Basic Usage

PHP template files can use both Elements template directives and PHP code:

```php
<?php
// PHP variables from component properties
$componentId = '{{id}}';
$formAction = '{{formAction}}';
$maxFileSize = {{maxFileSize}};

@if(enableLogging)
// Conditional PHP
error_log("Component $componentId initialized");
@endif
?>

<form action="<?php echo $formAction; ?>" method="POST">
    <input type="hidden" name="component_id" value="{{id}}">
    <input type="hidden" name="max_size" value="{{maxFileSize}}">
    <!-- Form fields -->
</form>
```

## Property Insertion in PHP

Insert component properties into PHP code:

```php
<?php
// String properties
$title = '{{title}}';
$description = '{{description}}';

// Numeric properties
$maxItems = {{maxItems}};
$timeout = {{timeout}};

// Boolean properties
$isEnabled = {{enabled}};  // true or false

@if(debugMode)
// Debug information
var_dump([
    'component_id' => '{{id}}',
    'title' => $title,
    'max_items' => $maxItems
]);
@endif
?>
```

## PHP as the Main Template (index.php)

A component's main template can be `templates/index.php` instead of `index.html`. The core Table component uses this to load and render CSV files on the server.

### Declare requiresPhp in info.json

Components that output PHP must set [`requiresPhp`](../info.json.md) in `info.json` so Elements knows the page containing the component must be published with a `.php` filename — otherwise the PHP won't execute. (Child components that only ever appear inside a parent that already requires PHP don't need the flag.)

```json
{
    "identifier": "com.realmacsoftware.table",
    "title": "Table",
    "group": "Content",
    "requiresPhp": true
}
```

### The Full Template Language Still Works

`index.php` is processed like any other template — directives, editable areas, and includes work alongside the PHP. PHP can't execute inside the RapidWeaver editor, so the Table renders example rows in edit mode and reserves the PHP for the exported page. The excerpt below is condensed from the file's CSV mode:

```php
@if(isCSVMode)
    @if(edit)
    <!-- Edit mode: PHP can't run in the editor, so show example rows -->
    <table class="{{classes.table}}">
        <!-- ... -->
    </table>
    @else
    <div x-data="elementsTable('{{id}}', {{alpineConfig}})">
        <?php
        $csvSource = '{{csvSource}}';

        // Normalise values that may arrive as strings
        $rawFirstRow = '{{csvFirstRowIsHeader}}';
        $firstRowIsHeader = in_array($rawFirstRow, ['true', '1', 'yes'], true);
        ?>
        <!-- ... -->
    </div>
    @endif
@else
<!-- Manual mode: rows are edited in the app, no PHP needed -->
@endif
```

`alpineConfig` is prepared in `hooks.js` with the [quote-swap pattern](js-templates.md#the-quote-swap-pattern) — `JSON.stringify(config).replace(/"/g, "'")` — so the JSON survives inside the double-quoted `x-data` attribute.

### Patterns from the Table Component

Two details of the real `index.php` are worth copying.

**Use closures, not named functions.** Root-level templates are processed once per instance, so a named function would be declared twice when two tables share a page:

```php
<?php
// A closure (not a named function) so multiple table instances on the
// same page don't trigger "Cannot redeclare function" fatal errors.
$tableGetColumnMeta = function ($columnMeta, $idx) {
    return $columnMeta[$idx] ?? [
        'widthClass' => '',
        'headerAlignmentClass' => '',
        'bodyAlignmentClass' => '',
        'hiddenClass' => '',
        'extraClasses' => '',
        'isSortable' => false,
    ];
};
?>
```

**Pass structured data via heredoc + `json_decode`.** JSON contains quote characters that would break a normal quoted PHP string:

```php
<?php
$columnMetaJson = <<<COLUMNMETA
{{csvColumnMeta}}
COLUMNMETA;
$columnMeta = json_decode($columnMetaJson, true);
if (!is_array($columnMeta)) {
    $columnMeta = [];
}
?>
```

A heredoc still processes PHP `$variable` interpolation and escape sequences. If the data might contain a `$` or backslashes, use a **nowdoc** (`<<<'COLUMNMETA'`) instead — it treats the body as literal text. Elements interpolates `{{csvColumnMeta}}` before PHP ever sees the file, so a nowdoc doesn't affect template processing.

## Processing Behavior

### Template Processing First

Elements template directives are processed **before** PHP execution:

1. Elements processes `{{property}}`, `@if`, `@each`, etc.
2. Resulting PHP code is deployed to the server
3. PHP executes when the page is requested

This means you can use template directives to generate PHP code dynamically.

## Backend Directory (Recommended Pattern)

The most common use case for PHP in components is form handling in the backend directory:

```php
<!-- templates/backend/submit.php -->
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // Get component ID from template
    $componentId = '{{id}}';

    // Sanitize input
    $name = htmlspecialchars(strip_tags(trim($_POST["name"])));
    $email = filter_var(trim($_POST["email"]), FILTER_SANITIZE_EMAIL);

    @if(enableValidation)
    // Conditional validation
    if (empty($name) || empty($email)) {
        http_response_code(400);
        echo json_encode(['error' => 'Missing required fields']);
        exit;
    }
    @endif

    // Process form
    $result = processFormData($name, $email);

    @if(sendEmail)
    // Send notification email
    mail('{{notificationEmail}}', 'Form Submission', $result);
    @endif

    echo json_encode(['success' => true, 'message' => 'Form submitted']);
}
?>
```

Then reference it from your HTML template:

```html
<!-- templates/index.html -->
<form id="contact-form-{{id}}">
    <input type="text" name="name" required>
    <input type="email" name="email" required>
    <button type="submit">Submit</button>
</form>

<script>
document.getElementById('contact-form-{{id}}').addEventListener('submit', async (e) => {
    e.preventDefault();
    const formData = new FormData(e.target);

    const response = await fetch('{{node.backendPath}}/submit.php', {
        method: 'POST',
        body: formData
    });

    const result = await response.json();
    console.log(result);
});
</script>
```

See the [Backend documentation](backend.md) for complete examples and best practices.

## Limitations

### Template Processing Only

PHP files in templates are processed by Elements template engine during publish, but they're not executed during the build process. They're deployed to the server and execute when requested.

### Security Considerations

Always sanitize and validate user input in PHP:

```php
<?php
// Sanitize input
$userInput = htmlspecialchars(strip_tags(trim($_POST['input'])));

// Validate
if (!filter_var($userInput, FILTER_VALIDATE_EMAIL)) {
    http_response_code(400);
    exit('Invalid input');
}

// Use prepared statements for database queries
$stmt = $pdo->prepare('SELECT * FROM users WHERE email = ?');
$stmt->execute([$userInput]);
?>
```

## Common Patterns

### Form Processing

Process form submissions with component properties:

```php
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $componentId = '{{id}}';
    $maxFileSize = {{maxFileSize}};

    $allowedTypesJson = <<<'ALLOWEDTYPES'
{{allowedTypesJson}}
ALLOWEDTYPES;
    $allowedTypes = json_decode($allowedTypesJson, true) ?: [];

    // Process uploaded file
    if (isset($_FILES['file'])) {
        if ($_FILES['file']['size'] > $maxFileSize) {
            http_response_code(400);
            echo json_encode(['error' => 'File too large']);
            exit;
        }

        // Handle file upload
        // ...
    }

    echo json_encode(['success' => true]);
}
?>
```

Array properties can't be interpolated into PHP source directly — serialise them to JSON in `hooks.js` and receive them through a nowdoc so quote characters and backslashes survive (see [Patterns from the Table Component](#patterns-from-the-table-component)):

```javascript
// hooks.js
const transformHook = (rw) => {
    rw.setProps({
        allowedTypesJson: JSON.stringify(rw.props.allowedTypes ?? []),
    });
};
exports.transformHook = transformHook;
```

### API Endpoints

Create simple API endpoints:

```php
<?php
header('Content-Type: application/json');

$componentId = '{{id}}';
$apiKey = '{{apiKey}}';

// Verify API key
if (!isset($_SERVER['HTTP_X_API_KEY']) || $_SERVER['HTTP_X_API_KEY'] !== $apiKey) {
    http_response_code(401);
    echo json_encode(['error' => 'Unauthorized']);
    exit;
}

// Handle request
$data = [
    'component' => $componentId,
    'items' => getItems(),
    'timestamp' => time()
];

echo json_encode($data);
?>
```

### Configuration Files

Generate PHP configuration from component properties:

```php
<?php
return [
    'component_id' => '{{id}}',
    'settings' => [
        'enabled' => {{enabled}},
        'max_items' => {{maxItems}},
        'cache_duration' => {{cacheDuration}},
        'api_endpoint' => '{{apiEndpoint}}'
    ],
    @if(features)
    'features' => [
        'feature1' => {{feature1Enabled}},
        'feature2' => {{feature2Enabled}}
    ],
    @endif
];
?>
```

## Best Practices

### Use Backend Directory for Request Handlers

Place request handlers in `templates/backend/` rather than at the root level — root-level PHP is for page output (like an `index.php` main template), not for handling requests:

```
✓ templates/backend/handler.php
✗ templates/handler.php
```

### Pass Configuration from Properties

Use component properties to configure PHP behavior:

```javascript
// hooks.js
const transformHook = (rw) => {
    rw.setProps({
        node: rw.node,
        apiEndpoint: '/api/data',
        timeout: 30,
        enableCaching: true
    });
};
exports.transformHook = transformHook;
```

```php
<!-- templates/backend/api.php -->
<?php
$endpoint = '{{apiEndpoint}}';
$timeout = {{timeout}};
$caching = {{enableCaching}};

// Use configuration
?>
```

### Separate Logic from Configuration

Keep complex PHP logic in shared assets, use templates for configuration. Pass the shared-asset path from `hooks.js`:

```javascript
// hooks.js
const transformHook = (rw) => {
    rw.setProps({
        siteAssetPath: rw.component.siteAssetPath,
    });
};
exports.transformHook = transformHook;
```

```php
<!-- templates/backend/process.php -->
<?php
// Include shared library
require_once('{{siteAssetPath}}/lib/processor.php');

// Configure from properties
$processor = new Processor([
    'option1' => '{{option1}}',
    'option2' => {{option2}},
    'option3' => {{option3}}
]);

// Execute
$result = $processor->run($_POST);
echo json_encode($result);
?>
```

### Handle Errors Gracefully

Provide proper error handling:

```php
<?php
try {
    @if(debugMode)
    error_reporting(E_ALL);
    ini_set('display_errors', 1);
    @else
    error_reporting(0);
    @endif

    // Process request
    $result = processRequest($_POST);

    echo json_encode([
        'success' => true,
        'data' => $result
    ]);

} catch (Exception $e) {
    http_response_code(500);

    @if(debugMode)
    $message = $e->getMessage();
    @else
    $message = 'An error occurred';
    @endif

    echo json_encode([
        'success' => false,
        'error' => $message
    ]);
}
?>
```

## Templates vs Assets

Choose the right location for PHP files:

### Use `templates/backend/` When:

* PHP needs component property values
* PHP is component-specific functionality
* PHP handles form submissions or AJAX requests
* Configuration varies per component

### Use Shared Assets When:

* PHP is a reusable library
* PHP doesn't need component properties
* Code is shared across multiple components
* You want to minimize deployed files

## Related Documentation

* [Backend Directory](backend.md) - Detailed backend PHP documentation
* [Shared Assets](../shared-files/assets.md) - Shared PHP libraries
* [Elements Language](../language/) - Template syntax in PHP
* [Hooks.js](../hooks.js/) - Passing data to PHP templates
* [Properties](../properties.json/) - Defining configuration properties
* [Server-Side PHP Components](../../guides/server-side-php-components.md) - Runtime rendering, @raw tokens, and caching
* [External Data Sources](../../guides/external-data-sources.md) - CSV and remote data ingestion patterns
