# Template Data

The Elements CMS gives you full control over how your content is displayed by supporting the [Twig](https://twig.symfony.com/) templating language — a fast, secure, and flexible engine widely used in modern content systems.

With Twig, you can dynamically output content, apply filters, and build custom logic directly into your website.

### Item Data

Inside of a Collection, Collection Item, and Static Item component you have access to the following data.

|               |                          |   |
| ------------- | ------------------------ | - |
| title         | \{{item.title\}}         |   |
| date          | \{{item.date\}}          |   |
| url           | \{{item.url\}}           |   |
| slug          | \{{item.slug\}}          |   |
| datePublished | \{{item.datePublished\}} |   |
| dateModified  | \{{item.dateModified\}}  |   |
| body          | \{{item.body\}}          |   |
| raw body      | \{{item.bodyRaw\}}       |   |
| status        | \{{item.status\}}        |   |
| featured      | \{{item.featured\}}      |   |
| image         | \{{item.image\}}         |   |
| excerpt       | \{{item.excerpt\}}       |   |

### Collection Pagination

|              |                              |   |
| ------------ | ---------------------------- | - |
| Current Page | \{{pagination.currentPage\}} |   |
| Per Page     | \{{pagination.perPage\}}     |   |
| Total Items  | \{{pagination.totalItems\}}  |   |
| Last Page    | \{{pagination.lastPage\}}    |   |

This object, combined with Twig, will allow you to build custom pagination to suite your project's needs.

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
