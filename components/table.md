---
description: Display structured data in rows and columns
---

# Table

The Table component allows you to present structured data in a clean, organised format using rows and columns. It renders a standard HTML table with full control over layout, styling, and content.

You can configure the number of columns and rows, toggle a header row, enable striped row backgrounds, and set per-column widths. Header and body cells have independent styling controls for text, padding, borders, and backgrounds, making it easy to create tables that match your design.

### Component Settings

#### Settings

The Settings section contains the core controls for defining the structure of your table.

**Columns**

Use the Columns collection to add, remove, and reorder the columns in your table. Each column can have an optional custom width.

*   **Width**

    Set the width of an individual column. Leave as auto to distribute space evenly, or enter a custom value to control the exact width.

{% hint style="info" %}
When any column has a custom width set, the table switches to a fixed layout so that column widths are respected exactly as defined.
{% endhint %}

**Table Settings**

*   **Rows**

    Set the number of body rows displayed in the table. The minimum value is 1 and the default is 3.



#### Header Cells

The Header Cells section controls the appearance of the table header row. These settings are only visible when the header is enabled.

*   **Show**

    Toggle the header row on or off. When disabled, the table will display only body rows.

**Padding**

Set the inner spacing for header cells. You can adjust the top, right, bottom, and left padding independently.

**Background**

Choose the background colour for the header row.

**Borders**

Customise the borders around each header cell.

*   **Style**

    Choose between Solid, Dashed, or Dotted border styles.
*   **Width**

    Set the border width on each side of the header cells independently.
*   **Color**

    Choose the border colour for header cells.



#### Header Text

The Header Text section controls the typography and appearance of text within header cells. These settings are only visible when the header is enabled.

*   **Alignment**

    Align header text to the Left, Center, Right, or Justify.
*   **Font**

    Choose a font family from your project's theme. The default is the heading font.
*   **Color**

    Set the text colour for header cells.
*   **Size**

    Choose a text size from your project's theme.
*   **Weight**

    Adjust the font weight from Thin (100) to Black (900). The default is Semi Bold (600).
*   **Spacing**

    Control the letter spacing. Options range from Tighter to Widest, with Normal as the default.



#### Body Cells

The Body Cells section controls the appearance of cells in the table body, including padding, backgrounds, and borders.

**Padding**

Set the inner spacing for body cells. You can adjust the top, right, bottom, and left padding independently.

**Background**

*   **Color**

    Set the background colour for body rows. By default this applies uniformly to all rows.
*   **Striped**

    Enable alternating row backgrounds for improved readability. When enabled, an additional colour picker appears for even rows.
*   **Even**

    Set the background colour for even-numbered rows. This setting is only visible when Striped is enabled.

{% hint style="success" %}
**Tip:** Striped rows make it easier for users to follow data across wide tables. Use subtle colour differences between odd and even rows for the best result.
{% endhint %}

**Borders**

*   **Width**

    Set the border width on each side of the body cells independently.
*   **Color**

    Choose the border colour for body cells.



#### Body Text

The Body Text section controls the typography and appearance of text within body cells.

*   **Alignment**

    Align body text to the Left, Center, Right, or Justify.
*   **Font**

    Choose a font family from your project's theme. The default is the body font.
*   **Color**

    Set the text colour for body cells.
*   **Size**

    Choose a text size from your project's theme.
*   **Weight**

    Adjust the font weight from Thin (100) to Black (900). The default is Normal (400).
*   **Spacing**

    Control the letter spacing. Options range from Tighter to Widest, with Normal as the default.

{% include "../.gitbook/includes/common-controls (1).md" %}
