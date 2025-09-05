---
description: Access the latest Elements Addons, directly from the source.
hidden: true
icon: rss
---

# Marketplace API

The Elements Marketplace API provides a simple, read-only JSON endpoint for fetching all available Addons. Use this to power in-app listings, build third-party tools, or stay up to date with the latest components, templates, and integrations available for Elements.

### Example Use Case

The Marketplace API is used inside of the Elements Project Chooser to return a list of free projects.

<figure><img src="../.gitbook/assets/CleanShot 2025-06-16 at 10 .09.53@2x.png" alt=""><figcaption><p>Project Chooser inside of Elements for macOS.</p></figcaption></figure>

### Endpoint

The Marketplace API is accessible via a single, public URL. This endpoint returns a JSON array of all current Addons available in the Elements Marketplace — including templates, components, and integrations.

You can fetch the data using any standard HTTP client, or load it directly into your app or website.

```
https://marketplace.realmacsoftware.com/api/elements/addons
```

### Response

API responses are paginated and results for the current page are found in the `data` array. Here’s an example of the generic response structure:

```json
{
    "current_page":1,
    "data":[...],
    "first_page_url":"https:\/\/marketplace.realmacsoftware.com\/api\/elements\/addons?page=1",
    "from":1,"last_page":7,
    "last_page_url":"https:\/\/marketplace.realmacsoftware.com\/api\/elements\/addons?page=7",
    "links":[
        {"url":null,"label":"&laquo; Previous","active":false},
        {"url":"https:\/\/marketplace.realmacsoftware.com\/api\/elements\/addons?page=1","label":"1","active":true},
        {"url":"https:\/\/marketplace.realmacsoftware.com\/api\/elements\/addons?page=2","label":"2","active":false},
        {"url":"https:\/\/marketplace.realmacsoftware.com\/api\/elements\/addons?page=3","label":"3","active":false},
        {"url":"https:\/\/marketplace.realmacsoftware.com\/api\/elements\/addons?page=4","label":"4","active":false},
        {"url":"https:\/\/marketplace.realmacsoftware.com\/api\/elements\/addons?page=5","label":"5","active":false},
        {"url":"https:\/\/marketplace.realmacsoftware.com\/api\/elements\/addons?page=6","label":"6","active":false},
        {"url":"https:\/\/marketplace.realmacsoftware.com\/api\/elements\/addons?page=7","label":"7","active":false},
        {"url":"https:\/\/marketplace.realmacsoftware.com\/api\/elements\/addons?page=2","label":"Next &raquo;","active":false}
    ],"next_page_url":"https:\/\/marketplace.realmacsoftware.com\/api\/elements\/addons?page=2",
    "path":"https:\/\/marketplace.realmacsoftware.com\/api\/elements\/addons",
    "per_page":2,
    "prev_page_url":null,
    "to":2,
    "total":13
}
```

### List Elements Addons

`GET` `/api/elements/addons`\
To appear in the listing, Addons must meet the following criteria:

* Approved review status
* At least one version
* Has a preview image

Optional properties are **omitted** when they have no value. The following properties are optional:

* `shortDescription`
* `shortDescriptionHTML`
* `elementsCloudId`
* `links.onlinePreview`

Here’s an example of the data structure for an Addon result:

```json
{
    "title": "Link in Bio",
    "version":"0.9",
    "developer":"Realmac Software",
    "shortDescription":"Create a beautiful and customizable link-in-bio website for free, where you can showcase links to all your social media accounts, websites, and more. Perfect for creators, and anyone looking to unify their online presence in one easy-to-share link.",
    "shortDescriptionHTML":"<p>Create a beautiful and customizable link-in-bio website for free, where you can showcase links to all your social media accounts, websites, and more. Perfect for creators, and anyone looking to unify their online presence in one easy-to-share link.<\/p>",
    "description":"This user-friendly link-in-bio project is designed for effortless customization, allowing you to create a personalized page in just seconds.\n\nIn addition to linking to your social networks, the Link in Bio template includes sections to showcase your achievements, projects, and favorite apps.\n\nStandout Features\n\nLight &amp; Dark ModeThemes: Customize Text, Brand, and Surface ColorsResponsive: Optimized for Mobile and Small-Medium Breakpoints\n\nHelp Customizing the Project\n\nIf you need help customizing the project, feel free to post on the RapidWeaver Forum, we\u2019re always happy to help!",
    "descriptionHTML":"<p>This user-friendly link-in-bio project is designed for effortless customization, allowing you to create a personalized page in just seconds.<\/p>\n\n<p>In addition to linking to your social networks, the Link in Bio template includes sections to showcase your achievements, projects, and favorite apps.<\/p>\n\n<h2>Standout Features<\/h2>\n\n<ul><li><p><strong>Light &amp; Dark Mode<\/strong><\/p><\/li><li><p><strong>Themes:<\/strong> Customize Text, Brand, and Surface Colors<\/p><\/li><li><p><strong>Responsive:<\/strong> Optimized for Mobile and Small-Medium Breakpoints<\/p><\/li><\/ul>\n\n<h2>Help Customizing the Project<\/h2>\n\n<p>If you need help customizing the project, feel free to post on the RapidWeaver Forum, we\u2019re always happy to help!<\/p>",
    "price":0,
    "priceForHumans":"Free",
    "kind":"project",
    "elementsCloudId":"NBzpojokRjtH",
    "images": {
        "icon":"https:\/\/rapidweavermarketplace.ams3.cdn.digitaloceanspaces.com\/images\/2030\/icon.jpg",
        "preview":"https:\/\/rapidweavermarketplace.ams3.cdn.digitaloceanspaces.com\/images\/2025\/conversions\/Project-small.jpg"
    },
    "links": {
        "marketplace":"https:\/\/marketplace.realmacsoftware.com\/addons\/01jds5e3cpfsetd79pfy9mg8q4",
        "onlinePreview":"https:\/\/forums.realmacsoftware.com\/t\/project-link-in-bio\/45658",
        "developer":"https:\/\/www.realmacsoftware.com",
        "developerSupport":"https:\/\/www.realmacsoftware.com\/support\/"
    }
}
```

### Query Parameters

You can refine the returned results by appending query parameters to the URL. For example:

```
https://marketplace.realmacsoftware.com/api/elements/addons?items=5
```

| Name    | Description                                                            | Default | Options                                                                                              |
| ------- | ---------------------------------------------------------------------- | ------- | ---------------------------------------------------------------------------------------------------- |
| `free`  | Filter results to show only addons which are available free of charge. | `false` | `true`                                                                                               |
| `items` | Set the pagination size. Maximum 100.                                  | `50`    |                                                                                                      |
| `kind`  | Filter results by the kind of Addon. Single value.                     | -       | <p><code>component</code><br><code>project</code><br><code>resource</code><br><code>theme</code></p> |
| `page`  | Requested page of paginated results.                                   | `1`     | Integer                                                                                              |
