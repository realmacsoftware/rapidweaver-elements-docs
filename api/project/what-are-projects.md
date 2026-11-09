---
icon: circle-question
---

# What is a Project?

To include a project in your Elements Pack you'll need to add the project, a thumbnail and a projects.json file. Here's an example screenshot of how this looks:

<figure><img src="../../.gitbook/assets/CleanShot 2026-04-03 at 11 .03.12@2x.png" alt=""><figcaption></figcaption></figure>

The projects.json file should contain the following keys:&#x20;

* `filename` - the filename for the project, must including .elements extension.
* `title` - The title of the project.
* `description` - a short description about the project.
* `thumbanail` - the name of the thumbnail in the projects folder.

### projects.json Example

You can use the following code as a starting point for your own projects.json file.

```json
{
    "projects": [{
        "filename": "Modern business.elements",
        "title": "Modern business",
        "description": "Show the world you mean business.",
        "thumbnail": "thumbnail.jpg"
    }
]
}
```

### Project thumbnail guidelines.

The Project thumbnail should represent your project, ideally a screenshot of the home page.

* Dimension: 1920(w)x1080(h)
* Format: jpg

The New Projects window below will give you some guidance on how your thumbnail should look. Do not include extra type, logos, or watermarks. Try to keep the thumbnail as close as possible to the actual look of the project.

<figure><img src="../../.gitbook/assets/CleanShot 2026-04-03 at 11 .13.49@2x.png" alt=""><figcaption></figcaption></figure>
