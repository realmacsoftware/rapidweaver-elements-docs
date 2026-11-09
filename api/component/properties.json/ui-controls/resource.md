# Resource

Displays a resource dropwell that accepts all file types.

{% tabs %}
{% tab title="Control Example" %}
```json
{
  "title": "Image",
  "id": "image",
  "resource": {}
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
  "groups": [{
    "title": "Content",
    "icon": "photo",
    "properties": [{
      "title": "Image",
      "id": "image",
      "resource": {}
    }]
  }]
}
```
{% endtab %}
{% endtabs %}

### Supported Options

The resource control accepts all file types by default. Use the following options to restrict it.

| Key        | Type   | Notes                                                                                          |
| ---------- | ------ | ---------------------------------------------------------------------------------------------- |
| `accepts`  | string | HTML `<input accept>`-style comma-separated list restricting which file types can be assigned. |
| `excludes` | string | Same token grammar as `accepts`, but subtracts matching types.                                 |

An empty or omitted `accepts` accepts any file type.

#### `accepts`

`accepts` uses the same token grammar as the HTML [`<input accept>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file#accept) attribute:

| Token          | Matches                          | Example      |
| -------------- | -------------------------------- | ------------ |
| `.ext`         | A file extension                 | `.svg`       |
| `type/*`       | A MIME major type                | `image/*`    |
| `type/subtype` | An exact MIME type               | `video/mp4`  |

Combine multiple tokens with commas, e.g. `".png,.jpg"`.

```json
{
  "title": "Icon",
  "id": "icon",
  "resource": {
    "accepts": ".svg"
  }
}
```

#### `excludes`

`excludes` uses the same token grammar and subtracts specific types from `accepts`. A file matching any `excludes` token is rejected even if an `accepts` token matches. `excludes` without `accepts` means "accept everything except the excluded types".

```json
{
  "title": "Photo",
  "id": "photo",
  "resource": {
    "accepts": "image/*",
    "excludes": ".svg"
  }
}
```

Restrictions are enforced when a resource is assigned in the inspector, the canvas editor, and via the API, and also filter which drop targets accept a dragged file.

{% hint style="info" %}
The legacy `"types": ["svg"]` array shorthand is still supported and folded in alongside `accepts`, but new components should use `accepts`.
{% endhint %}

## Using Resources in Templates

### Resource Properties

When you define a resource control, you can access its properties in your template:

| Property | Description |
|----------|-------------|
| `{{resource.image}}` | The URL/path to the image |
| `{{resource.path}}` | The file path (use for non-image files like video, PDF) |
| `{{resource.width}}` | Original width in pixels (images only) |
| `{{resource.height}}` | Original height in pixels (images only) |
| `{{resource.aspect}}` | Aspect ratio, e.g. `16/9` (images only) |

### Displaying an Image

```html
<img
  src="{{photo.image}}"
  alt="{{altText}}"
  width="{{photo.width}}"
  height="{{photo.height}}"
/>
```

### Displaying a Video

For non-image resources like video files, use the `.path` property:

```html
<video controls>
  <source src="{{myVideo.path}}" type="video/mp4">
</video>
```

### Checking if a Resource Exists

Use a conditional to handle cases where no resource has been selected:

```html
@if(photo.image)
  <img src="{{photo.image}}" alt="{{altText}}" />
@else
  <p>No image selected</p>
@endif
```

## Resource Dropzones

You can enable drag-and-drop directly onto an element in the editor by adding the `rwResourceDropZone` attribute. The value should match the `id` of your resource control.

```html
<div rwResourceDropZone="photo">
  @if(photo.image)
    <img src="{{photo.image}}" alt="{{altText}}" />
  @else
    <p>Drop an image here</p>
  @endif
</div>
```

## Complete Example

**properties.json:**

```json
{
  "groups": [{
    "title": "Image",
    "icon": "photo",
    "properties": [{
      "title": "Photo",
      "id": "photo",
      "resource": {}
    }, {
      "title": "Alt Text",
      "id": "altText",
      "text": { "default": "" }
    }]
  }]
}
```

**templates/index.html:**

```html
<div rwResourceDropZone="photo">
  @if(photo.image)
    <img
      src="{{photo.image}}"
      alt="{{altText}}"
      width="{{photo.width}}"
      height="{{photo.height}}"
    />
  @else
    <p>Drop an image here</p>
  @endif
</div>
```

