# hooks.js



### Code Examples

Code used to get and set values:

```
const transformHook = (context) => {
  const {
    value,
  } = context.getValues();

  context.setValues({
    newValue: `h${value*2}`,
  });
};

exports.transformHook = transformHook;

```

This is the implementation/logic code for switching between default and custom sizing properties:

```
  const sizeClasses = [
    !customSizing && size,
    customSizing && fontSize,
    customSizing && paddingTop,
    customSizing && paddingRight,
    customSizing && paddingBottom,
    customSizing && paddingLeft,
  ]
    .filter(Boolean)
    .join(" ");
```
