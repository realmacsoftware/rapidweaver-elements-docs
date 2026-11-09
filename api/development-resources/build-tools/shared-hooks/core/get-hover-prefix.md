---
description: getHoverPrefix utility function
---

# getHoverPrefix

Utility function for core.

## Signature

```javascript
getHoverPrefix(node = {},
    applyTo = "",
    hoverGroup = "self",
    customId = "")
```

## Parameters

| Parameter | Description |
|-----------|-------------|
| `node` | - |
| `applyTo` | - |
| `hoverGroup` | - |
| `customId` | - |

## Usage

```javascript
const transformHook = (rw) => {
    const classes = getHoverPrefix(rw);
};
```
