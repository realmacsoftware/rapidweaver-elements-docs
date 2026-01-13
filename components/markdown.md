# Markdown

The Markdown component lets you write content using standard Markdown syntax and render it directly inside your Elements layout. It’s ideal for longer blocks of text, technical documentation, blog-style content, or anywhere you want fast, readable formatting without manually styling individual text elements.

Markdown is widely used, easy to read, and quick to write. If you’re already familiar with it, you’ll feel right at home.

#### Adding a Markdown Component

To add a Markdown component to your page:

1. Open the **Components** panel
2. Drag **Markdown** onto your page
3. **Right-click** on the Markdown Component in the page and choose the "Edit Markdown" option.

The content is rendered live as you type, so you can immediately see how your Markdown will appear on the page.

#### Supported Markdown Syntax

The Markdown component supports standard, [official Markdown syntax](https://daringfireball.net/projects/markdown/syntax), including:

**Headings**

```
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6
```

**Paragraphs and Line Breaks**

```
This is a paragraph.

This is another paragraph.
```

**Emphasis**

```
*Italic text*
**Bold text**
***Bold and italic***
```

**Unordered lists:**

```
- Item one
- Item two
- Item three
```

**Ordered lists:**

```
1. First item
2. Second item
3. Third item
```

**Links**

```
[Visit Realmac Software](https://realmacsoftware.com)
```

**Images**

```
![Alt text](/photos/image-name.jpg)
```

Images should reference files already added to your Elements project.

**Blockquotes**

```
> This is a blockquote
```

**Inline code:**

```
`inline code`
```

#### Styling and Appearance

Markdown content inherits its styling from your project’s **Typography** **Settings** in the **Theme Studio**. This keeps your Markdown visually consistent with the rest of your site without needing extra configuration. If you want more granular visual control, consider using the **Text** component instead.

#### When to Use Markdown&#x20;

The Markdown component is a great choice when:&#x20;

* Writing documentation or help pages
* Creating blog-style or editorial content
* Displaying formatted text quickly
* Working with content written outside of Elements&#x20;

For highly visual layouts or fine-grained typographic control, standard Elements components may be a better fit.&#x20;

#### Notes and Limitations

* Markdown is rendered as static content
* Interactive Elements components cannot be embedded inside Markdown
* Styling is controlled globally rather than per element Markdown keeps things simple, readable, and fast.
