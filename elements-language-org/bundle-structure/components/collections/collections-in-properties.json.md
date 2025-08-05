# Collections in properties.json

For your collection to appear in the page inspector alongside the other controls for your Component you need to also add an entry into the [properties.json](../properties.json/) file, for example:

```json
    {
      "title": "Rows",
      "icon": "tablecells",
      "properties": [
        {
          "title": "Links",
          "property": "links",
          "collection": {
            "identifier": "com.acme.table.collections.rows"
          }
        }
      ]
    },
```
