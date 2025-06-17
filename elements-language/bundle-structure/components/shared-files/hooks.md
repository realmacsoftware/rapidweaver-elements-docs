---
hidden: true
---

# Hooks

This folder should only contain JS files! There is no restriction on naming.

{% hint style="info" %}
All files in this directory are compressed into a single file and executed prior to executing the [hooks.js file](../hooks.js/) within a component.
{% endhint %}

There is no access to component properties or the Elements API directly within these files. However, you may create a function and pass them in as properties.

### Example

Two components within an element pack display a description of the current temperature, chosen by the user using a [slider](../properties.json/ui-controls/slider.md) called `temperature` with a range of 0 to 40.

Instead of writing the same code twice in the [hooks.js file](../hooks.js/) of each component, define a function within a `temperature.js` file and place it in the shared hooks directory, then add the following code.

```javascript
const getTemperatureDescription = (rw) => {
    // Get the temperature property
    const { temperature } = rw.props
    
    // return a description of the temperature
    if (temperature < 17) {
        return "It's cold";
    } else if (temperature < 24) {
        return "Just right";
    } else {
        return "Too hot!";
    }
};
```

Each component can then use the above function in their respective [hooks.js files](../hooks.js/).

```javascript
const transformHook = (rw) => {
  // Get the temperature description, passing in rw so the function has access to the API
  const description = getTemperatureDescription(rw)

  // Set a property to the description so it can be accessed from the template
  rw.setProps({
    description: description
  });
};

exports.transformHook = transformHook;

```
