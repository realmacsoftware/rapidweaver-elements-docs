# Data collections in Hooks.js

To access your data collections in the hooks.js file of your element, you can access the `rw.collections` object. This will give you access to all of the data collections setup for your element.

Note: all data collections are automatically injected in to all templates via the `collections` object. Meaning you can call `collections.{collection-name}` in any template automatically.

### Manipulating Data Collections

Something you might want or need to manipulate the data collection before it's sent to your templates. You can do this in the hooks.js file by accessing the `rw.collections` object. You can then use native javascript to manipulate this data as required.



One example would when your template needs to know if the data collection is empty. We could send through a `hasFeatures` boolean to our template, allowing us to conditionally display a portion of our template code.

#### Hooks.js

```
const transformHook = (rw) => {
  const hasFeatures = rw.collections.features ?? false;
  
  rw.setProps({ hasFeatures })
};

exports.transformHook = transformHook;
```

#### Template

```
@if(hasFeatures)
  @each(feature in collections.features)
     <h3>{{feature.title}}</h3>
     <p>{{feature.description}}</p>
  @endeach
@else
  <p>We have no features</p>
@endif
```



