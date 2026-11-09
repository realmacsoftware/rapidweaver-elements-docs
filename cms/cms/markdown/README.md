---
description: Structure your content using Markdown and Frontmatter
icon: hashtag
---

# Markdown

[Markdown](https://www.markdownguide.org/) is a lightweight markup language that lets you format text using plain characters, no clunky toolbars or complex syntax. It’s perfect for writing clean, readable content that works beautifully inside the Elements CMS.

Elements CMS supports all [Basic Markdown Syntax](https://www.markdownguide.org/cheat-sheet/),  it does not currently support the unofficial extended syntax.

* \# creates a heading. More # symbols = smaller headings.
  * \# heading 1
  * \## heading 2
  * \### heading 3
  * \#### heading 4
* \*\*bold\*\* and \_italic\_ give your text emphasis.
* \- or \* can be used to create bullet lists.
* \`code\` adds inline code styling.
* Links look like this: \[text]\(https://example.com)
* Images are similar: !\[alt text]\(image.jpg)

Markdown files in Elements are stored as plain .md text files, making them easy to version control, edit, and preview.

If you’re familiar with writing in a notes app or using a basic text editor, you’ll feel right at home.

{% code title="welcome-post.md" %}
```markdown
# Welcome to the Elements CMS
Elements CMS lets you manage content using simple Markdown files with frontmatter. It’s fast, flexible, and built to fit seamlessly into your Elements projects.

This is a sample post to show you how content is structured. You can write normal Markdown below the frontmatter, and Elements will handle the rest.

## What You Can Do
- Add headings, lists, images, and links
- Include metadata in the frontmatter
- Preview your content instantly
- Keep everything version-controlled with Git

> Markdown gives you the structure. Elements gives you the style.

Ready to get started? Save this file and start editing!
```
{% endcode %}

### Adding Frontmatter

The Elements CMS uses [YAML Frontmatter](frontmatter.md) to define metadata and editable fields for your Markdown content. This is a block of structured data placed at the top of a Markdown file, enclosed by triple dashes.

Frontmatter is how you tell Elements what kind of content is in the file, like titles, images, links, or anything else you want to edit via the CMS. It lets you create custom data models for different types of pages (blog posts, staff bios, projects, etc).

You’re in full control of the structure, the CMS will (eventually) automatically generate fields based on the frontmatter keys you define.

Everything below the frontmatter is treated as the main body content and can also be edited in Markdown.

{% code title="welcome-post.md" %}
```markdown
---
title: Welcome to the Elements CMS
date: 2025-08-07
author: Jonny Appleseed
tags: [introduction, getting-started]
summary: A quick overview of how to get started with the Elements CMS.
image:
  src: welcome.jpg
  alt: Abstract illustration of a CMS interface
---

# Welcome to the Elements CMS
Elements CMS lets you manage content using simple Markdown files with frontmatter. It’s fast, flexible, and built to fit seamlessly into your Elements projects.

This is a sample post to show you how content is structured. You can write normal Markdown below the frontmatter, and Elements will handle the rest.

## What You Can Do
- Add headings, lists, images, and links
- Include metadata in the frontmatter
- Preview your content instantly
- Keep everything version-controlled with Git

> Markdown gives you the structure. Elements gives you the style.

Ready to get started? Save this file and start editing!
```
{% endcode %}

You can [learn more about defining Frontmatter here](frontmatter.md)

### Websafe Image and Resource Naming

Always ensure you reference images with a lowercase name and file path.

Instead of `Images/My-Image.jpg` use all loweracse, like this: `images/my-image.jpg`.

When Publishing, Elements will lowercase all resource filenames and ensure they are websafe by swapping out foreign characters and spaces with an underscore. For example:

* `my~file.png` would become `my_file.png`.
* `my file has spaces.png` would become `my_file_has_spaces.png`.
* `myFile.png` would become `myfile.png`.

Many web servers (Linux/Unix based) treat File.jpg and file.jpg as two different files. However, on Windows or macOS (i.e. Elements), the filesystem often isn’t case-sensitive, so it _looks_ fine locally, but when uploaded, it can cause broken links and 404 errors.

By using lowercase files, you’ll ensure they will ALWAYS work on different environments (Windows, Linux, macOS), this could be very important depending on the hosting platform you have chosen.
