---
description: Reveal more Collection items in place, without a full page reload.
---

# Load More

The **Load More** component reveals additional items from a parent [Collection](collection.md) without navigating to a new page. Visitors stay where they are, click the button, and the next batch appears below the existing items — a smoother, more app-like browsing experience than numbered pages.

It's ideal for long lists where readers benefit from continuous scrolling: blog archives, project portfolios, product catalogues, and infinite-feed-style layouts.

{% hint style="warning" %}
**The** [**Collection Pagination**](collection-pagination.md) **and Load More components cannot be used together.** They both control how items are fetched and displayed within a Collection, so enabling both at the same time will conflict. Pick Pagination for clear page-based navigation, or Load More for a progressive experience.
{% endhint %}

### Where to place it

Drop the Load More component into the **After** drop zone of a [Collection](collection.md). The Collection still controls which items are shown, how many appear initially (its **Items Per Page** setting), and how they're sorted and filtered — Load More just hooks into that same pipeline to fetch the next batch.

```
Collection (Items Per Page = 6)
├── Before zone — heading, intro
├── Repeating zone — the per-item card template
└── After zone
    └── Load More — the button shown when there's more to fetch
```

### How it works

When the page first loads, the Collection renders its initial batch of items (set by **Items Per Page** on the Collection). The Load More button calls back to the CMS API for the next page, clones your repeating-item template once per new item, and appends them in place.

If there are no more items to show, the button is automatically hidden — no need to handle the empty case yourself.

### Designing the button

Whatever you place inside the Load More drop zone becomes the button. There are no built-in label fields — instead, drop a Heading, Text, or Button component into the zone and design it like any other element on your page. A button with an icon, a hover state, and centered alignment is a common choice.

The component handles the click target and the disabled/loading states for you. While a fetch is in flight, the wrapper applies `opacity-50` and a `cursor-not-allowed` class so your button visually communicates the loading state without you wiring it up.

### Settings

Load More has no functional settings — its behaviour is fully driven by the parent Collection. The inspector exposes only the **Advanced** group (Classes and ID) for custom styling and anchors.

If you want to change how many items load per click, change the **Items Per Page** value on the parent Collection. Each Load More click fetches one Collection page worth of items.

### Common pitfalls

**The Load More button doesn't appear at all.**\
Make sure it's placed inside a Collection's After zone, not at the page level. Outside a Collection, it has no parent to fetch from.

**Clicking the button does nothing.**\
The component fetches via the CMS API, which means the page must be served from a working PHP environment. If the page extension is `.html`, or PHP is misconfigured, the request will silently fail. See [Troubleshooting](../../getting-started/troubleshooting/).

**Both Pagination and Load More appear on the page.**\
Remove one — they can't coexist. They both manage the same paging state and will fight each other.

**New items don't match the existing items' design.**\
Load More renders new items using the same template as the Collection's Repeating zone. If new items look different, double-check that you haven't placed components _outside_ the Repeating zone that you intended to be part of each card.
