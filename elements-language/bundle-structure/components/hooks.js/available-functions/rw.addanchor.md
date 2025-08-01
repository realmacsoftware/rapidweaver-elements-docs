# rw.addAnchor

The `addAnchor` method enables a component to be linkable, via the "Anchor" menu, from within a Link sheet.

Full Example

```
const transformHook = (rw) => {
  const { customID } = rw.props;
  
  if (customID.length > 0) {
    rw.addAnchor(globalID);
  }
  
};

exports.transformHook = transformHook;
```
