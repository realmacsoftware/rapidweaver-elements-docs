---
description: The built in blogging components allow you to create a fully functional blog.
hidden: true
---

# Blogging Components

A `$post` array containing the post's information is available to any component placed inside a Blog List or Blog Post component.

<table><thead><tr><th width="165">Name</th><th width="131">Type</th><th>Example</th></tr></thead><tbody><tr><td>title</td><td>string</td><td><code>&#x3C;?=$post['title']?></code></td></tr><tr><td>published_date</td><td>string</td><td><code>&#x3C;?=$post['published_date']?></code></td></tr><tr><td>tags</td><td>array</td><td><code>&#x3C;?=$post['tags']?></code></td></tr><tr><td>featured</td><td>boolean</td><td><code>&#x3C;?=$post['featured']?></code></td></tr><tr><td>status</td><td>string</td><td><code>&#x3C;?=$post['status']?></code></td></tr><tr><td>feature_image</td><td>string</td><td><code>&#x3C;?=$post['feature_image']?></code></td></tr><tr><td>author</td><td>string | array</td><td><code>&#x3C;?=$post['author']?></code></td></tr></tbody></table>
