---
icon: code
description: Component Template Folder
---

# Templates

Template files in RapidWeaver Elements house all the HTML, CSS, JavaScript, and other assets your component needs to work seamlessly. These files are dynamically processed by Elements, allowing for property replacements (think handlebars-style), perform iterations, and more—enabling you to build highly flexible and reusable components.

### Templates Directory Structure

The structure of the templates directory is important and denotes in which area the contained files will be inserted into the page. Any files placed at the root of the templates directory will be processed and added for each instance of the component on the page.

The templates directory may also contain the following sub directories

* **headStart** - placed at the top of head&#x20;
* **headEnd** - placed at the end of head&#x20;
* **bodyStart** - placed at the top of body&#x20;
* **bodyEnd** - placed at the bottom of body
* **include** - files can be included from other template files using an [@include](includes.md) statement

### Supported Template File Types

* **html** - contains HTML content
* **js** - contains javascript
* **css** - CSS styles
* **php** - files containing PHP&#x20;
