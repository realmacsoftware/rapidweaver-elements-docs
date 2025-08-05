# rw.setRootElement

If you want to control the outermost DOM element for a component, you can do so via `setRootElement`&#x20;

```javascript
const transformHook = (rw) => {

  const classes = "" // custom classes for this component
  
  rw.setRootElement({
    as: "div", // or section, nav, aside, or any other valid tag
    class: classes,
    args: {
      role: "separator",
      "aria-orientation": "horizontal",
    },
  });
  
};

exports.transformHook = transformHook;
```
