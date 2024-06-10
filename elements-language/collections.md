# Collections

Collcetions are a flexible way to create datasets for your element. You can add multiple collections to your elements.

To add data collections to your element you must first create a `collections` folder at the root of your element.

**Example structure**

```
/com.company.element.element-name
  /collections
    /{data-collection-name}
      • info.json
      • properties.json
```

Inside the collections folder you must create a folder with the name of your data collection. Inside the data collection folder you must create both a `info.json` and `properties.json` file.

### Basic Example

If we want to create an data collection for `features` we need to create the following structure in your element:

```
/com.company.element.element-name
  /collections
    /features
      • info.json
      • properties.json
```

#### Info.json

We then need to identify this data collection with RapidWeaver. To do this we must add the following code to the info.json file.

```
{
  "identifier": "com.company.element.features",
  "title": "Features"
}

```

#### Properties.json

To add properties to our collection we need to describe the fields for each item added to our features collection.

Data collection properties are described in the same way as Element properties.

This means we must create a `properties.json` file and describe our properties in exactly the same way as Element properties.

**Note:** all properties available to Elements are also available to data collections. Read the [properties.json docs](properties.json/) for more information.

So, given that a feature should have a title, description, and icon, we should add the following to properties.json:

```
{
  "groups": [
    {
      "title": "Feature",
      "properties": [
        {
          "title": "Title",
          "id": "title",
          "text": {
            "default": ""
          }
        },
        {
          "title": "Description",
          "id": "description",
          "textArea": {
            "default": ""
          }
        },
        {
          "title": "Icon",
          "id": "icon",
          "resource": {}
        }
      ]
    }
  ]
}


```

With this all setup your element will have a Features data collection that allows the user to add unlimited items with a title, description, and icon.
