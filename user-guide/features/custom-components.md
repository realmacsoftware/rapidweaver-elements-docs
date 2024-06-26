---
description: Extend RapidWeaver by creating your very own custom Components
---

# Custom Components

If you know a bit of HTML you can create your own custom Components for use in your projects. These can be anything from a simple html snippet to a fully blown Component with custom UI controls and local data stores. **The possibilities of what you can create are endless!**

#### A few things to note before you get started:

1. No extrenal code editor is required, you can build everything inside of RapidWeaver  Elements.
2. Custom Components are stored in the project they were created in.
3. Custom Components have full access to the Elements Language.
4. Custom Components can build and create local data stores.

### Adding Editable Content Areas

The following code should be placed in the HTML Template area. Using any of the following tags enable editable areas with the page. No setup of configuration in the properties file is required.

Replace any text in the html template that you want to make editable within the page.

```
@text("heading")
```

Here's a real world example of using the code to make the heading editible/

```html
<h1 class="text-lg text-gray-300 font-heading">@text("heading")</h1>
<p class="text-sm text-slate-300/70">Build the website of your dreams.</p>
```

You can also a default value to editable text areas, so that when your custom component is droped into a page it will be populated with a defulat value. In the example below, it would be "Hello World!".

```
@text("heading", default: "Hello World!")
```

A dropzones is an area within an HTML template where existing component can be added.

```
@dropzone("extraItems")
```

### Going Further

Custom Components inside of Elements only scratch the surface of what's possible. You can take things further by creating Element Packs outside of RapidWeaver Elements. You can learn more about Element Packs in the [Elements Pack section](../../element-packs/introduction/getting-started.md) of this manual.