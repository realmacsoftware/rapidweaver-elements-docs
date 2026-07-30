---
description: Display, search, sort, and paginate structured data
---

# Table

The Table component presents structured data in rows and columns. Data can be entered manually, loaded from a CSV resource, or fetched from a CSV or Google Sheets URL. Tables can include headers, footers, sorting, search, pagination, striped rows, and custom cell content.

### Requirements

{% hint style="warning" %}
Pages containing the Table component must be published as PHP.
{% endhint %}

Remote CSV data must be publicly accessible to the published site.

### Supported Content and File Types

* Manual columns and rows
* CSV files stored in Resources
* Public CSV URLs
* Published Google Sheets data

### How to Use Table

You’ll find Table under **Content** in the Components list.

1. Drag **Table** onto the page.
2. Choose Manual, CSV File, or CSV URL.
3. Add and configure the Columns collection.
4. For Manual data, set the row count and edit the cells.
5. Optionally enable sorting, search, pagination, header, and footer.
6. Style cells, text, search, and pagination, then test the published PHP page.

### Component Settings

#### Settings

**Data Source**

* **Manual** — Uses editable cells and a Rows setting. This is the default.
* **CSV File** — Loads a CSV resource.
* **CSV URL** — Loads a public CSV or Google Sheets URL.

CSV File reveals **CSV File**. CSV URL reveals **CSV URL**.

For CSV sources, **First Row is Header** is enabled by default. The Columns collection maps to CSV columns by position.

For Manual data, **Rows** sets the number of body rows and defaults to 3.

**Columns Collection**

Each column provides:

* **Cell Mode** — Text or Dropzone for Manual data. Text is the default.
* **Width** — Defaults to Auto.
* **Alignment** — Default, Left, Centre, or Right.
* **Sortable** — Enables sorting for that column and is off by default.
* **Hidden** — Hides the column and is off by default.
* **Classes** and **ID** — Advanced values for the column.

#### Interactive

Sorting is enabled per column in the Columns collection.

**Search** is off by default. Enabling it reveals **Placeholder**, which defaults to “Search…”.

**Pagination** is off by default. Enabling it reveals **Rows Per Page**, which defaults to 10.

#### Header Cells

**Show** is enabled by default.

**Padding** defaults to theme spacing 2 on every side. **Align** offers Top, Middle, or Bottom and defaults to Top. **Background** defaults to Surface 50.

Borders provide Solid, Dashed, or Dotted Style, plus Width and Color. Style defaults to Solid and Color to Surface 200.

#### Header Text

Set Alignment, Font, Color, Size, Weight, and Spacing. Defaults include Heading font, Text 50, Base size, and weight 600.

#### Body Cells

Padding defaults to theme spacing 2 and vertical Align to Top.

**Background**

* **Color** — Sets the base row colour and defaults to Surface 50.
* **Striped** — Enables alternating rows and is off by default.
* **Even** — Appears for striped rows and defaults to Surface 100.

**Hover** is off by default. Enabling it reveals Hover Color, which defaults to Surface 200.

Body borders provide Style, Width, and Color. Style defaults to Solid and Color to Surface 200.

#### Body Text

Set Alignment, Font, Color, Size, Weight, and Spacing. Defaults include Body font, Text 50, Base size, and weight 400.

#### Footer Cells and Footer Text

**Show Footer** is off by default. When enabled, Footer Cells provide Padding, Align, Background, and border controls. Defaults include theme spacing 2, Top alignment, Surface 100 background, Solid borders, and Surface 200 border colour.

Footer Text provides Alignment, Font, Color, Size, Weight, and Spacing. Defaults include Body font, Text 50, Base size, and weight 600.

#### Search Bar

Set Padding, Margin Bottom, Font, Text Color, Size, Placeholder Color, Background, border Style, Width, Color, and Radius.

Defaults include padding 2 vertically and 3 horizontally, margin 4, Body font, Text 50, Base size, Text 300 placeholder, Surface 50 background, Solid border, Surface 200 border colour, and Medium radius.

#### Pagination Bar

**Margin Top** defaults to theme spacing 4.

**Alignment** offers Between, Centre, or End and defaults to Between.

Button controls set Font, Size, Text Color, and Disabled Color. Defaults are Body, Small, Text 50, and Text 300.

### Accessibility

Use a header row for column names and keep labels concise. Do not hide information required to understand the data. Check search, sorting, pagination, and Dropzone controls with a keyboard.

### Troubleshooting

#### Remote data does not load

Confirm that the page is PHP, the CSV URL is public, and the server can reach it. For Google Sheets, use a published CSV-compatible URL rather than an editor-only link.

#### CSV columns are mismatched

Reorder the Columns collection so its first item maps to the first CSV column, the second item to the second column, and so on.

### Related Components

* [Grid](grid.md) — Builds visual card layouts rather than semantic tabular data.
* [Filter](filter.md) — Filters tagged components outside a Table.

{% include "../../.gitbook/includes/common-controls.md" %}
