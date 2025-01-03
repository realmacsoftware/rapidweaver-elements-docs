# Portal

The  portal feature allows you to transport sections of your template code to another part of the page.

```html
@portal(pageStart)
<!-- Code here will be transported to the top of the page before the open HTML tag.-->
@endportal
```

```html
@portal(pageEnd)
<!-- Code here will be transported to the bottom of the page after the end html tag.-->
@endportal
```

```html
@portal(headStart)
<!-- Code here will be transported to the top of the page head.-->
@endportal
```

```html
@portal(headEnd)
<!-- Code here will be transported to the bottom of the page head.-->
@endportal
```

```html
@portal(bodyStart)
<!-- Code here will be transported to the top of the page body.-->
@endportal
```

```html
@portal(bodyEnd)
<!-- Code here will be transported to the bottom of the page body.-->
@endportal
```

If you are linking and including scripts, you'll want to tell Elements to only include the link once (when multiple instances of the same component are on the page). To do that you can use the "includeOne argument.

```html
@portal(headEnd, includeOnce: true)
<!-- Code will only be included once when using multiple instances of the same component.-->
@endportal
```

Include once across multiple components.

```html
@portal(headEnd, id: "com.realmacsoftware.alpine", includeOnce: true)
<!-- Code will only be included once when using the same ID across multiple compoenents.-->
@endportal

```
