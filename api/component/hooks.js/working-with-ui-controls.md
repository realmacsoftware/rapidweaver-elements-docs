# Working with UI Controls

```javascript
const transformHook = (rw) => {
  const { isVisible, firstName, lastName } = rw.props;
  
  const visibilityText = isVisible ? 'Visible' : 'Not Visible';
  const fullName = `${firstName} ${lastName}`;
  
  // Send properties to the template
  rw.setProps({ 
    visibilityText,
    fullName
  });
};

exports.transformHook = transformHook;
```

You can read more about [passing data to templates](passing-data-to-templates.md).
