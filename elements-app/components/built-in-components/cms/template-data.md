# Template Data

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

