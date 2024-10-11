# Themes

Element Themes are based on standard [Tailwind config files](https://tailwindcss.com/docs/configuration). They can be built by hand or inside of the Theme Studio in Elements.&#x20;

Themes are a set of pre-configured values based on the available settings inside of the Theme Studio. The gif below shows how a site can look radically different depending on the theme chosen.

<figure><img src="../.gitbook/assets/CleanShot 2024-10-11 at 10 .45.49.gif" alt=""><figcaption><p>Changing Themes in Elements Beta (October 2024)</p></figcaption></figure>

### Theme Structure

A theme contains three files, they should be stored in a folder using a reverse domain name. They can be distributed inside of .elementspacks alongisde components.

* youraddon.elementsdevpack
  * themes
    * com.yourdomain.themes.exampletheme
      * [icon.png](themes.md#icon) (440 × 280 pixels)
      * [info.json](themes.md#info.-json-file)
      * [theme.json](themes.md#theme.json)

<figure><img src="../.gitbook/assets/CleanShot 2024-10-11 at 10 .14.29@2x.png" alt=""><figcaption><p>Example layout for an Elements Dev Pack</p></figcaption></figure>

### Icon

The icon for your theme should be a PNG, and sized at 440x280px. Ideally it will use the font and colour from the theme to give the user as idea of what to expect.

<figure><img src="../.gitbook/assets/CleanShot 2024-10-11 at 10 .20.54@2x.png" alt=""><figcaption><p>Included Themes in the beta version of Elements (October 2024)</p></figcaption></figure>

### Info. json file

The info file store basic information about your theme.

```
{
  "author": "Your Awesome Company Name",
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

The following is an example of a theme.json file. Please note; not all theme values are defined in the theme sample below.

```json
{
    "theme": {
        "screens": {
            
        },
        "extend": {
            "fontSize": {
                "6xl": [
                    "3.75rem",
                    {
                        "lineHeight": "4.50rem",
                        "letterSpacing": "-0.01rem",
                        "fontWeight": "400"
                    }
                ],
                "2xl": [
                    "1.50rem",
                    {
                        "lineHeight": "2.00rem",
                        "letterSpacing": "-0.01rem",
                        "fontWeight": "400"
                    }
                ],
                "base": [
                    "1.00rem",
                    {
                        "fontWeight": "400",
                        "lineHeight": "1.50rem",
                        "letterSpacing": "-0.01rem"
                    }
                ],
                "9xl": [
                    "8.00rem",
                    {
                        "fontWeight": "400",
                        "letterSpacing": "-0.01rem",
                        "lineHeight": "8.50rem"
                    }
                ],
                "8xl": [
                    "6.00rem",
                    {
                        "fontWeight": "400",
                        "lineHeight": "6.50rem",
                        "letterSpacing": "-0.01rem"
                    }
                ],
                "3xl": [
                    "1.88rem",
                    {
                        "letterSpacing": "-0.01rem",
                        "lineHeight": "2.25rem",
                        "fontWeight": "400"
                    }
                ],
                "7xl": [
                    "4.50rem",
                    {
                        "fontWeight": "400",
                        "lineHeight": "5.50rem",
                        "letterSpacing": "-0.01rem"
                    }
                ],
                "sm": [
                    "0.88rem",
                    {
                        "fontWeight": "400",
                        "lineHeight": "1.25rem",
                        "letterSpacing": "-0.01rem"
                    }
                ],
                "lg": [
                    "1.12rem",
                    {
                        "fontWeight": "400",
                        "lineHeight": "1.75rem",
                        "letterSpacing": "-0.01rem"
                    }
                ],
                "xl": [
                    "1.25rem",
                    {
                        "lineHeight": "1.75rem",
                        "letterSpacing": "-0.01rem",
                        "fontWeight": "400"
                    }
                ],
                "4xl": [
                    "2.25rem",
                    {
                        "fontWeight": "400",
                        "lineHeight": "2.50rem",
                        "letterSpacing": "-0.01rem"
                    }
                ],
                "5xl": [
                    "3.00rem",
                    {
                        "lineHeight": "3.50rem",
                        "fontWeight": "400",
                        "letterSpacing": "-0.01rem"
                    }
                ],
                "xs": [
                    "0.75rem",
                    {
                        "lineHeight": "1.00rem",
                        "fontWeight": "400",
                        "letterSpacing": "-0.01rem"
                    }
                ]
            },
            "borderRadius": {
                "DEFAULT": "0px"
              },
              "borderWidth": {
                "DEFAULT": "2px"
                },
            "spacing": {
                "0": "0px",
                "48": "192px",
                "11": "44px",
                "6": "24px",
                "2": "8px",
                "36": "144px",
                "72": "288px",
                "32": "128px",
                "64": "256px",
                "14": "56px",
                "28": "112px",
                "3": "12px",
                "10": "40px",
                "20": "80px",
                "44": "176px",
                "12": "48px",
                "7": "28px",
                "px": "1px",
                "16": "64px",
                "52": "208px",
                "40": "160px",
                "96": "384px",
                "4": "16px",
                "2.5": "10px",
                "1": "4px",
                "5": "20px",
                "80": "320px",
                "9": "36px",
                "1.5": "6px",
                "0.5": "2px",
                "3.5": "14px",
                "56": "224px",
                "8": "32px",
                "60": "240px",
                "24": "96px"
            }
        },
        "colors": {
            "gray": {
                "400": "#9ca3af",
                "900": "#111827",
                "500": "#6b7280",
                "200": "#e5e7eb",
                "700": "#374151",
                "800": "#1f2937",
                "600": "#4b5563",
                "100": "#f3f4f6",
                "300": "#d1d5db",
                "50": "#f9fafb",
                "DEFAULT": "#6b7280"
            },
            "sky": {
                "800": "#075985",
                "200": "#bae6fd",
                "900": "#0c4a6e",
                "DEFAULT": "#0ea5e9",
                "300": "#7dd3fc",
                "100": "#e0f2fe",
                "500": "#0ea5e9",
                "700": "#0369a1",
                "50": "#f0f9ff",
                "600": "#0284c7",
                "400": "#38bdf8"
            },
            "purple": {
                "700": "#7e22ce",
                "100": "#f3e8ff",
                "300": "#d8b4fe",
                "800": "#6b21a8",
                "400": "#c084fc",
                "900": "#581c87",
                "50": "#faf5ff",
                "500": "#a855f7",
                "200": "#e9d5ff",
                "600": "#9333ea",
                "DEFAULT": "#a855f7"
            },
            "pink": {
                "DEFAULT": "#ec4899",
                "300": "#f9a8d4",
                "600": "#db2777",
                "200": "#fbcfe8",
                "700": "#be185d",
                "800": "#9d174d",
                "500": "#ec4899",
                "400": "#f472b6",
                "50": "#fdf2f8",
                "900": "#831843",
                "100": "#fce7f3"
            },
            "indigo": {
                "900": "#312e81",
                "500": "#6366f1",
                "700": "#4338ca",
                "50": "#eef2ff",
                "400": "#818cf8",
                "300": "#a5b4fc",
                "800": "#3730a3",
                "200": "#c7d2fe",
                "600": "#4f46e5",
                "DEFAULT": "#6366f1",
                "100": "#e0e7ff"
            },
            "black": {
                "800": "#000000",
                "200": "#6c6c6c",
                "DEFAULT": "#000000",
                "700": "#000000",
                "500": "#000000",
                "100": "#9a9a9a",
                "600": "#000000",
                "300": "#404040",
                "900": "#000000",
                "50": "#cbcbcb",
                "400": "#1a1a1a"
            },
            "lime": {
                "50": "#f7fee7",
                "600": "#65a30d",
                "DEFAULT": "#84cc16",
                "400": "#a3e635",
                "700": "#4d7c0f",
                "500": "#84cc16",
                "100": "#ecfccb",
                "900": "#365314",
                "300": "#bef264",
                "200": "#d9f99d",
                "800": "#3f6212"
            },
            "stone": {
                "700": "#44403c",
                "600": "#57534e",
                "800": "#292524",
                "200": "#e7e5e4",
                "50": "#fafaf9",
                "300": "#d6d3d1",
                "900": "#1c1917",
                "500": "#78716c",
                "400": "#a8a29e",
                "100": "#f5f5f4",
                "DEFAULT": "#78716c"
            },
            "amber": {
                "900": "#78350f",
                "700": "#b45309",
                "500": "#f59e0b",
                "600": "#d97706",
                "800": "#92400e",
                "DEFAULT": "#f59e0b",
                "200": "#fde68a",
                "300": "#fcd34d",
                "100": "#fef3c7",
                "400": "#fbbf24",
                "50": "#fffbeb"
            },
            "yellow": {
                "200": "#fef08a",
                "300": "#fde047",
                "500": "#eab308",
                "700": "#a16207",
                "50": "#fefce8",
                "600": "#ca8a04",
                "800": "#854d0e",
                "DEFAULT": "#eab308",
                "100": "#fef9c3",
                "900": "#713f12",
                "400": "#facc15"
            },
            "red": {
                "200": "#fecaca",
                "50": "#fef2f2",
                "300": "#fca5a5",
                "800": "#991b1b",
                "500": "#ef4444",
                "100": "#fee2e2",
                "900": "#7f1d1d",
                "600": "#dc2626",
                "700": "#b91c1c",
                "DEFAULT": "#ef4444",
                "400": "#f87171"
            },
            "blue": {
                "800": "#1e40af",
                "900": "#1e3a8a",
                "DEFAULT": "#3b82f6",
                "100": "#dbeafe",
                "300": "#93c5fd",
                "400": "#60a5fa",
                "200": "#bfdbfe",
                "500": "#3b82f6",
                "700": "#1d4ed8",
                "50": "#eff6ff",
                "600": "#2563eb"
            },
            "secondary": {
                "900": "#33000b",
                "50": "#ffe6eb",
                "700": "#990022",
                "100": "#ffccd7",
                "DEFAULT": "#ff0039",
                "400": "#ff3361",
                "600": "#cc002e",
                "200": "#ff99b0",
                "800": "#660017",
                "500": "#ff0039",
                "300": "#ff6688"
            },
            "green": {
                "50": "#f0fdf4",
                "200": "#bbf7d0",
                "300": "#86efac",
                "800": "#166534",
                "500": "#22c55e",
                "600": "#16a34a",
                "DEFAULT": "#22c55e",
                "100": "#dcfce7",
                "700": "#15803d",
                "900": "#14532d",
                "400": "#4ade80"
            },
            "cyan": {
                "300": "#67e8f9",
                "400": "#22d3ee",
                "900": "#164e63",
                "200": "#a5f3fc",
                "100": "#cffafe",
                "700": "#0e7490",
                "DEFAULT": "#06b6d4",
                "800": "#155e75",
                "500": "#06b6d4",
                "600": "#0891b2",
                "50": "#ecfeff"
            },
            "zinc": {
                "50": "#fafafa",
                "100": "#f4f4f5",
                "900": "#18181b",
                "200": "#e4e4e7",
                "800": "#27272a",
                "DEFAULT": "#71717a",
                "300": "#d4d4d8",
                "500": "#71717a",
                "700": "#3f3f46",
                "400": "#a1a1aa",
                "600": "#52525b"
            },
            "inherit": {
                "50": "#e7e7e7",
                "300": "#a0a0a0",
                "800": "#2f2f2f",
                "400": "#8a8a8a",
                "DEFAULT": "#7f7f7f",
                "500": "#7f7f7f",
                "900": "#1b1b1b",
                "600": "#5b5b5b",
                "700": "#444444",
                "200": "#b7b7b7",
                "100": "#cfcfcf"
            },
            "orange": {
                "700": "#c2410c",
                "900": "#7c2d12",
                "600": "#ea580c",
                "100": "#ffedd5",
                "400": "#fb923c",
                "800": "#9a3412",
                "300": "#fdba74",
                "500": "#f97316",
                "200": "#fed7aa",
                "DEFAULT": "#f97316",
                "50": "#fff7ed"
            },
            "text": {
                "100": "#374151",
                "400": "#9ca3af",
                "600": "#e5e7eb",
                "500": "#d1d5db",
                "50": "#111827",
                "800": "#f9fafb",
                "300": "#6b7280",
                "900": "#ffffff",
                "200": "#4b5563",
                "DEFAULT": "#d1d5db",
                "700": "#f3f4f6"
            },
            "rose": {
                "300": "#fda4af",
                "800": "#9f1239",
                "900": "#881337",
                "200": "#fecdd3",
                "700": "#be123c",
                "DEFAULT": "#f43f5e",
                "50": "#fff1f2",
                "400": "#fb7185",
                "100": "#ffe4e6",
                "500": "#f43f5e",
                "600": "#e11d48"
            },
            "teal": {
                "100": "#ccfbf1",
                "300": "#5eead4",
                "800": "#115e59",
                "200": "#99f6e4",
                "700": "#0f766e",
                "600": "#0d9488",
                "400": "#2dd4bf",
                "500": "#14b8a6",
                "DEFAULT": "#14b8a6",
                "900": "#134e4a",
                "50": "#f0fdfa"
            },
            "transparent": {
                "700": "#444444",
                "600": "#5b5b5b",
                "500": "#7f7f7f",
                "200": "#b7b7b7",
                "100": "#cfcfcf",
                "DEFAULT": "#7f7f7f",
                "300": "#a0a0a0",
                "50": "#e7e7e7",
                "800": "#2f2f2f",
                "900": "#1b1b1b",
                "400": "#8a8a8a"
            },
            "slate": {
                "700": "#334155",
                "900": "#0f172a",
                "400": "#94a3b8",
                "DEFAULT": "#64748b",
                "50": "#f8fafc",
                "200": "#e2e8f0",
                "300": "#cbd5e1",
                "100": "#f1f5f9",
                "500": "#64748b",
                "600": "#475569",
                "800": "#1e293b"
            },
            "violet": {
                "900": "#4c1d95",
                "100": "#ede9fe",
                "400": "#a78bfa",
                "500": "#8b5cf6",
                "DEFAULT": "#8b5cf6",
                "600": "#7c3aed",
                "50": "#f5f3ff",
                "300": "#c4b5fd",
                "200": "#ddd6fe",
                "800": "#5b21b6",
                "700": "#6d28d9"
            },
            "neutral": {
                "900": "#171717",
                "100": "#f5f5f5",
                "300": "#d4d4d4",
                "800": "#262626",
                "600": "#525252",
                "50": "#fafafa",
                "500": "#737373",
                "400": "#a3a3a3",
                "700": "#404040",
                "DEFAULT": "#737373",
                "200": "#e5e5e5"
            },
            "fuchsia": {
                "800": "#86198f",
                "600": "#c026d3",
                "500": "#d946ef",
                "200": "#f5d0fe",
                "900": "#701a75",
                "50": "#fdf4ff",
                "100": "#fae8ff",
                "DEFAULT": "#d946ef",
                "300": "#f0abfc",
                "700": "#a21caf",
                "400": "#e879f9"
            },
            "white": {
                "500": "#ffffff",
                "900": "#2c2c2c",
                "400": "#ffffff",
                "DEFAULT": "#ffffff",
                "50": "#ffffff",
                "800": "#565656",
                "700": "#828282",
                "100": "#ffffff",
                "200": "#ffffff",
                "600": "#b2b2b2",
                "300": "#ffffff"
            },
            "current": {
                "DEFAULT": "#7f7f7f",
                "900": "#1b1b1b",
                "300": "#a0a0a0",
                "400": "#8a8a8a",
                "600": "#5b5b5b",
                "700": "#444444",
                "100": "#cfcfcf",
                "50": "#e7e7e7",
                "200": "#b7b7b7",
                "500": "#7f7f7f",
                "800": "#2f2f2f"
            },
            "surface": {
                "300": "#cfcfcf",
                "400": "#bfbfbf",
                "500": "#afafaf",
                "900": "#6f6f6f",
                "800": "#7f7f7f",
                "200": "#dfdfdf",
                "50": "#ffffff",
                "700": "#8f8f8f",
                "DEFAULT": "#afafaf",
                "100": "#efefef",
                "600": "#9f9f9f"
            },
            "emerald": {
                "800": "#065f46",
                "200": "#a7f3d0",
                "DEFAULT": "#10b981",
                "300": "#6ee7b7",
                "600": "#059669",
                "100": "#d1fae5",
                "500": "#10b981",
                "50": "#ecfdf5",
                "900": "#064e3b",
                "700": "#047857",
                "400": "#34d399"
            },
            "brand": {
                "50": "#fff0f0",
                "DEFAULT": "#ff2626",
                "800": "#af0505",
                "400": "#ff5959",
                "700": "#dc0000",
                "600": "#fc0606",
                "300": "#ff9595",
                "500": "#ff2626",
                "200": "#ffc1c1",
                "100": "#ffdddd",
                "900": "#900c0c"
            }
        },
        "fontFamily": {
            "quote": [
                "Georgia",
                "Cambria",
                "'Times New Roman'",
                "Times",
                "serif"
            ],
            "code": [
                "Menlo",
                "Monaco",
                "Consolas",
                "'Liberation Mono'",
                "'Courier New'",
                "monospace"
            ],
            "heading": [
                "Playfair Display"
            ],
            "body": [
                "Playfair Display"
            ]
        }
    }
}
```
