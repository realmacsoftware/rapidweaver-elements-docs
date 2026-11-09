---
description: Display collections in the component inspector
---

# Collections in properties.json

After creating your collection folder structure, you need to register it in your component's main `properties.json` file. This makes the collection appear in the inspector panel alongside your other component controls.

## Syntax

Add a collection reference using the `collection` control type:

```json
{
    "title": "Collection Title",
    "property": "collectionName",
    "collection": {
        "identifier": "com.company.component.collections.name"
    }
}
```

## Parameters

| Property | Required | Description |
|----------|----------|-------------|
| `title` | Yes | Display name shown in the inspector |
| `property` | Yes | The property name used to access the collection in templates |
| `collection.identifier` | Yes | Must match the `identifier` in your collection's `info.json` |

## Examples

### Basic Collection Reference

Add a features collection to your component:

```json
{
    "groups": [
        {
            "title": "Content",
            "icon": "square.stack",
            "properties": [
                {
                    "title": "Features",
                    "property": "features",
                    "collection": {
                        "identifier": "com.company.features.collections.features"
                    }
                }
            ]
        }
    ]
}
```

### Tags Collection with Icon

The Grid, Flex, and Container components use a tags collection for filtering:

```json
{
    "groups": [
        {
            "title": "Tags",
            "icon": "tag",
            "properties": [
                {
                    "title": "Tags",
                    "property": "tags",
                    "collection": {
                        "identifier": "com.realmacsoftware.grid.collections.tags"
                    }
                }
            ]
        }
    ]
}
```

### Audio Playlist Tracks

The Audio Playlist component registers its tracks collection:

```json
{
    "groups": [
        {
            "title": "Tracks",
            "icon": "music.note",
            "properties": [
                {
                    "title": "Tracks",
                    "property": "tracks",
                    "collection": {
                        "identifier": "com.realmacsoftware.audioPlaylist.collections.tracks"
                    }
                }
            ]
        }
    ]
}
```

### Multiple Collections

Components can have multiple collections. Each gets its own group for clarity:

```json
{
    "groups": [
        {
            "title": "Slides",
            "icon": "photo.stack",
            "properties": [
                {
                    "title": "Slides",
                    "property": "slides",
                    "collection": {
                        "identifier": "com.company.slider.collections.slides"
                    }
                }
            ]
        },
        {
            "title": "Thumbnails",
            "icon": "square.grid.3x3",
            "properties": [
                {
                    "title": "Thumbnails",
                    "property": "thumbnails",
                    "collection": {
                        "identifier": "com.company.slider.collections.thumbnails"
                    }
                }
            ]
        }
    ]
}
```

### Collection with Related Controls

Place collection controls alongside related settings:

```json
{
    "groups": [
        {
            "title": "Accordion",
            "icon": "list.bullet",
            "properties": [
                {
                    "title": "Items",
                    "property": "items",
                    "collection": {
                        "identifier": "com.company.accordion.collections.items"
                    }
                },
                {
                    "divider": {}
                },
                {
                    "title": "Default State",
                    "property": "defaultState",
                    "responsive": false,
                    "segmented": {
                        "default": "closed",
                        "items": [
                            { "title": "Open", "value": "open" },
                            { "title": "Closed", "value": "closed" }
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Accessing Collection Data

Once registered, the collection data is available:

- **In templates**: `collections.{property}` (e.g., `collections.features`)
- **In hooks.js**: `rw.collections.{property}` (e.g., `rw.collections.features`)

See [Accessing Data in Templates](accessing-data-in-templates.md) and [Data Collections in hooks.js](data-collections-in-hooks.js.md) for usage details.

## Best Practices

1. **Use descriptive property names** - The property name becomes part of the template syntax, so make it clear and concise.

2. **Add appropriate icons** - Use SF Symbols that represent the collection content (e.g., `music.note` for tracks, `tag` for tags).

3. **Group collections logically** - Place collections in dedicated groups or alongside related controls.

4. **Match identifiers exactly** - The identifier must match your collection's `info.json` exactly, including case.
