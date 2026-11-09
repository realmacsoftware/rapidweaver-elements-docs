# rw.getBreakpoints()

Access theme breakpoint configuration for responsive design. This data is also available via `rw.theme.breakpoints`.

## Accessing Breakpoints

```javascript
const transformHook = (rw) => {
    const { breakpoints } = rw.theme;
    const { names, screens } = breakpoints;
    
    console.log(names);   
    // ["sm", "md", "lg", "xl", "2xl"]
    
    console.log(screens); 
    // { sm: 640, md: 768, lg: 1024, xl: 1280, "2xl": 1536 }
};

exports.transformHook = transformHook;
```

## Properties

| Property | Type | Description |
|----------|------|-------------|
| `names` | Array | Ordered list of breakpoint names |
| `screens` | Object | Breakpoint names mapped to pixel widths |

## Common Patterns

### Generate Responsive Sources

```javascript
const transformHook = (rw) => {
    const { breakpoints } = rw.theme;
    const { names, screens } = breakpoints;
    const { image } = rw.props;
    
    const sources = names
        .filter(name => screens[name])
        .sort((a, b) => screens[b] - screens[a])
        .map(name => ({
            media: `(min-width: ${screens[name]}px)`,
            srcset: rw.resizeResource(image, screens[name] * 2),
            breakpoint: name,
            minWidth: screens[name]
        }));
    
    rw.setProps({ sources });
};

exports.transformHook = transformHook;
```

### Build Responsive Classes

```javascript
const transformHook = (rw) => {
    const { breakpoints } = rw.theme;
    const { columns } = rw.responsiveProps;
    
    // columns = { base: 1, md: 2, lg: 3 }
    
    const gridClasses = Object.entries(columns)
        .map(([breakpoint, cols]) => {
            const prefix = breakpoint === 'base' ? '' : `${breakpoint}:`;
            return `${prefix}grid-cols-${cols}`;
        })
        .join(' ');
    
    rw.setProps({
        gridClasses  // "grid-cols-1 md:grid-cols-2 lg:grid-cols-3"
    });
};

exports.transformHook = transformHook;
```

### Responsive Visibility

```javascript
const transformHook = (rw) => {
    const { hidden } = rw.responsiveProps;
    
    // hidden = { base: true, md: false }
    
    const visibilityClasses = Object.entries(hidden)
        .map(([breakpoint, isHidden]) => {
            const prefix = breakpoint === 'base' ? '' : `${breakpoint}:`;
            return isHidden ? `${prefix}hidden` : `${prefix}block`;
        })
        .join(' ');
    
    rw.setProps({ visibilityClasses });
};

exports.transformHook = transformHook;
```

## Default Breakpoints

Elements typically uses Tailwind CSS breakpoints:

| Name | Width |
|------|-------|
| `sm` | 640px |
| `md` | 768px |
| `lg` | 1024px |
| `xl` | 1280px |
| `2xl` | 1536px |

## Notes

- Breakpoints are defined by the active theme
- Use `names` when you need ordered iteration
- Use `screens` when you need to lookup specific widths
- Combine with `rw.responsiveProps` for per-breakpoint values
