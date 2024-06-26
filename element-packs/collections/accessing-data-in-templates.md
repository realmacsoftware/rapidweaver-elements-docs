# Accessing Data in Templates

To access an individual data collection in a template file you can simply use `collections.{collection-name}` . This will give you an array of items that have been added to the given data collection.

Assuming we have a `features` data collection setup, we can do the following in our template files:

```
@each(feature in collections.features)
 <h3>{{feature.title}}</h3>
 <p>{{feature.description}}</p>
@endeach
```
