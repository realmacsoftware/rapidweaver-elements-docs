---
icon: file
description: Outline basic information about your Element
---

# info.json

The info.json file contains important information about a Component. The file uses the JSON format and consists of a series of key and value pairs. It's required for Component to function.

### Component Categories

Every Component needs to define a category in which they belong. This tells Elements how to group components in the UI and helps users to locate components. Your Component MUST use one of the following pre-defined categories.&#x20;

If you think we're missing a category, please visit the [forum and let us know](https://forums.realmacsoftware.com/c/rapidweaver-elements/developer/).

| Group             | example                                                       |
| ----------------- | ------------------------------------------------------------- |
| **Content**       | Headings, Paragraphs, Lists.                                  |
| **Layout**        | Grid, Flex, Containers, Columns.                              |
| **Navigation**    | Menus, Nav Bars, Breadcrumbs, Tabs.                           |
| **Forms**         | Text Fields, Text Areas, Checkboxes, Buttons.                 |
| **SEO**           | Keywords, SEO helpers.                                        |
| **Media**         | Images, Video, Audio Players, Icons, Embeds (YouTube, Vimeo). |
| **Ecommerce**     | Cart Integration, Product display, Add to Cart Buttons.       |
| **Accessibility** | ARIA Lables, Contrast Checkers.                               |
| **Animation**     | Hover Effects, Animated SVG's.                                |
| **Dynamic**       | CMS Components, Google Sheets                                 |
| **Utilities**     | Cookies, Anchors, Placeholders, Dividers.                     |
| **Interactive**   | Modals, Popovers, Accordions, Carousels.                      |
| **Security**      | Password Protection, Login Forms.                             |



### Supported Key-Value Pairs <a href="#key-value-pairs-explained" id="key-value-pairs-explained"></a>

The Elements info.json file supports the following key-value pairs.

<table><thead><tr><th>Key</th><th width="100">Type</th><th>Notes</th></tr></thead><tbody><tr><td><code>identifier (Required)</code></td><td>string</td><td>The identifier is the unique ID for your Element. We recommend using a <a href="https://developer.apple.com/library/archive/documentation/FileManagement/Conceptual/understanding_utis/understand_utis_conc/understand_utis_conc.html">reverse DNS format</a>. This should be a string consisting of just lowercase characters and periods without spaces.</td></tr><tr><td><code>author (Required)</code></td><td>string</td><td>The name of the author of the Element. This would usually be the developer name, or the name of the company publishing the Element.</td></tr><tr><td><code>title (Required)</code></td><td>string</td><td>The name of the Element. This will be displayed inside of RapidWeaver. A unique and descriptive name is preferable. Overly long names will get truncated, check inside of the RapidWeaver UI for readability.</td></tr><tr><td><code>group (Required)</code></td><td>string</td><td>One of the above categories. Components with the same category are grouped together.</td></tr><tr><td><code>tags</code></td><td>array</td><td>A list of tags relevant to the Elements.</td></tr><tr><td><code>helpURL</code></td><td>string</td><td>A URL to the location of the help documentation online.</td></tr><tr><td><code>infoURL</code></td><td>string</td><td>A URL to the location of the marketing page online.</td></tr><tr><td><code>assets</code></td><td>array</td><td>A list of required assets for the Element. This can be a mixed list of images and files for example.</td></tr></tbody></table>

### info.json Example

You can use the following code as a starting point for your own info.json file.

```
{
  "identifier": "com.realmac.elementpack.helloworld",
  "author": "Realmac Software",
  "title": "Hello World",
  "group": "Utility",
  "tags": [
    "simple",
    "example"
  ],
  "assets": [
    {
      "filename": "assets/image-square.png"
    }
  ]
}
```

<figure><img src="../../../.gitbook/assets/CleanShot 2023-08-04 at 5.17.44@2x.png" alt=""><figcaption><p>Example info.json file inside of an Element.</p></figcaption></figure>
