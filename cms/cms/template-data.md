---
description: >-
  This guide explains how to create and use your CMS content withing Elements
  using Twig, a powerful and user-friendly template language.
icon: brackets-curly
---

# Template Data

The Elements CMS gives you full control over how your content is displayed by supporting the [Twig](https://twig.symfony.com/) templating language; a fast, secure, and flexible engine widely used in modern content systems.

[Twig](twig.md) is a template engine that lets you create dynamic, reusable templates for your website content. Think of it as a way to create a "skeleton" for your content that automatically fills in the details from your CMS items.

### Using CMS Data in Elements Components

You can access your CMS data in any Elements component, as long as that component is placed inside a Collection or Item component. This allows you to create dynamic, data-driven layouts without writing custom templates.

<figure><img src="../../.gitbook/assets/CleanShot 2025-08-06 at 21.10.54.gif" alt=""><figcaption></figcaption></figure>

### Accessing Your Content Data

#### Basic Properties

You can access any property from your content files using the `{{item.PROPERTY_NAME}}` syntax, for example:

* `{{item.title}}` - The title of your content
* `{{item.body}}` - The main content/body text
* `{{item.date}}` - The publication date
* `{{item.tags}}` - Any tags you've assigned
* `{{item.excerpt}}` - A short summary or excerpt

#### Custom Properties

If you've added custom properties in your content's frontmatter (the section at the top of your markdown files), you can access them the same way:

```yaml
---
title: My Blog Post
author: John Doe
category: Technology
featured: true
custom_field: Some value
---
```

In your template, you can use:

* `{{item.category}}`
* `{{item.featured}}`
* `{{item.custom_field}}`&#x20;

#### Collection Properties

You can access `{{collection.rssURL}}` inside the Collection component, which means you can add a Text component to the "Before" or "After" dropzones and link text/svg/anything to the RSS feed for that collection.

#### Nested Properties

Some properties — like an image — contain multiple pieces of information. You can access these using dot notation:

* `{{item.image.src}}` - Image URL or path
* `{{item.image.alt}}` - Image alt text
* `{{item.image.title}}` - Image title (optional)
* `{{item.image.width}}` and `{{item.image.height}}` - Image dimensions (optional)

See [Frontmatter](markdown/frontmatter.md) for the full list of nested keys an image object supports, and how to define arrays of images for galleries.

### Related Data Properties

The system can automatically connect related data between different content folders. This is especially useful for tags and authors.

**How It Works**

If you have a folder structure like this:

```
content/
├── posts/
│   ├── my-first-post.md
│   ├── my-second-post.md
│   └── my-third-post.md
├── tags/
│   ├── technology.md
│   ├── design.md
│   └── business.md
└── authors/
    ├── john-doe.md
    ├── jane-smith.md
    └── bob-wilson.md
```

When a post references tags or an author, the system automatically connects to the corresponding tag and author files.

**Example Content Structure**

**Post file (`posts/my-first-post.md`):**

```yaml
---
title: My First Blog Post
author: john-doe
tags: [technology, design]
date: 2024-01-15
---
```

**Author file (`authors/john-doe.md`):**

```yaml
---
name: John Doe
email: john@example.com
bio: A passionate web developer with 10 years of experience
avatar: images/john-doe.jpg
website: https://johndoe.com
---
```

**Tag file (`tags/technology.md`):**

```yaml
---
name: Technology
description: Posts about web development, programming, and tech trends
---
```

**Accessing Related Data**

Once the relationships are established, you can access the full data from the related files:

**Author Data:**

* `{{item.author.name}}` - Full name from author file
* `{{item.author.email}}` - Email from author file
* `{{item.author.bio}}` - Biography from author file
* `{{item.author.avatar}}` - Profile picture from author file
* `{{item.author.website}}` - Website from author file

**Tag Data:**

* `{{item.tags[0].name}}` - First tag's full name
* `{{item.tags[0].description}}` - First tag's description

**Displaying Author Information:**

```html
@raw()
    {% if item.author %}
        <div class="author-info">
            {% if item.author.avatar %}
                <img
                    src="{{item.author.avatar}}"
                    alt="{{item.author.name}}"
                    class="author-avatar"
                />
            {% endif %}
            <div class="author-details">
                <h3>By {{item.author.name}}</h3>
                {% if item.author.bio %}
                    <p>{{item.author.bio}}</p>
                {% endif %}
                {% if item.author.website %}
                    <a href="{{item.author.website}}" target="_blank">Visit Website</a>
                {% endif %}
            </div>
        </div>
    {% endif %}
@endraw
```

**Displaying Tags with Full Data:**

```html
@raw()
    {% if item.tags %}
        <div class="tags">
            {% for tag in item.tags %}
                <span class="tag">
                    {{tag.name}}
                    {% if tag.description %}
                        <span class="tag-description">{{tag.description}}</span>
                    {% endif %}
                </span>
            {% endfor %}
        </div>
    {% endif %}
@endraw
```

**Note:** if you're using twig syntax directly in an Elements component template, you'll need to wrap the code in an `@raw()` directive.

### Working with URLs

#### Item URLs

Each piece of content automatically gets a URL. You can access it using:

* `{{item.url}}` - The full URL to this content item
* `{{item.slug}}` - The URL-friendly version of the title

#### Pretty URLs

Elements CMS system supports "pretty URLs" which are more readable and SEO-friendly. Instead of URLs like:

```
yoursite.com/blog/post?id=123
```

You get clean URLs like:

```
yoursite.com/blog/my-awesome-blog-post
```

The system automatically generates these pretty URLs based on your component settings, and requires an htaccess file. Read more about [setting up Pretty URLs](pretty-urls.md).

### Conditional Content

You can show or hide content based on certain conditions:

```html
@raw()
    {% if item.featured %}
        <div class="featured-badge">Featured Post</div>
    {% endif %}
    
    {% if item.image %}
        <img src="{{item.image}}" alt="{{item.title}}" />
    {% endif %}
    
    {% if item.tags %}
        <div class="tags">
            {% for tag in item.tags %}
                <span class="tag">{{tag}}</span>
            {% endfor %}
        </div>
    {% endif %}
@endraw
```

### Looping Through Lists

If you have multiple items (like tags, categories, or related content), you can loop through them:

```html
@raw()
    {% if item.tags %}
        <div class="tags">
            {% for tag in item.tags %}
                <a href="/tags/{{tag}}" class="tag">{{tag}}</a>
            {% endfor %}
        </div>
    {% endif %}
@endraw
```

### Formatting Dates

You can format dates in various ways:

```html
<!-- Full date -->
<p>Published on {{item.date|date('F j, Y')}}</p>

<!-- Short date -->
<p>{{item.date|date('M j, Y')}}</p>

<!-- Just the year -->
<p>{{item.date|date('Y')}}</p>
```

### Common Template Patterns

#### Blog Post Template

```html
<article class="blog-post">
    <header>
        <h1>{{item.title}}</h1>
        <div class="meta">
            <span class="author">By {{item.author}}</span>
            <span class="date">{{item.date|date('F j, Y')}}</span>
        </div>
    </header>

    {% if item.image %}
    <img src="{{item.image}}" alt="{{item.title}}" class="featured-image" />
    {% endif %}

    <div class="content">{{item.body}}</div>

    {% if item.tags %}
    <footer>
        <div class="tags">
            {% for tag in item.tags %}
            <a href="/tags/{{tag}}" class="tag">{{tag}}</a>
            {% endfor %}
        </div>
    </footer>
    {% endif %}
</article>
```

#### Product Template

```html
<div class="product">
    <h1>{{item.title}}</h1>

    {% if item.image %}
    <img src="{{item.image}}" alt="{{item.title}}" />
    {% endif %}

    <div class="price">${{item.price}}</div>

    <div class="description">{{item.body}}</div>

    {% if item.features %}
    <ul class="features">
        {% for feature in item.features %}
        <li>{{feature}}</li>
        {% endfor %}
    </ul>
    {% endif %}
</div>
```

### Tips and Best Practices

1. **Always check if properties exist** before using them to avoid errors
2. **Use meaningful property names** in your content frontmatter
3. **Keep templates simple** - focus on structure and let the content drive the design
4. **Test your templates** with different types of content to ensure they work properly
5. **Use consistent naming** for your properties across all your content

### Common Properties Reference

Here's a quick reference of commonly available properties:

| Property        | Description        | Example                          |
| --------------- | ------------------ | -------------------------------- |
| `item.title`    | Content title      | "My Blog Post"                   |
| `item.body`     | Main content       | HTML content                     |
| `item.date`     | Publication date   | 2024-01-15                       |
| `item.author`   | Author name        | "John Doe"                       |
| `item.slug`     | URL-friendly title | "my-blog-post"                   |
| `item.url`      | Full URL           | "/blog/my-blog-post"             |
| `item.image`    | Featured image     | "/images/post.jpg"               |
| `item.excerpt`  | Short summary      | "This is a brief description..." |
| `item.tags`     | Content tags       | \["technology", "web-design"]    |
| `item.category` | Content category   | "Technology"                     |

Remember, you can always add custom properties to your content's frontmatter and access them using the same `{{item.property_name}}` syntax!
