---
description: Adding styling for lists (ul and ol) in Elements CMS
---

# Styling Lists

If you’re using lists in your Markdown documents, it’s worth adding some styling. You can either apply Tailwind classes directly to your Typography component, or add a small block of custom CSS to your project template.

Here are some example Tailwind classes you can drop into the Typography CSS Classes field:

```php-template
[&_ul]:list-disc
[&_ul]:pl-4
[&_ul]:mt-3
[&_ul]:mb-3
[&_ul_li]:my-1
[&_ul_li]:marker:text-gray-500
```

<figure><img src="../../../.gitbook/assets/CleanShot 2025-11-24 at 9 .44.06@2x.png" alt=""><figcaption></figcaption></figure>

Or:

```ruby
[&_ul]:list-disc
[&_ul]:pl-5
[&_ul]:space-y-2
[&_ul_li]:leading-relaxed
[&_ul_li]:text-gray-800
```

For ordered lists:

```markdown
[&_ol]:list-decimal
[&_ol]:pl-5
[&_ol]:space-y-2
[&_ol_li]:my-1
```

And if you want tighter spacing:

```ruby
[&_ul]:list-disc [&_ul]:pl-4 [&_ul_li]:my-0.5
```

Alternatively you can add the following vanilla CSS to your project template’s `<head>` section, but we highly recommend using Tailwind.

{% code overflow="wrap" %}
```css

<style>
ul, ol {
  padding-left: 1.25rem;
  margin: 0.75rem 0;
}
ul {
  list-style: disc;
}
ol {
  list-style: decimal;
}
ul li,
ol li {
  margin: 0.25rem 0;
  line-height: 1.5;
  color: #333;
}
</style>
```
{% endcode %}

<figure><img src="../../../.gitbook/assets/CleanShot 2025-11-24 at 9 .47.29@2x.png" alt=""><figcaption></figcaption></figure>

### Styling links in lists

Tailwind’s arbitrary variants let you chain selectors togther, the following is an example of styling an ordered list containing links.

```css
[&_ol]:list-decimal
[&_ol]:pl-5
[&_ol]:space-y-2
[&_ol_li]:my-1
[&_ol_li_a]:text-blue-600
[&_ol_li_a]:underline
```

That \[&\_ol\_li\_a] selector is doing:

* \_ol → the ordered list
* \_li → list items inside it
* \_a → links inside the list items

If you want hover styles as well:

```css
[&_ol_li_a:hover]:text-blue-800
```

Or if you want something a bit more refined:

```css
[&_ol_li_a]:text-primary
[&_ol_li_a]:no-underline
[&_ol_li_a:hover]:underline
```
