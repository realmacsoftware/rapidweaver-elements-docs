---
icon: circle-question
---

# What are Themes?

Element Themes are based on standard [Tailwind config files](https://tailwindcss.com/docs/configuration). They can be built using the Theme Studio in Elements.

Themes are a set of pre-configured values based on the available settings inside of the Theme Studio. The gif below shows how a site can look radically different depending on the theme chosen.

## Theme Structure

A theme contains three files, they should be stored in a folder using a reverse domain name. They can be distributed in the same pack alongisde components.

* youraddon.elementsdevpack
  * themes
    * com.yourdomain.themes.exampletheme
      * [icon.png](what-are-themes.md#icon) (440 × 280 pixels)
      * [info.json](what-are-themes.md#info.-json-file)
      * [theme.json](what-are-themes.md#theme.json)

### Icon

The icon for your theme should be a PNG, and sized at 440x280px. Ideally it will use the font and colour from the theme to give the user as idea of what to expect.

### Info. json file

The info file stores basic information about your theme, including the required Google Fonts.

| Key               | Type    | Notes                                                                                                                                                                                                                               |
| ----------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `author`          | string  | The name of the author or publishing company.                                                                                                                                                                                       |
| `title`           | string  | The display name of the theme shown inside RapidWeaver.                                                                                                                                                                             |
| `subTitle`        | string  | A short descriptor shown below the title.                                                                                                                                                                                           |
| `helpURL`         | string  | A URL to the online help documentation.                                                                                                                                                                                             |
| `infoURL`         | string  | A URL to the marketing page.                                                                                                                                                                                                        |
| `googleFontNames` | array   | Font family names loaded from Google Fonts. Must match the families used in `theme.json`.                                                                                                                                           |
| `deprecated`      | boolean | Marks the theme as deprecated. Default `false`.                                                                                                                                                                                     |
| `deploy`          | boolean | Should this theme be included when deploying a pack, true or false. Default `true`. Set to `false` to keep a theme for local development only — it will still appear in Theme Studio but will be excluded from the built `.rwpack`. |
| `tailwindVersion` | string  | This value must be set to `v4` to use Tailwind 4 in Elements 3.0 or newer.                                                                                                                                                          |
| `build`           | integer | Can be included to specify a build number for the theme.                                                                                                                                                                            |

```
{
  "author": "Awesome Company",
  "title": "Example Theme",
  "subTitle": "clean, bold, and classy.",
  "build": "100",
  "helpURL": "https://forums.realmacsoftware.com/",
  "infoURL": "https://www.realmacsoftware.com/",
  "tailwindVersion": "v4",
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

### Screens (Automatic)

Screens are mananged by Elements, so do not need to be defined within the theme.

### Font Families (Required)

When defining Google Fonts within your theme, ensure they are included in the [theme info.json](what-are-themes.md#info.-json-file) for consistency and proper loading.

* **Body** - The primary font used for main body text to ensure readability and consistency.
* **Code** - Typically a monospaced font for displaying code snippets and technical content.
* **Heading** - The designated font for headings, ensuring clear typographic hierarchy.
* **Quote** - Usually a serif font, enhancing the distinctiveness of blockquotes and citations.

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
