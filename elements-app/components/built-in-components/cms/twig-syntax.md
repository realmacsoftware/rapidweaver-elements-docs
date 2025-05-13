# Twig Syntax

The Elements CMS gives you full control over how your content is displayed by supporting the [Twig](https://twig.symfony.com/) templating language — a fast, secure, and flexible engine widely used in modern content systems.

With Twig, you can dynamically output content, apply filters, and build custom logic directly into your website.

### Twig Filter Examples

For example, if you need to ensure your title is uppercased you could append a pipe and upper text to the item.title tag, like this:

```
{{item.title}} 
```

Outputs: Hello world!

```
{{item.title|upper}}
```

Outputs: HELLO WORLD!

### Useful Links

* [Twig Filters](https://twig.symfony.com/doc/3.x/filters/index.html)

