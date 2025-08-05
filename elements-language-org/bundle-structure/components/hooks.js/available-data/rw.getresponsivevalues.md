# rw.responsiveProps

This method enables you to fetch the unformatted values of a control. This is handy if you require values that are not formatted for Tailwind.

```javascript
const transformHook = (rw) => {
  const { width } = rw.responsiveProps;
  
  // Width will be something like:
  // const width = {
  //   base: string|number|boolean|etc,
  //   sm: string|number|boolean|etc,
  //   md: string|number|boolean|etc,
  //   lg: string|number|boolean|etc
  // }
  
;

exports.transformHook = transformHook;
```
