---
description: Show one randomly selected piece of content each time a page loads
---

# Random Content (Paid)

{% hint style="success" %}
Random Content is available as a **paid product via the Elements Store**. Install the current version of Elements before adding it to a project.
{% endhint %}

Random Content displays one item selected at random whenever a page loads. Each item is a dropzone that accepts any Elements components, making it useful for rotating testimonials, promotions, projects, quotations, or complete hero variations.

Choose JavaScript for a straightforward browser-based setup, or PHP when the selection needs to happen on the server. Only the selected item is inserted into the visible page.

<a href="elementsapp://storeProduct/com.elementsplatform.randomcontentpack" class="button primary" data-icon="store">Purchase Random Content</a>

{% embed url="https://www.youtube.com/watch?v=lX6LB9BzJsU" %}

### Features

* **One random item per page load** — Show a different variation without manually changing the page.
* **Component dropzones** — Each item can contain a complete Elements layout.
* **Up to 20 items** — Create a small variation or a larger content pool.
* **JavaScript and PHP modes** — Choose browser-side convenience or server-side rendering.
* **Focused editor preview** — Work on one item at a time without the other variations getting in the way.

### Requirements

Before using Random Content, make sure you have:

* The Random Content pack installed from the Elements Store.
* At least one completed content item.
* PHP hosting and a `.php` page extension if you select PHP mode.

{% hint style="warning" %}
PHP mode must be published as PHP on a server that supports it. JavaScript mode requires JavaScript in the visitor’s browser and is less suitable when every variation must be available to search engines.
{% endhint %}

### Supported Content and File Types

Random Content supports:

* Any Elements components placed inside its item dropzones.
* Between 1 and 20 content variations.
* Client-side JavaScript or server-side PHP rendering.

### How to Use Random Content

You’ll find Random Content under **Interactive** in the Components list.

1. Drag **Random Content** onto the page.
2. Set **Items** to the number of variations you need.
3. Use **Active Item** to select an item in the editor, then add its child components.
4. Repeat until every item contains finished content.
5. Choose JavaScript or PHP from **Render Mode**.
6. Preview or publish the page, then reload it several times to check the variations.

### Component Settings

#### Content

**Render Mode**

* **JavaScript** — The browser chooses and inserts one item after the page loads. Visitors with JavaScript disabled see a message asking them to enable it.
* **PHP** — The server chooses one item while generating the page. This is the better option when the selected content should be present in the initial HTML.

**Active Item**

Chooses which numbered item is visible while editing. This setting only changes the editor view; it does not affect which item is selected on the published page.

**Items**

Sets the number of content variations from 1 to 20. The default is 3.

#### Advanced

Use **Classes** to add custom CSS classes and **ID** to assign a unique HTML identifier.

### Accessibility

* Make every variation understandable in the same page context and give each one an equivalent purpose.
* Do not place essential instructions in only one random item.
* Check headings and landmarks in every variation so that any selected item preserves a logical page structure.
* If JavaScript is not guaranteed, use PHP mode or provide important information outside Random Content.

### Tips and Best Practices

* **Keep the variations comparable:** Similar dimensions reduce layout movement between page loads.
* **Use PHP for indexable content:** Server-side selection places the chosen variation in the initial response.
* **Finish every item:** Empty items can be selected and leave a blank space.
* **Test repeatedly:** Reload enough times to confirm every variation works on its own.

### Troubleshooting

#### The page shows PHP code or reports a server error

Confirm that Render Mode is set to PHP, the page extension is `.php`, and the hosting server supports PHP. Remove any older `.html` copy of the same page from the server.

#### Nothing appears in JavaScript mode

Make sure the selected item count matches the items you populated and that JavaScript is enabled. Check every Active Item for an empty dropzone.

#### The same item appears several times

Selection is random, so repeats are expected. Reloading does not cycle through the items in a fixed order.

### Related Components

* [Content Slider](../components/content-slider.md) — Let visitors move through several content items themselves.
* [Reveal](../components/reveal.md) — Reveal a chosen block in response to an interaction.

{% include "../../.gitbook/includes/common-controls.md" %}
