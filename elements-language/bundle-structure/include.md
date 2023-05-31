---
description: Include content from another template file
---

# Include

An include allows you to insert the content of another template file within the current template file.

Include files should be stored in the "include" directory. Refer to the [Bundle Structure](../structure.md) for more information.

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
%include -template="hello"% %include -template="world"%
```

The output from template.html would look like this

```
Hello World
```

## Property access

The include template files allow access to properties as if they were part of the main template file.

```
%include -template="menuitem" -property="rw:menuitems"%
```

