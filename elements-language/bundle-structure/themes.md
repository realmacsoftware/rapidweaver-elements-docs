---
icon: masks-theater
---

# Themes

Element Themes are based on standard [Tailwind config files](https://tailwindcss.com/docs/configuration). They can be built using the Theme Studio in Elements.

Themes are a set of pre-configured values based on the available settings inside of the Theme Studio. The gif below shows how a site can look radically different depending on the theme chosen.

<figure><img src="../../.gitbook/assets/CleanShot 2024-10-11 at 10 .45.49.gif" alt=""><figcaption><p>Changing Themes in Elements Beta (October 2024)</p></figcaption></figure>

## Theme Structure

A theme contains three files, they should be stored in a folder using a reverse domain name. They can be distributed in the same pack alongisde components.

* youraddon.elementsdevpack
  * themes
    * com.yourdomain.themes.exampletheme
      * [icon.png](themes.md#icon) (440 × 280 pixels)
      * [info.json](themes.md#info.-json-file)
      * [theme.json](themes.md#theme.json)

<figure><img src="../../.gitbook/assets/CleanShot 2024-10-11 at 10 .14.29@2x.png" alt=""><figcaption><p>Example layout for an Elements Dev Pack</p></figcaption></figure>

### Icon

The icon for your theme should be a PNG, and sized at 440x280px. Ideally it will use the font and colour from the theme to give the user as idea of what to expect.

<figure><img src="../../.gitbook/assets/CleanShot 2024-10-11 at 10 .20.54@2x.png" alt=""><figcaption><p>Included Themes in the beta version of Elements (October 2024)</p></figcaption></figure>

### Info. json file

The info file stores basic information about your theme, including the required Google Fonts.

```
{
  "author": "Awesome Company",
  "title": "Example Theme",
  "subTitle": "clean, bold, and classy.",
  "helpURL": "https://forums.realmacsoftware.com/",
  "infoURL": "https://www.realmacsoftware.com/",
  "googleFontNames": [
    "Playfair Display"
  ]
}
```

## Theme Settings

The following settings are required for a complete Elements Theme that will be compatible with users’ projects.

### Theme Colours (Required)

As well as all of the named [Default Tailwind Colours](https://tailwindcss.com/docs/colors), Element Themes must also specify these additional colours:

* **Brand** – Dominant colour used for branding and key items.
* **Accent** – Complementary color used for secondary elements, and supporting details.
* **Surface** – Background color that provides contrast behind text and elements.
* **Text** – Primary color for headings and body text, ensuring readability and visual clarity.
* **Black** – Pure black (will eventually be automatically defined by Elements).
* **White** – Pure white (will eventually be automatically defined by Elements).

<figure><img src="../../.gitbook/assets/CleanShot 2025-03-17 at 6 .06.41@2x.png" alt=""><figcaption></figcaption></figure>

### Screens (Automatic)

Screens are mananged by Elements, so do not need to be defined within the theme.

<figure><img src="../../.gitbook/assets/CleanShot 2025-03-17 at 6 .07.49@2x.png" alt=""><figcaption></figcaption></figure>

### Font Families (Required)

When defining Google Fonts within your theme, ensure they are included in the [theme info.json](themes.md#info.-json-file) for consistency and proper loading.

* **Body** - The primary font used for main body text to ensure readability and consistency.
* **Code** - Typically a monospaced font for displaying code snippets and technical content.
* **Heading** - The designated font for headings, ensuring clear typographic hierarchy.
* **Quote** - Usually a serif font, enhancing the distinctiveness of blockquotes and citations.

<figure><img src="../../.gitbook/assets/CleanShot 2025-03-17 at 6 .07.19@2x.png" alt=""><figcaption></figcaption></figure>

### Font Size (Required)

Must include the Default Tailwind Font Sizes.

### Spacing (Required)

Must include the Default Tailwind Spacing Scale.

### Shadow (Required)

Must include the Default Tailwind Spacing Scale, along with an **aditional "Default" value** for the theme.

### Border Width (Required)

Must include the Default Tailwind Border Width Scale, along with an **aditional "Default" value** for the theme.

### Border Radius (Required)

Must include the Default Tailwind Border Radius Scale, along with an **aditional "Default" value** for the theme.

### Typography (Required)

Must be setup with a default "article" typography style.

<figure><img src="../../.gitbook/assets/CleanShot 2025-03-17 at 6 .05.55@2x.png" alt=""><figcaption><p>"article" Typography Style</p></figcaption></figure>
