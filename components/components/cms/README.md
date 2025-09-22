---
description: Markdown based Content Management System in Elements
hidden: true
---

# CMS

### Server Requirements

The CMS Components in Elements require PHP 8.x or newer. **You must ensure all CMS related pages use a .php extension.**

#### Wrapper Components

These components are used as wrappers, or container, components. You should place other components inside of these. Components placed inside these components will gain access to CMS data.

| CMS Component     | Description                                                                                                  |
| ----------------- | ------------------------------------------------------------------------------------------------------------ |
| Static Item       | Wrapper for fetching a single item from the CMS.                                                             |
| Collection        | Wrapper for fetching a collection (folder) og items.                                                         |
| Collection Item   | Used for Collection page templates. Will fetch the requested Collection Item based on the `slug` in the URL. |
| Collection Search | Adds instant search for any collection.                                                                      |

#### Child Components

These components should be placed inside the wrapper components. These components have access to CMS data, such as as the title, date, author, body, and so on.

| Component             | Description                                                                                            |
| --------------------- | ------------------------------------------------------------------------------------------------------ |
| Body                  | Used to access the body of an item.                                                                    |
| Item Author           | Display the author for the current item.                                                               |
| Item Tags             | Display tags for the current item.                                                                     |
| Related Items         | Display items related to the current item. **Must be placed inside a Static Item or Collection Item.** |
| Collection Pagination | Adds pagination links to any collection. **Must be placed inside a Collection.**                       |
| Conditional           | Conditionally display content.                                                                         |

### File and Folder Setup

The built-in CMS system in Element requires a specific file and folder setup to work. You must ensure all **blog related pages use a .php extension**.&#x20;

### Content

Content should be stored as Markdown down files inside a dedicated folder.

* cms
  * posts
    * 2025-04-18-my-first-post.md
    * 2025-04-19-another-blog-post.md

The structure for the Markdown file:

```
---
title: "An Example Post"
date_published: "2025-04-20"
author: Steve
tags: [technology]
status: published
feature_image: blog/myimage.jpg
featured: true
---
This is the contents of my first post.
```

### Authors

You can create additional metadata about Authors by organizing a folder structure with supplementary markdown files. In this example, the authors folder is placed at the same level as the "posts" folder.

* cms
  * posts
  * authors
    * steve.md
    * jasmin.md

The structure for the Authors Markdown file:

```
---
name: "Steve"
avatar: blog/steve-photo.png
---
This is all about Steve.
```

### RSS Feed

Any page with a CMS collection can provide an RSS feed. Simply append  `?format=rss` to the end of the URL, like this `yourwebsite.com/blog/?format=rss` .

### Advanced

A `$post` array containing the post's information is available to any component placed inside a Collection or Item component.

<table><thead><tr><th width="165">Name</th><th width="131">Type</th><th>Example</th></tr></thead><tbody><tr><td>author</td><td>array</td><td><code>&#x3C;?=$post['author']?></code></td></tr><tr><td>author.avatar</td><td>string | null</td><td><code>&#x3C;?=$post['author']['avatar']?></code></td></tr><tr><td>author.bio</td><td>string | null</td><td><code>&#x3C;?=$post['author']['bio']?></code></td></tr><tr><td>author.name</td><td>string</td><td><code>&#x3C;?=$post['author']['name']?></code></td></tr><tr><td>author.slug</td><td>string</td><td><code>&#x3C;?=$post['author']['slug']?></code></td></tr><tr><td>body</td><td>string</td><td><code>&#x3C;?=$post['body']?></code></td></tr><tr><td>date_published</td><td>string</td><td><code>&#x3C;?=$post['date_published']?></code></td></tr><tr><td>featured</td><td>boolean</td><td><code>&#x3C;?=$post['featured']?></code></td></tr><tr><td>feature_image</td><td>string</td><td><code>&#x3C;?=$post['feature_image']?></code></td></tr><tr><td>slug</td><td>string</td><td><code>&#x3C;?=$post['slug']?></code></td></tr><tr><td>status</td><td>string</td><td><code>&#x3C;?=$post['status']?></code></td></tr><tr><td>tags</td><td>array</td><td><code>&#x3C;?=$post['tags']?></code></td></tr><tr><td>title</td><td>string</td><td><code>&#x3C;?=$post['title']?></code></td></tr></tbody></table>

