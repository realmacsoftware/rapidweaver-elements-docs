---
description: Learn more about the Elements Store API and deep linking system
---

# Store API & Deep Linking

The Elements Store API and deep linking system allow you to integrate your products more seamlessly with the wider Elements ecosystem. Whether you are building companion apps, marketing pages, automation tools, or partner dashboards, you can programmatically access store data and create direct links that open products inside RapidWeaver Elements.

This page outlines how to retrieve catalog data, access product resources and release notes, and construct deep links that take users straight to a specific product in the built-in Store. Used responsibly and with sensible caching, these tools make it easy to surface accurate, up-to-date information while providing a smooth experience for your customers.

### Deep linking to Element Products

Elements supports deep linking to products within its built-in Store, allowing you to send users directly to a specific product page inside RapidWeaver Elements. This makes it easy to connect marketing websites, documentation, onboarding flows, emails, or companion apps straight to the exact pack you want to showcase, without requiring users to manually search the Store.

When a deep link is triggered, Elements opens and navigates directly to the relevant product, creating a fast and seamless experience. This is especially useful for upgrade prompts, cross-promotion between packs, launch announcements, and partner integrations where precision and convenience matter.

Deep linking helps reduce friction, improves conversion, and ensures your customers land exactly where you intend inside the Elements ecosystem.

{% hint style="warning" %}
**Important:** Store links require RapidWeaver Elements 2.0 or newer on macOS.
{% endhint %}

To link to the Elements Store, use: `elementsapp://storeProduct/`. To link to your product, append the reverse domain name from your `info.json` file in your devpack.

For example, consider this `info.json` for the Essentials pack:

```json
{
  "author": "Elements Platform",
  "identifier": "com.elementsplatform.essentials",
  "version": 1,
  "build": 1
}
```

Take the `identifier` value: `com.elementsplatform.essentials`, and append it to the store link: `elementsapp://storeProduct/com.elementsplatform.essentials`.

Link Example:

👉 [View Essentials Pack in the Elements Store](elementsapp://storeProduct/com.elementsplatform.essentials) (Elements Required)

### Listing Element Products

Please use the following responsibly. We strongly recommend caching responses locally to minimise load and ensure good performance.

The full product catalogue is available at:

[https://store.elementsapp.cloud/catalog.json](https://store.elementsapp.cloud/catalog.json)

This is rebuilt whenever any pack is published/unpublished/updated. It contains all public store product data needed for browse, search, and category filtering.

This endpoint returns all products currently available in the Elements Store:

```
{
    "version": 1,
    "generatedAt": "2026-02-24T12:00:00Z",
    "packs": [
        {
            "packId": "com.example.gallery-pro",
            "version": 1,
            "build": 5,
            "packName": "Gallery Pro",
            "developerName": "Elements Platform",
            "description": "Advanced gallery component...",
            "tags": ["gallery", "photos", "lightbox"],
            "contentTypes": ["component", "template"],
            "thumbnailUrl": "https://assets.elementsapp.cloud/live/...",
            "screenshots": ["https://..."],
            "resourceFiles": ["preview1.png"],
            "features": ["Lightbox", "Grid Layout"],
            "infoURL": "https://...",
            "pricing": {
                "enableFree": false,
                "enableLifetime": true,
                "enableSubscription": false,
                "lifetimeUSD": 2999,
                "subscriptionUSD": 0,
                "discountPercent": 20,
                "discountEndDate": "20260301"
            },
            "featured": true,
            "publishedDate": "20260220120000",
            "lastUpdated": "20260222150000"
        }
    ]
}
```

Resources referenced in the catalog.json file can be accessed using the following URL structure:

`https://assets.elementsapp.cloud/live/{packId}-v{version}/resources/{filename}`

Release notes for each product are available at:

`https://assets.elementsapp.cloud/live/{packId}-v{version}/release-notes.json`

For example:

`https://assets.elementsapp.cloud/live/com.elementsplatform.marqueepack-v1/release-notes.json`
