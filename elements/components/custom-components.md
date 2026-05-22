---
description: Extend RapidWeaver by creating your very own custom Components
---

# Custom Components

If you know a bit of HTML you can create your own custom Components for use in your projects. These can be anything from a simple html snippet to a fully blown Component with custom UI controls taking full advantage of the[ Elements API](https://docs.realmacsoftware.com/elements-docs/elements-language).

{% hint style="success" %}
**The possibilities of what you can create are endless.**\
Learn more about using the [Elements API here](https://docs.realmacsoftware.com/elements-docs/elements-language).
{% endhint %}

### **Adding a simple HTML snippet**

One of the easiest ways get started using Custom Components is by adding an HTML snippet to your page.

{% embed url="https://www.youtube.com/watch?v=rHDCpYrg-j4" %}

### A Guide to Creating Custom Components

In this laid-back conversation, Dan and Ben discuss the intricacies of building custom components in RapidWeaver Elements, focusing on the integration of properties, resources, and advanced features like drop zones and hooks.

{% embed url="https://youtu.be/aqOOChtClwI?si=sKpgkAruLBAROR7P" %}

{% hint style="success" %}
Learn more about using the [Elements API here](https://docs.realmacsoftware.com/elements-docs/elements-language).
{% endhint %}

### Creating a Custom Component

Creating a Custom Component in Elements is the easiest and fastest way to get started with exploring the [Elements API](https://docs.realmacsoftware.com/elements-docs/elements-language). Custom Components can easily be migrated to distributable Element Pack at a later date.

#### A few things to note before you get started:

1. No external code editor is required, you can build everything inside of RapidWeaver Elements.
2. Custom Components are stored in the project they were created in.
3. Custom Components have full access to the Elements Language and can define their own Properties (the UI controls shown in the Inspector) right inside the Component Editor — they just can't bundle separate _files_ (such as extra assets, icons, or additional template files) the way an external Element Pack can.
4. To ensure compatibility with Elements you should use Tailwind CSS classes when writing your Template HTML.
5. Custom Components can easily be converted into an encrypted component and shared or sold on the Elements Marketplace.

#### Let's get Started:

{% stepper %}
{% step %}
#### Open the Components area in the sidebar of your project

Press the "+" button next to the "Custom" heading, and choose HTML. You should now see the component appear in the list.

<figure><img src="../../.gitbook/assets/CleanShot 2025-06-01 at 12 .02.15@2x.png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### Drag your newly created component onto the Page

Drag your HTML component into the page, you're now ready to start customizing it.

<figure><img src="../../.gitbook/assets/CleanShot 2025-06-01 at 12 .03.57@2x.png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### Edit your Custom Component

Next, open the Component Editor so we can view and edit the code. All changes made to the code update in realtime. Go ahead, change the text and watch the preview update.

<figure><img src="../../.gitbook/assets/CleanShot 2025-06-01 at 12 .04.38@2x.png" alt=""><figcaption></figcaption></figure>

The Component Editor is a panel so can be placed or added anywhere in the UI. Right-click an icon in the inspector to select it from the drop down menu.

<figure><img src="../../.gitbook/assets/CleanShot 2025-06-01 at 12 .08.23@2x.png" alt=""><figcaption></figcaption></figure>
{% endstep %}
{% endstepper %}

### Adding Editable Content Areas

Using the following tags enable editable areas with the page. No setup of configuration in the properties file is required.

Replace any text in the html template to make it editable within the page.

```
@text("heading")
```

Here's a real world example of using the code to make the a heading editable.

```html
<h1 class="text-lg text-gray-300 font-heading">@text("heading")</h1>
<p class="text-sm text-slate-300/70">Build the website of your dreams.</p>
```

You can also set a default value for an editable text areas, so that when your custom component is dropped into a page it will be populated with a defulat value. In the example below, it would be "Hello World!".

```
@text("heading", default: "Hello World!")
```

A dropzones is an area within an HTML template where existing component can be added.

```
@dropzone("extraItems")
```

Can also be written like this.

```
@dropzone(name: "content")
```

You can also add a title for the Dropzone, this will be shown in the Node Browser.

```
@dropzone("zone-1", title: "Zone 1")
```

### Adding Custom Properties (UI Controls)

Editable text and dropzones are just the start. Custom Components can also have their own **Properties** — the controls that appear in the Inspector, such as sliders, switches, and color or font pickers. The Component Editor has a **Properties** area alongside the **Template** area, and the configuration you add there uses the same format as an Element Pack's `properties.json`.

Add a control in the **Properties** area, give it an `id`, then reference that `id` in your **Template** with `{{id}}`. For example, a control that lets the user pick the text colour:

Place this in the **Properties:**

```json
{
    "groups": [{
        "title": "Settings",
        "properties": [{
            "title": "Text Color",
            "id": "textColor",
            "format": "text-{{value}}",
            "themeColor": {
                "default": { "name": "red", "brightness": 600 }
            }
        }]
    }]
}
```

And reference it in the **Template:**

```html
<p class="{{textColor}}">Hello World!</p>
```

{% hint style="info" %}
For the full list of available controls — text, slider, switch, select, and the theme-aware color, font, and spacing controls — see the [Properties reference](https://app.gitbook.com/s/oWVD0W05KiZtfQynqfZo/component/properties-json/general-structure). For a complete worked example that drives a snow effect from **Amount** and **Follow Mouse** controls, see [Add Snow to your Website](../../elements-app/how-to/add-snow-to-your-website.md).
{% endhint %}

### Going Further with the Elements API

Using the above tags inside of Custom Components only scratch the surface of what's possible, you can also use the [Elements API](https://docs.realmacsoftware.com/elements-docs/elements-language) inside of your Custom Components.

If you're a developer you can take things even further by creating distributable (and sellable) [Element Packs for RapidWeaver Elements](https://docs.realmacsoftware.com/elements-docs/elements-language/getting-started/getting-started).
