---
description: Include content from another template file
---

# Includes

An include allows you to insert the content of another template file within the current template file.

Include files should be stored in the "include" directory. Refer to the [Bundle Structure](../bundle-structure/) for more information.

Suppose you have the following template files in your include folder:

**hello.html**

```
Hello
```

**world.html**

```
World
```

You could then include the contents of those files into your main template.html file by using the following code:

```
@include("hello")
@include("world")
```

The output from template.html would look like this

```
Hello World
```

### Property access

The include template files allow access to properties as if they were part of the main template file. Given that you have set a `pages` value in your hooks file (via the `rw.setProps()` method), you can pass that property to your template like so:

```
@include("menuitem", property: pages)
```

You can of cause include multiple properties simply by comma separating them:

```
@include("banner", title: "Can be a string", body: canAlsoBeAVariable)
```

### Conditional Includes

Rather than wrapping your @include statement inside an @if statement, you can use the @includeIf helper:

```
// Instead of doing this:
@if(myVariable)
  @include("myTemplate")
@endif

// you can do this:
@includeIf(myVariable, "myTemplate")
```

