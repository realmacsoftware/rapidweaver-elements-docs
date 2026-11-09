---
description: An overview of the Elements CMS components and how they fit together.
icon: object-ungroup
---

# Components

The Elements CMS ships with a small family of components that you combine to build content-driven pages. Each one has a clear job, and most are designed to work _inside_ another component, the same way a list item only makes sense inside a list.

This page is a tour of what's available and a quick guide to picking the right component for the job.

### The two components everything else builds on

Almost every CMS-powered page is built around one of these two components.

* [**Collection**](collection.md)\
  Displays a group of items pulled from a folder in your CMS, such as every post in `posts/` or every member in `team/`. Use a Collection anywhere you want to show a _list_ of content: a blog index, a portfolio grid, a team page, a product catalogue.
* [**Item**](item.md)\
  Displays a single piece of CMS content, typically the post, project, or profile that matches the slug in the page's URL. Use an Item anywhere you want a _detail_ view, like an individual blog post page.

A typical blog uses both: a Collection on `/blog/` to list posts, and an Item on `/blog/post/` to show one post at a time.

### Components that live inside a Collection

These only function when placed inside a Collection's drop zones. They control how the Collection's items are paged or revealed.

* [**Collection Pagination**](collection-pagination.md)\
  Numbered page links for navigating long Collections. Best when readers benefit from seeing how many pages there are or jumping around.
* [**Load More**](load-more.md)\
  A single button that fetches the next batch of items in place. Best for a smooth, app-like browsing experience.

{% hint style="warning" %}
**Pagination and Load More cannot be used together.** They both control how items are fetched, so enabling both at once will conflict. Pick one per Collection.
{% endhint %}

### Components that live inside an Item

These rely on the context of a single CMS item to work. Place them inside an Item component or one of its drop zones.

* [**Related Items**](related-items.md)\
  Surfaces other items that share tags or an author with the current one. Ideal for a "You might also like" section under a blog post.
* [**Comments**](comments.md)\
  Adds a moderated comments thread to the current item, with a built-in submission form and server-side storage.

### Discovery and navigation

* [**Search**](search.md)\
  Adds an instant, client-side search box that filters CMS content as the visitor types. Results are rendered using a template you design.
* [**Tag List**](tag-list.md)\
  Renders every tag used in a Collection as a list of links, with optional post counts. The building block for a "Browse by topic" sidebar.

### Online editing

* [**Online Editor**](online-editor.md)\
  Mounts the browser-based admin app on a page of your site. Place it on a dedicated page (typically `/admin`) so editors can sign in and manage content without opening Elements.

### Which component should I use?

| If you want to...                                          | Use this component                                     |
| ---------------------------------------------------------- | ------------------------------------------------------ |
| List posts, products, team members, or any group of items  | [Collection](collection.md)                            |
| Show a single post, project, or profile page               | [Item](item.md)                                        |
| Add numbered page navigation to a long list                | [Collection Pagination](collection-pagination.md)      |
| Add a "Load more" button to a long list                    | [Load More](load-more.md)                              |
| Suggest related content under a post                       | [Related Items](related-items.md)                      |
| Let visitors leave comments on a post                      | [Comments](comments.md)                                |
| Add an instant search box                                  | [Search](search.md)                                    |
| Show every tag in a collection as a list of links          | [Tag List](tag-list.md)                                |
| Let editors manage content from the browser                | [Online Editor](online-editor.md)                      |

### How components access your data

Any component placed inside a Collection or Item can read the current CMS data using `{{item.*}}` and `{{collection.*}}` references. This is what makes the system feel "magical" — drop a Text or Heading component into a Collection, type `{{item.title}}`, and it just works.

For the full data reference, see [Template Data](../template-data.md).
