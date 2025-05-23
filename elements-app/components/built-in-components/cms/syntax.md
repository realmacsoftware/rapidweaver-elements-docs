# Syntax

The Elements CMS gives you full control over how your content is displayed by supporting the [Twig](https://twig.symfony.com/) templating language — a fast, secure, and flexible engine widely used in modern content systems.

With Twig, you can dynamically output content, apply filters, and build custom logic directly into your website.

### Item Syntax

* item.title
* item.featured
* item.excerpt
* item.datepublished

### Pagination Syntax

* currentPage
* totalPages
* totalItems
* itemsPerPage
* hasPreviousPage
* hasNextPage
* previousPageUrl
* nextPageUrl

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



### Useful Resources

* [Twig Docs](https://twig.symfony.com/doc/3.x/)
* [Twig Filters](https://twig.symfony.com/doc/3.x/filters/index.html)
* [Twig Playground](https://twig.symfony.com/play)
* [PHP Date Functions](https://www.php.net/manual/en/function.date.php)

