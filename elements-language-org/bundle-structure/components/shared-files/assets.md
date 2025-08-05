# Assets

### Assets Folder

Assets used by one or more components can be stored here. This includes Javascript, Fonts, CSS, Images etc.&#x20;

When a component from the pack is added to a page, all shared templates are also added to the page. This will only happen once per page, regardless of the number of components added to the page.

To use shared assets, create an html file in the [shared Templates folder](templates.md).

The following HTML file placed in the shared templates \`headEnd\` folder links to an asset called "snowstorm.js" in the shared Assets folder.

```
<script src="{{assetPath}}/snowstorm.js"></script>
```

<figure><img src="../../../../.gitbook/assets/CleanShot 2024-12-01 at 2 .51.52@2x.png" alt=""><figcaption></figcaption></figure>
