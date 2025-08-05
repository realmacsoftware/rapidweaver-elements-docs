---
description: Deploy extra files to the backend.
---

# Backend

{% hint style="info" %}
Sub-directories are not supported in the backend directory. Instead, use the shared assets directory for the bulk of your code and reference it from backend scripts, passing in the values from properties. [See more](backend.md#subdirectories-are-not-supported)
{% endhint %}

Files added to the backend directory are processed in the same context as other template files. However, instead of forming part of the page, they will be deployed as extra files to the page's backend directory during publish.

To ensure there are no conflicts with other components, all backend files are stored in a subdirectory corresponding to the current node id. For example:

```
contact
    index.html
    backend
        rw29BB9A86_0D4A_4E46_9BF5_CD5041A9ECE2
            submit.php
```

The following file types are supported:

* html
* php
* js
* css

#### Example Usage

A good use-case for this would be to process a contact form. Create a new component and add the following code to the `templates/backend/submit.php`file.

```
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // Sanitize input data
    $name = htmlspecialchars(strip_tags(trim($_POST["name"])));
    $email = filter_var(trim($_POST["email"]), FILTER_SANITIZE_EMAIL);
    $message = htmlspecialchars(strip_tags(trim($_POST["message"])));
    
    // Validation
    if (empty($name) || empty($email) || empty($message)) {
        echo "All fields are required.";
        exit;
    }
    if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
        echo "Invalid email format.";
        exit;
    }
    
    
    // Process data (e.g., send email, save to database)
    
    
    echo "Thank you, $name. Your message has been received.";
}
?>
```

Then place this in the `templates/form.html` frontend file.

```
<script>
    function submitForm(event) {
        event.preventDefault();
        let formData = new FormData(document.getElementById("contactForm"));
        
        fetch("{{node.backendPath}}/process.php", {
            method: "POST",
            body: formData
        })
        .then(response => response.text())
        .then(data => {
            document.getElementById("messageDisplay").innerText = data;
        })
        .catch(error => {
            document.getElementById("messageDisplay").innerText = "An error occurred.";
        });
    }
</script>

<form id="contactForm" onsubmit="submitForm(event)">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required>
    <br>
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>
    <br>
    <label for="message">Message:</label>
    <textarea id="message" name="message" required></textarea>
    <br>
    <button type="submit">Submit</button>
</form>
<p id="messageDisplay"></p>
```

When the submit button is pressed in the above form, the form sends all the form values to the \{{node.backendPath\}}`/submit.php` file on the server. The `node.backendPath` property will be replaced with the node's unique id.

To use the `node.backendPath` property, we'll need to use the hooks.js file. Create a hooks.js file in your component and add this.

```
const transformHook = (rw) => {
    rw.setProps({
        node: rw.node
    });
};

exports.transformHook = transformHook;
```

#### Subdirectories are not supported

Elements monitors every file in the backend directory for changes. This can cause problems when adding large php libraries with hundreds of files. A better solution is to add the php library to the Element pack's [shared assets](../shared-files/assets.md) directory.

The assets are deployed only once after a component from the pack is added to the page. Use the hooks file to find the site assets path and pass it to the backend file.

```
const transformHook = (rw) => {
    rw.setProps({
        siteAssetPath: rw.component.siteAssetPath,
        node: rw.node
    });
};

exports.transformHook = transformHook;
```

We've found it good practice to keep the backend php files to a minimum and use them to build a minimal config object using the properties from the component. Then call a method included from a php file within site assets, passing in the config object.
