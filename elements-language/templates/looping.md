# Looping

Elements gives you access to the current RapidWeaver mode inside of conditional statements. This can be particularly useful for showing content in edit mode or in preview when a certain property evaluates to true.

```
@each(item in items)
   This is item: {{item.title}}
@endeach
```

|             |   |   |
| ----------- | - | - |
| `::index`   |   |   |
| `::isFirst` |   |   |
| `::isLast`  |   |   |
