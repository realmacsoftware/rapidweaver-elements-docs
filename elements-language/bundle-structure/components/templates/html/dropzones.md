# Dropzones

### Dropzone Naming

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

### Resource Dropzone

Sometimes you want to allow the user to drop the resources directly into the Editor, this can be achieved with the `rwResourceDropZone` key.

The following example shows how to support dropping a folder of images directly into the Editor. Place the following in the Template HTML:

```
<div class="grid grid-cols-4 gap-4" rwResourceDropZone="images">
    @if(!images.isFolder)
        <!-- if the `images` resource property is not a folder, display this message -->
        <h3 class="font-bold text-lg uppercase text-brand-500 p-10 col-span-full place-self-center">
            Drop a folder of images here!
        </h3>
    @else
        <!-- Otherwise we have a folder of resources (yay!) -->
        @each(image in images.resources)
            <img src="{{image.image}}" alt="{{image.caption}}" />
        @endeach
    @endif
</div>
```

You also need a corresponding image control in the Properties file:

```
{
    "groups": [{
        "title" : "Content",
        "properties" : [{
            "title" : "Images",
            "property": "images",
            "resource": {
                "types": ["image"]
            }
        }]
    }]
}
```
