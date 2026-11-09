---
description: Define structured metadata at the top of your Markdown files.
---

# Frontmatter

The Elements CMS uses [YAML frontmatter](https://yaml.org/) to attach structured metadata to each piece of content. Frontmatter sits at the very top of a Markdown file, enclosed by triple dashes, and lets you define titles, dates, authors, tags, images, and any other custom fields your design needs.

Here's a complete example file with frontmatter and body:

{% code title="sample.md" %}
```markdown
---
title: Elements CMS Example
date: 2025-08-07
author: Jonny Appleseed
tags: [introduction, getting-started]
---

## Example introduction

Elements CMS lets you manage content using *simple Markdown* files with frontmatter.
You can write normal Markdown below the frontmatter, and **Elements** will handle the rest.
```
{% endcode %}

The block between the `---` lines is the frontmatter. Everything below it is the body content. Both are accessible in your templates — frontmatter via `{{item.<key>}}` references, the body via `{{item.body}}`.

### Date format

The `date` key uses ISO format: `year-month-day`.

```yaml
date: 2025-08-07
```

Time is also respected for date filtering, so you can write `2025-08-21 17:00`. The time is currently interpreted as UTC; customising the timezone is not supported.

The CMS sorts and filters Collections by date, so getting this right matters — see the [Collection](../components/collection.md) **Filters** group for the date-based filters that depend on this value.

### When you need quotes

YAML usually doesn't require quotes around strings, but some characters force the issue. The safest rule of thumb: if you're unsure, quote it — quoting a simple string never breaks anything.

#### No quotes needed

For simple text values:

```yaml
title: My Blog Post
date: 2025-08-06
author: Julia
```

#### Quotes required

When the value contains special YAML characters like `:`, `@`, `#`, or `{}`:

```yaml
title: "My Favorite Tools: Tailwind, Alpine, and Elements"
```

When the value starts with a number that might be misread (like a version):

```yaml
version: "1.0"
```

When the value looks like a boolean, `null`, or includes time-style colons:

```yaml
status: "false"
time: "14:30"
```

When the value contains line breaks (rare, but possible in multiline strings).

### Default values for missing keys

If a key is missing from a file's frontmatter, the corresponding `{{item.<key>}}` reference outputs nothing. To provide a fallback, use the Twig `default` filter:

```twig
{{item.subtitle|default("No subtitle")}}
```

See [Twig](../twig.md) for the full filter reference.

### Common keys and their behaviour

The CMS recognises a handful of frontmatter keys with built-in behaviour. You can use any other keys you like — they'll all be available via `{{item.<key>}}` — but these have special handling.

* `title` — used as the item's title across listings and the default page title.
* `date` — used for sorting and date-based filters; ISO format (see above).
* `author` — used for the author filter and for related-data lookups against an `authors/` folder.
* `tags` — array; used for the tag filter, [Tag List](../components/tag-list.md), and related-data lookups against a `tags/` folder.
* `status` — `published` (default) or `draft`. Drafts are hidden from Collections by default.
* `featured` — boolean; toggled by the **Featured** filter on a Collection.
* `image` — nested object; see [Image frontmatter](#image-frontmatter) below.
* `excerpt` — short summary, useful for search results and meta descriptions.

Custom keys (`category`, `price`, `rating`, anything you invent) are passed through verbatim. There's no schema you need to declare — the CMS adapts to whatever you write.

### Image frontmatter

You can define images in your frontmatter using nested keys. This stores multiple pieces of information about each image rather than just a path:

```markdown
---
title: Welcome to the Elements CMS
date: 2025-08-07
image:
  src: welcome.jpg
  alt: Abstract illustration of a CMS interface
---
```

The following keys are supported inside an image object:

* `src` — the path or URL to the image. Required.
* `alt` — a short text description, used for accessibility. Strongly recommended.
* `title` — the image title, often used for tooltips.
* `width` — image width in pixels.
* `height` — image height in pixels.

`src` can point to a local file in your project's resources folder or to a remote image hosted online.

You're not limited to the key name `image`. Anything you like will work the same way — `banner`, `thumbnail`, `photo`, `cover`:

```markdown
---
title: Welcome to the Elements CMS
date: 2025-08-07
banner:
  src: blog/interface.jpg
  title: CMS interface
  alt: Abstract illustration of a CMS interface
---
```

To reference these in a template:

```html
@raw()
<img src="{{item.image.src}}" alt="{{item.image.alt}}">
@endraw
```

### Arrays of images

For galleries or sliders, define an array of image objects. Each entry can use the same nested structure.

Local images:

```markdown
gallery:
  - src: "images/project1.jpg"
    alt: "Exterior view of the finished building"
  - src: "images/project2.jpg"
    alt: "Interior design showcasing the main lobby"
  - src: "images/project3.jpg"
    alt: "Construction phase with scaffolding"
```

Remote images:

```markdown
gallery:
  - src: "https://images.unsplash.com/photo-1626692987335-15dfc7a6f4b2"
    title: "Chichen Itza: Ancient Precision - View 1"
    alt: "Chichen Itza image 1"
  - src: "https://images.unsplash.com/photo-1544214889-03dfb1348b48"
    title: "Chichen Itza: Ancient Precision - View 2"
    alt: "Chichen Itza image 2"
```

To loop through them in a template:

```html
@raw()
<ul class="flex gap-2">
{% for image in item.gallery %}
    <li><img src="{{ image.src }}" alt="{{ image.alt }}" class="w-20 h-auto aspect-[1]">
{% else %}
    <li>No images.
{% endfor %}
</ul>
@endraw
```

### Common pitfalls

**My frontmatter isn't being parsed at all.**\
Check that the block is delimited by `---` on its own line, both above and below. A trailing space, a missing dash, or non-ASCII characters in the delimiter will all silently break parsing.

**A value is being interpreted as a boolean or null.**\
Strings like `yes`, `no`, `true`, `false`, `null`, and `~` are reserved YAML literals. Wrap them in quotes if you mean them as text.

**Indentation looks wrong even though it looks right.**\
YAML requires _spaces_, not tabs. Most editors insert tabs by default — configure your editor to use 2 spaces for `.md` files, or copy the indentation from a known-good file.

**A date filter is showing 1970 dates.**\
The `date` value is missing or in an unparseable format. Use ISO format (`2025-08-07`) and consider quoting it if your value includes a time component.
