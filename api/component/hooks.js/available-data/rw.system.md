# rw.system

The `rw.system` object provides metadata about the **Elements app** itself — not the project, page, or component.

Use this when a pack or custom component needs to branch on the host product (compatibility, feature detection, diagnostics). Do not read `rw.component.version` / `rw.component.build` for that: those are the **component’s** integers.

## Properties

| Property | Type | Description |
|----------|------|-------------|
| `version` | String | Elements marketing version (`CFBundleShortVersionString`) |
| `build` | String | Elements build number (`CFBundleVersion`) |

Both values are strings, matching the app Info.plist. That is distinct from `rw.component.version` / `rw.component.build`, which are integers.

## Accessing App Version

```javascript
const transformHook = (rw) => {
    const { version, build } = rw.system;

    console.log(version); // "4.0.0"
    console.log(build);   // "100"
};

exports.transformHook = transformHook;
```

## Feature Detection

```javascript
const transformHook = (rw) => {
    const { version, build } = rw.system;

    rw.setProps({
        appVersion: version,
        appBuild: build
    });
};

exports.transformHook = transformHook;
```

In templates:

```html
<!-- Only if you passed rw.system through setProps -->
<span>Built with Elements {{appVersion}} ({{appBuild}})</span>
```
