# Portal

The  portal feature allows you to transport part of your template code to the body or head area of the page.

```
@portal("head")
//Any code here will be transported into the head of the page.
@endportal
```

```
@portal("body")
//Any code here will be transported to the top of the page body.
@endportal
```

If you are linking and including scripts, you'll want to tell Elements to only include the link once (when multiple instances of the same compoenent are on the page). To do that you can use the "includeOne argument.

```
@portal("head", includeOnce: true)
<script src="https://js.api.here.com/v3/3.1/mapsjs-core.js"</script>
@endportal
```
