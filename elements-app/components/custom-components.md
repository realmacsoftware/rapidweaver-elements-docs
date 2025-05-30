---
description: Extend RapidWeaver by creating your very own custom Components
---

# Custom Components

If you know a bit of HTML you can create your own custom Components for use in your projects. These can be anything from a simple html snippet to a fully blown Component with custom UI controls. **The possibilities of what you can create are endless!**

### A few things to note before you get started:

1. No external code editor is required, you can build everything inside of RapidWeaver  Elements.
2. Custom Components are stored in the project they were created in.
3. Custom Components have full access to the [Elements Language](../../elements-language/api-introduction/) (although they cannot include extra files like third-party component can).
4. To ensure compatibility with Elements you should use Tailwind CSS classes when writting your Template HTML.
5. Custom Components can easily be converted into an encrpyted third-party component that can be [distributed and sold via the Elements platform](../../elements-store/distribution.md).

### Creating a Custom Component

Creating a Custom Component in Elements is the easiest and fastest way to get started with exploring the Elements API. Custom Components can eaily be migrated to distributable [Element Packs](../../elements-language/api-introduction/getting-started.md) at a later date.

{% stepper %}
{% step %}
### Open the Components area in the sidebar of your project

Press the "+" button next to the "Custom" heading, and choose HTML. You should now see the component appear in the list.

<img src="../../.gitbook/assets/CleanShot 2024-11-29 at 4 .20.54@2x.png" alt="" data-size="original">
{% endstep %}

{% step %}
### Drag your newly created component onto the Page

Drag your HTML component into the page, you're now ready to start customizing it.

<img src="../../.gitbook/assets/CleanShot 2024-11-29 at 4 .23.42@2x.png" alt="" data-size="original">
{% endstep %}

{% step %}
### Edit your Custom Component

Next, open the Component Editor so we can view and edit the code. All changes made to the code update in realtime. Go ahead, change the text and watch the preview update.

<img src="../../.gitbook/assets/CleanShot 2024-11-29 at 4 .26.20@2x (1).png" alt="" data-size="original">
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

### Going Further with the Elements API

Using the above tags inside of Custom Components only scratch the surface of what's possible, you can also use the [Elements API](../../elements-language/api-introduction/) inside of your Custom Components.

If you're a developer you can take things even further by creating distributable (and sellable) Element Packs for RapidWeaver Elements. You can learn more about Element Packs in the [Elements Pack section](../../elements-language/api-introduction/getting-started.md) of this manual.

### Dev Diary Videos for Custom Elements

The following videos will show you how to create Custom Elements. The following videos were recorded with a development version of Elements so the feature(s) available now may differ slightly to those in the video. View the [Tutorial playlist on YouTube](https://www.youtube.com/playlist?list=PLlqV01jBZsjAODafdmCOpU7dYxqiB6y02) for more videos.

{% embed url="https://www.youtube.com/watch?v=FeNoKUzd_fg" %}

{% embed url="https://youtu.be/COzwMMJDr5U?si=7ey-mtI0eJvh7BjQ" %}

{% embed url="https://www.youtube.com/watch?v=ekiHAQDWsMg" %}

{% embed url="https://www.youtube.com/watch?v=c3hejkIlloQ&list=PLlqV01jBZsjAODafdmCOpU7dYxqiB6y02&index=4&t=1106s&pp=gAQBiAQB" %}

{% embed url="https://www.youtube.com/watch?v=oYEIdQUKXTY&list=PLlqV01jBZsjAODafdmCOpU7dYxqiB6y02&index=2&pp=gAQBiAQB" %}

{% embed url="https://www.youtube.com/watch?v=kbIQjRuteY4&list=PLlqV01jBZsjAODafdmCOpU7dYxqiB6y02&index=1&pp=gAQBiAQB" %}
