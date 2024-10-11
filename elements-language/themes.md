# Themes

Element Themes are based on standard [Tailwind config files](https://tailwindcss.com/docs/configuration). They can be built by hand or inside of the Theme Studio in Elements.

### Theme Structure

A theme contains three files, they are should be stored in a folder using a reverse domain name. They can be distibuted inside of .elementspacks alongisde components.

*
* com.yourdomain.themes.exampletheme
  * icon.png (440 × 280 pixels)
  * info.json
  * theme.json

<figure><img src="../.gitbook/assets/CleanShot 2024-10-11 at 10 .14.29@2x.png" alt=""><figcaption></figcaption></figure>

### Info. json file

The info file store basic information about your theme.

```
{
  "author": "Yoru Awesome Company Name",
  "title": "Example Theme",
  "subTitle": "clean, bold, and classy.",
  "tags": [
    "clean",
    "bold",
    "classy"
  ],
  "build": "100",
  "version": "1.0.0",
  "deprecated": false,
  "helpURL": "https://forums.realmacsoftware.com/",
  "infoURL": "https://www.realmacsoftware.com/",
  "googleFontNames": [
    "Playfair Display"
  ]
}

```

### theme.json

The Theme json files are based on standard [Tailwind config files](https://tailwindcss.com/docs/configuration). They can be built by hand or inside of the Theme Studio in Elements. All values from the Theme Studio can be set inside of a theme.

<figure><img src="../.gitbook/assets/CleanShot 2024-07-27 at 6 .23.20@2x.png" alt=""><figcaption><p>A screenshot of the Tailwind Theme Studio in Elements for macOS.</p></figcaption></figure>
