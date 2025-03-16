---
icon: masks-theater
---

# Themes

Element Themes are based on standard [Tailwind config files](https://tailwindcss.com/docs/configuration). They can be built using the Theme Studio in Elements.

Themes are a set of pre-configured values based on the available settings inside of the Theme Studio. The gif below shows how a site can look radically different depending on the theme chosen.

<figure><img src="../../.gitbook/assets/CleanShot 2024-10-11 at 10 .45.49.gif" alt=""><figcaption><p>Changing Themes in Elements Beta (October 2024)</p></figcaption></figure>

### Required Theme Colours

As well as the named [Default Tailwind Colours](https://tailwindcss.com/docs/colors), Element Themes must also specify these additional colours:

* **Brand** – The primary brand color, commonly used for logos and brand assets.
* **Primary** – The dominant colour used for interface elements, such as buttons and key actions.
* **Secondary** – A complementary color used for additional UI elements, accents, and supporting details.
* **Surface** – The background color that provides contrast behind text and UI elements.
* **Text** – The primary color for headings and body text, ensuring readability and visual clarity.
* **White** – Usually just shades of Black, but can be a deep, rich color palette.
* **Black** – Usually just shades of White, but can be a soft, neutral color palette.

### Theme Structure

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

The info file stores basic information about your theme, inlcuding the required Google Fonts.

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



<figure><img src="../../.gitbook/assets/CleanShot 2024-07-27 at 6 .23.20@2x.png" alt=""><figcaption><p>A screenshot of the Tailwind Theme Studio in Elements for macOS.</p></figcaption></figure>
