# Dropzones

## Naming

A dropzones is an area within a template where child element can be added. Each dropzone requires a name giving you a consistent & reliable way to manage child items.&#x20;

```
@dropzone("extraItems")
```

```
@dropzone(name: "content")
```

```
@dropzone("zone-1", title: "Zone 1")
```

{% hint style="info" %}
Multiple dropzones with the same name can used, but you should be careful not to show them at the same time. This can be useful if you want to show child items in different places based on a control.
{% endhint %}

```
@if(edit)
   @dropzone("extraItems")
@elseif(preview)
   @dropzone("extraItems")
@endif
```

