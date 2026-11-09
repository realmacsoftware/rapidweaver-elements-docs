# Passing data to templates

To send data to your templates, you can utilise the `rw.setProps()` method. By passing an object to this method, you are able to dynamically inject data into your templates.

#### Example 1: Simple Property Passing

```javascript
const transformHook = (rw) => {
  const message = 'Hello, World!';

  rw.setProps({
    greetingMessage: message
  });
};

exports.transformHook = transformHook;
```

#### Example 2: Conditional Logic for Display

```javascript
const transformHook = (rw) => {
  const { isVisible } = rw.props;

  const display = isVisible ? 'visible' : 'hidden';

  rw.setProps({
    display
  });
};

exports.transformHook = transformHook;
```

#### Example 3: Basic Computation and Formatting

```javascript
const transformHook = (rw) => {
  const { quantity } = rw.props;

  const totalPrice = quantity * 15; // Assuming price per item is 15
  const formattedPrice = `$${totalPrice.toFixed(2)}`;

  rw.setProps({
    formattedPrice
  });
};

exports.transformHook = transformHook;
```

#### Example 4: String Manipulation

```javascript
const transformHook = (rw) => {
  const { username } = rw.props;

  const welcomeMessage = `Welcome, ${username.charAt(0).toUpperCase() + username.slice(1)}!`;

  rw.setProps({
    welcomeMessage
  });
};

exports.transformHook = transformHook;
```

#### Example 5: Complex Calculation using collection data

```javascript
const transformHook = (rw) => {
  const { items } = rw.collections;

  const totalWeight = items.reduce((accumulator, item) => accumulator + item.weight, 0);

  const shippingCost = totalWeight > 10 ? totalWeight * 1.5 : totalWeight * 1.2;

  const formattedShippingCost = `$${shippingCost.toFixed(2)}`;

  rw.setProps({
    totalWeight,
    formattedShippingCost
  });
};

exports.transformHook = transformHook;.
```
