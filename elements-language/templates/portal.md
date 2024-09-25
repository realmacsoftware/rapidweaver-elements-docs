# Portal

The  portal feature allows you to transport part of your template code to the body or head area of the page.

```
@portal(headStart)
//Code here will be transported to the top of the page head.
@endportal
```

```
@portal(headEnd)
//Code here will be transported to the bottom of the page head.
@endportal
```

```
@portal(bodyStart)
//Code here will be transported to the top of the page body.
@endportal
```

```
@portal(bodyEnd)
//Code here will be transported to the bottom of the page body.
@endportal
```

If you are linking and including scripts, you'll want to tell Elements to only include the link once (when multiple instances of the same component are on the page). To do that you can use the "includeOne argument.

```
@portal(head, includeOnce: true)
//Code will only be included once when using multiple instances of the same component.
@endportal
```

Include once across multiple components.

```
@portal(headEnd, id: "com.realmacsoftware.alpine", includeOnce: true)
//Code will only be included once when using the same ID across multiple compoenents.
@endportal

```
