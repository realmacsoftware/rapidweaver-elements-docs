---
description: Use the Twig templating language to format and transform CMS content.
icon: leaf
---

# Twig

Elements CMS supports the [Twig templating language](https://twig.symfony.com/) — a fast, secure, and flexible template engine widely used in modern PHP applications. Twig is what makes references like `{{item.title}}` work, and what powers everything from date formatting to control flow inside your CMS templates.

If you've ever written a template in Liquid, Jinja, or Handlebars, Twig will feel familiar. If not, the basics are quick to pick up — they're covered below.

### The four building blocks

Twig has four kinds of syntax you'll use over and over:

* `{{ … }}` — **output** a value. Anything between the double braces is evaluated and printed.
* `{% … %}` — a **statement** like an `if`, a `for` loop, or a variable assignment. Statements don't print anything by themselves.
* `{# … #}` — a **comment** that's stripped before output.
* `|filter` — a **filter** applied to a value. `{{item.title|upper}}` runs the title through the `upper` filter.

You can chain filters: `{{item.title|striptags|upper}}` strips HTML tags _then_ uppercases the result.

### Where Twig runs in Elements

Inside a Collection or Item drop zone, `{{item.title}}` and friends work natively in any Elements component — Headings, Typography, Text, Link, Image — without any extra setup. The component reads the reference and renders the value.

When you want to use Twig syntax that goes beyond a simple reference — control flow, filters, custom HTML — you have two options:

* In a custom HTML or Code component, wrap the Twig in an `@raw()` directive. Without `@raw()`, the surrounding template engine treats `{% %}` and `{{ }}` as its own syntax and may interfere.
* In a native Elements component's text field, simple references and filters work directly. Control flow doesn't.

```html
@raw()
{% if item.featured %}
    <span class="badge">Featured</span>
{% endif %}
@endraw
```

### Control flow

#### Conditionals

```html
@raw()
{% if item.featured %}
    <span class="badge">Featured</span>
{% endif %}

{% if item.tags %}
    Tagged: {{ item.tags|length }} tag(s)
{% else %}
    No tags
{% endif %}
@endraw
```

#### Loops

```html
@raw()
{% for tag in item.tags %}
    <a href="/tag/{{ tag }}">{{ tag }}</a>
{% else %}
    <em>No tags yet.</em>
{% endfor %}
@endraw
```

The `{% else %}` block inside a `{% for %}` runs when the collection is empty — handy for "no items" fallbacks.

Twig exposes a `loop` variable inside any loop with useful counters:

* `loop.index` — the current iteration, starting at 1.
* `loop.index0` — the same, starting at 0.
* `loop.first` and `loop.last` — booleans for the first and last iterations.
* `loop.length` — the total number of items.

```html
@raw()
{% for tag in item.tags %}
    {{ tag }}{% if not loop.last %}, {% endif %}
{% endfor %}
@endraw
```

### The most useful filters in CMS context

These come up constantly when working with Markdown content.

#### `date` — format a date

```html
{{ item.date|date('F j, Y') }}     {# January 15, 2024 #}
{{ item.date|date('M j, Y') }}     {# Jan 15, 2024     #}
{{ item.date|date('Y') }}          {# 2024             #}
{{ item.date|date('Y-m-d') }}      {# 2024-01-15       #}
```

The format string uses [PHP date tokens](https://www.php.net/manual/en/datetime.format.php). Twig also offers a [`date_modify` filter](https://twig.symfony.com/doc/3.x/filters/date_modify.html) for relative date math.

{% hint style="warning" %}
The Twig International Date Extension is installed, but it requires PHP's `intl` extension to be enabled on your server to function correctly. Check your PHP configuration if locale-aware date formatting fails.
{% endhint %}

#### `default` — fall back when a value is missing

```html
{{ item.author|default('Anonymous') }}
{{ item.subtitle|default('') }}
```

If `item.author` is missing or null, the filter substitutes the fallback. Without `|default`, missing properties output nothing.

#### `length` — count items in an array or characters in a string

```html
{{ item.tags|length }} tags
{{ item.body|length }} characters
```

#### `upper`, `lower`, `title`, `capitalize` — change case

```html
{{ item.title|upper }}        {# HELLO WORLD       #}
{{ item.title|lower }}        {# hello world       #}
{{ item.title|title }}        {# Hello World       #}
{{ item.title|capitalize }}   {# Hello world       #}
```

#### `striptags` — strip HTML

Useful when reusing the rendered body in a `<meta>` description or excerpt.

```html
{{ item.body|striptags }}
```

#### `slice` — take part of an array or string

```html
{{ item.body|slice(0, 200) }}                {# first 200 characters    #}
{{ item.tags|slice(0, 3) }}                  {# first 3 tags            #}
```

#### `split` and `join` — break apart and reassemble

```html
{{ "a, b, c"|split(', ') }}                  {# ['a', 'b', 'c']         #}
{{ item.tags|join(', ') }}                   {# 'design, web, ui'       #}
```

#### `escape` (alias `e`) — make a string safe for output

Twig auto-escapes most output, but if you've manually marked a value as `|raw` and need to re-escape part of it, `|escape` does the trick.

#### Chaining: a clean text excerpt

A common recipe — take the body, strip HTML, take the first 32 words, and add an ellipsis:

```html
{{ item.body|striptags|split(' ')|slice(0, 32)|join(' ') ~ ' ...' }}
```

The `~` operator concatenates strings, equivalent to `+` in JavaScript.

### Variable assignment

```html
@raw()
{% set wordCount = item.body|striptags|split(' ')|length %}
<p>About {{ wordCount }} words · {{ (wordCount / 200)|round }} min read.</p>
@endraw
```

`{% set %}` declares a variable that's only in scope for the rest of the template. Useful when you'd otherwise repeat a long expression.

### Working with arrays

```html
@raw()
{# First and last #}
First tag: {{ item.tags|first }}
Last tag: {{ item.tags|last }}

{# Membership #}
{% if 'design' in item.tags %}
    <span>Design article</span>
{% endif %}

{# Length #}
{{ item.tags|length }} tags
@endraw
```

### Common pitfalls

**My `{{ … }}` reference renders literally on the page.**\
You're inside a code or HTML component without `@raw()`. Wrap the block in `@raw() … @endraw` so the outer engine doesn't pre-process the Twig syntax.

**A property that exists in some posts but not others is breaking my template.**\
Use `|default` or wrap access in an `{% if %}`. Twig errors on undefined properties unless you guard against them.

**My HTML is being auto-escaped — `<` shows up as `&lt;`.**\
Twig auto-escapes string output by default. Use `|raw` to opt out of escaping for a specific value (only for content you trust):

```html
{{ item.body|raw }}
```

Be careful — anything user-supplied should stay escaped to prevent cross-site scripting.

**Date filters output `1970-01-01`.**\
Your frontmatter `date` value is missing or unparseable. See [Frontmatter](markdown/frontmatter.md) for the supported date formats.

### Useful resources

* [Twig documentation](https://twig.symfony.com/doc/3.x/)
* [Twig filter reference](https://twig.symfony.com/doc/3.x/filters/index.html)
* [Twig tag reference](https://twig.symfony.com/doc/3.x/tags/index.html) (for `{% if %}`, `{% for %}`, `{% set %}`, etc.)
* [Twig playground](https://twig.symfony.com/play) — paste templates and test them interactively.
* [PHP date format reference](https://www.php.net/manual/en/datetime.format.php) — every token you can use with the `date` filter.
