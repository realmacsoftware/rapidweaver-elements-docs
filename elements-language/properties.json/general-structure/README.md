# General Structure

All properties have the same general structure using the following object keys.

<table><thead><tr><th width="156">Key</th><th width="110">Value</th><th>Notes</th></tr></thead><tbody><tr><td><code>title</code></td><td>string</td><td>See <a href="title.md">Title</a> for more information</td></tr><tr><td><code>id</code></td><td>string</td><td>See <a href="property.md">ID</a> for more information</td></tr><tr><td><code>format</code></td><td>string</td><td>See <a href="format.md">Format</a> for more information</td></tr><tr><td><code>visible</code></td><td>string</td><td>See <a href="visible.md">Visible</a> for more information</td></tr><tr><td><code>enabled</code></td><td>string</td><td>See <a href="enabled.md">Enabled</a> for more information</td></tr></tbody></table>

### Code Example

```json
{
  "title": "Example Title",
  "id": "unique-id-here",
  "format": "pt-{{value}}",
  "visible": "myOtherControl == 'someValue'",
  "enabled": "anotherControl == 'anotherValue'"
}
```
