# rw.node

The `rw.node` object provides access to information about the current component instance (node) in the page structure.

## Properties

| Property | Type | Description |
|----------|------|-------------|
| `id` | String | Unique identifier for this component instance |
| `title` | String | The component's display title |
| `parent.id` | String | ID of the parent component |
| `parent.container` | String | Container identifier within parent |
| `backendPath` | String | Path to the node's backend folder |

## Accessing Node Data

```javascript
const transformHook = (rw) => {
    const { id, title, parent, backendPath } = rw.node;
    
    console.log(id);              // "abc123"
    console.log(title);           // "My Container"
    console.log(parent.id);       // "parent456"
    console.log(parent.container);// "content"
    console.log(backendPath);     // "/path/to/backend/"
};

exports.transformHook = transformHook;
```

{% hint style="info" %}
The `node` object is always available in templates without needing to pass it through `setProps`.
{% endhint %}

## Using Node ID for Unique Identifiers

The node ID is commonly used to create unique identifiers for DOM elements:

```javascript
const transformHook = (rw) => {
    const { id } = rw.node;
    
    rw.setProps({
        elementId: `container-${id}`,
        groupClass: `group/${id}`
    });
};

exports.transformHook = transformHook;
```

## Accessing Parent Information

Useful for creating grouped behaviors or scoped styling:

```javascript
const transformHook = (rw) => {
    const { id, parent } = rw.node;
    
    // Use parent ID for group hover effects
    const hoverClass = `group-hover/${parent.id}`;
    
    rw.setProps({
        nodeId: id,
        parentId: parent.id,
        hoverClass
    });
};

exports.transformHook = transformHook;
```

## Using in Templates

The node is automatically available in templates:

```html
<!-- Node ID for unique element IDs -->
<div id="{{node.id}}">
    <h2>{{node.title}}</h2>
</div>

<!-- For backend resources -->
<script src="{{node.backendPath}}/script.js"></script>
```
