# ID

The `id` is the unique key for a control. Use it to reference values in templates and in conditional logic (like `visible` and `enabled`). Keep it stable and unique within the component.

### Example

```json
{
  "title": "Button Label",
  "id": "buttonLabel",
  "text": {
    "default": "Buy Now"
  }
}
```

Template usage:

```html
<a class="btn">{{buttonLabel}}</a>
```
