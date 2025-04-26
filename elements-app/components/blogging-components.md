---
description: The built in blogging components allow you to create a fully functional blog.
---

# Blog



| Blog Components | Description                                                     |
| --------------- | --------------------------------------------------------------- |
| Author          |                                                                 |
| Blog Tags       |                                                                 |
| Conditional     |                                                                 |
| Link to Post    |                                                                 |
| Post            | Wrapper, other blog components should be placed inside of this. |
| Post Body       |                                                                 |
| Post Date       |                                                                 |
| Post List       |                                                                 |
| Post Summary    |                                                                 |
| Post Title      |                                                                 |

### File and Folder Setup

The built-in Blog system in Element requires a specifit file and folder setup to work.

### Posts

Posts should be stored as Markdown down files inside a dedicated folder.

* Blog
  * posts
    * 2025-04-18-my-first=post.md
    * 2025-04-19-another-blog-post.md

The structure for the Posts Markdown file:

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

You can create additional metadata about Authors by organizing a folder structure with supplementary markdown files. The authors folder should be placed at the same level as your "posts" folder.

* Blog
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

### Advanced

A `$post` array containing the post's information is available to any component placed inside a Blog List or Blog Post component.

<table><thead><tr><th width="165">Name</th><th width="131">Type</th><th>Example</th></tr></thead><tbody><tr><td>author</td><td>array</td><td><code>&#x3C;?=$post['author']?></code></td></tr><tr><td>author.avatar</td><td>string | null</td><td><code>&#x3C;?=$post['author']['avatar']?></code></td></tr><tr><td>author.bio</td><td>string | null</td><td><code>&#x3C;?=$post['author']['bio']?></code></td></tr><tr><td>author.name</td><td>string</td><td><code>&#x3C;?=$post['author']['name']?></code></td></tr><tr><td>author.slug</td><td>string</td><td><code>&#x3C;?=$post['author']['slug']?></code></td></tr><tr><td>body</td><td>string</td><td><code>&#x3C;?=$post['body']?></code></td></tr><tr><td>date_published</td><td>string</td><td><code>&#x3C;?=$post['date_published']?></code></td></tr><tr><td>featured</td><td>boolean</td><td><code>&#x3C;?=$post['featured']?></code></td></tr><tr><td>feature_image</td><td>string</td><td><code>&#x3C;?=$post['feature_image']?></code></td></tr><tr><td>slug</td><td>string</td><td><code>&#x3C;?=$post['slug']?></code></td></tr><tr><td>status</td><td>string</td><td><code>&#x3C;?=$post['status']?></code></td></tr><tr><td>tags</td><td>array</td><td><code>&#x3C;?=$post['tags']?></code></td></tr><tr><td>title</td><td>string</td><td><code>&#x3C;?=$post['title']?></code></td></tr></tbody></table>

