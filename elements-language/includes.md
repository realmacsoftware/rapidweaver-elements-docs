# Includes

An include allows you to insert the content of another template file within the current template file.

Suppose you have the following template files

**hello.html**

```
Hello
```

**world.html**

```
World
```

**template.html**

```
%include -template="hello"% %include -template="world"%
```

The output from template.html would look like this

```
Hello World
```

## Property access

The included template files allow access to properties as if they were part of the main template file.

```
%include -template="menuitem" -property="rw:menuitems"%
```

## TODO

* [ ] includes from parent stack?
* [ ] add include templates to plist or use directory structure
* [ ] describe how to use -property along with new builtins like rw:menuitems
