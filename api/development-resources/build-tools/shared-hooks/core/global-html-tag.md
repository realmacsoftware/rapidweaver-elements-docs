---
description: globalHTMLTag utility function
---

# globalHTMLTag

Utility function for core.

## Signature

```javascript
globalHTMLTag(app, fallback = "div")
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `app` | - |
| `fallback` | - |

## Usage

```javascript
const transformHook = (rw) => {
    const classes = globalHTMLTag(rw);
};
```
