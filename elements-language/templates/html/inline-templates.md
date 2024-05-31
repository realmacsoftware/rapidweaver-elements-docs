# Inline templates

At the start of a template file you can add an inline template that can be included like any other template file. This is handy if you have small parts of your template you want to extract, and don't want or need to create separate templates files.



```
@template("list-item")
    <li>{{item.name}}</li>
@endtemplate

<h1>My List</h1>
<ul>
    @each(item in items)
        @include("list-item")
    @endeach
</ul>
```
