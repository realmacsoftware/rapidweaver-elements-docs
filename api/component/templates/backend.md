---
description: Deploy server-side files to the backend directory
---

# Backend

The `templates/backend/` directory contains server-side files that are deployed to the page's backend directory during publish. Unlike files in the root templates directory, backend files are not included in the page output—they are deployed as separate files that can be accessed via server-side requests.

## Purpose

Use the backend directory for:

* Form submission handlers
* API endpoints
* Server-side data processing
* AJAX request handlers
* File upload processors

## Directory Location

```
com.yourcompany.component/
├── templates/
│   ├── index.html
│   └── backend/              # Backend directory
│       ├── submit.php
│       └── api.php
```

## How It Works

### 1. Deployment Structure

Backend files are deployed to a unique subdirectory based on the page's node ID to prevent conflicts:

```
published-site/
└── contact/
    ├── index.html
    └── backend/
        └── rw29BB9A86_0D4A_4E46_9BF5_CD5041A9ECE2/
            └── submit.php
```

### 2. Template Processing

Backend files are processed through the Elements template engine before deployment, allowing you to use component properties:

```php
<!-- templates/backend/submit.php -->
<?php
$componentId = '{{id}}';
$maxUploadSize = {{maxUploadSize}};
$notificationEmail = '{{notificationEmail}}';

// Your PHP code here
?>
```

### 3. Supported File Types

* `.php` - PHP scripts
* `.html` - HTML files
* `.js` - JavaScript files
* `.css` - Stylesheets

## Accessing Backend Files

### Using node.backendPath

To reference backend files from your component templates, use the `node.backendPath` property. This property must be passed from `hooks.js`:

```javascript
// hooks.js
const transformHook = (rw) => {
    rw.setProps({
        node: rw.node
    });
};

exports.transformHook = transformHook;
```

Then in your HTML template, reference the backend file:

```html
<script>
fetch('{{node.backendPath}}/submit.php', {
    method: 'POST',
    body: formData
});
</script>
```

See [Passing data to templates](../hooks.js/passing-data-to-templates.md) for more details.

## Example: Contact Form

A typical use case is processing form submissions. Create a backend PHP file to handle the form:

```php
<!-- templates/backend/submit.php -->
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $name = htmlspecialchars(strip_tags(trim($_POST["name"])));
    $email = filter_var(trim($_POST["email"]), FILTER_SANITIZE_EMAIL);

    // Process form data
    mail('{{notificationEmail}}', 'Form Submission', "Name: $name\nEmail: $email");

    echo json_encode(['success' => true]);
}
?>
```

Reference it from your HTML template:

```html
<!-- templates/index.html -->
<form id="form-{{id}}">
    <input type="text" name="name" required>
    <input type="email" name="email" required>
    <button type="submit">Submit</button>
</form>

<script>
document.getElementById('form-{{id}}').addEventListener('submit', async (e) => {
    e.preventDefault();
    const response = await fetch('{{node.backendPath}}/submit.php', {
        method: 'POST',
        body: new FormData(e.target)
    });
    const result = await response.json();
});
</script>
```

## Using Subdirectories

The backend directory supports subdirectories for organizing your backend files. However, Elements monitors every file in the backend directory for changes, so using subdirectories with large PHP libraries containing many files can impact performance.

### Best Practice: Use Shared Assets for Large Libraries

For large PHP libraries and frameworks, it's recommended to place them in the Element Pack's [shared assets](../shared-files/assets.md) directory and reference them from backend files:

```javascript
// hooks.js - Pass the asset path to templates
const transformHook = (rw) => {
    rw.setProps({
        siteAssetPath: rw.component.siteAssetPath,
        node: rw.node
    });
};
exports.transformHook = transformHook;
```

```php
<!-- templates/backend/handler.php -->
<?php
require_once('{{siteAssetPath}}/php-library/autoload.php');

// Use the library with component properties
$handler = new Handler([
    'api_key' => '{{apiKey}}',
    'timeout' => {{timeout}}
]);

echo $handler->process($_POST);
?>
```

This keeps backend files minimal and places complex logic in shared assets where it can be reused across components.

## Best Practices

### Always Validate Input

Sanitize and validate all user input to prevent security vulnerabilities:

```php
<?php
$email = filter_var($_POST['email'], FILTER_VALIDATE_EMAIL);
$name = htmlspecialchars(strip_tags(trim($_POST['name'])));
?>
```

### Return JSON Responses

Use structured JSON responses for consistency:

```php
<?php
header('Content-Type: application/json');
echo json_encode(['success' => true, 'message' => 'Data processed']);
?>
```

### Keep Backend Files Minimal

Use backend files primarily for configuration and routing. Place complex logic in [shared assets](../shared-files/assets.md) where it can be reused across components.

## Related Documentation

* [PHP Templates](php-templates.md) - Using PHP files at the template root level
* [Templates Overview](./) - Understanding the templates directory
* [Shared Assets](../shared-files/assets.md) - Storing large PHP libraries
* [Hooks.js](../hooks.js/) - Passing data to backend files
* [Elements Language](../language/) - Template syntax in PHP
* [Properties](../properties.json/) - Defining configuration properties
* [Building Form Components](../../guides/building-form-components.md) - A complete form suite with backend processing
* [Server-Side PHP Components](../../guides/server-side-php-components.md) - Advanced request-time PHP patterns
