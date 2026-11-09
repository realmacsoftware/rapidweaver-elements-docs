---
description: Display page numbers to navigate through multiple pages inside of Collections.
---

# Collection Pagination

The Collection Pagination component is used to display page numbers that allow visitors to navigate through multiple pages of items within a CMS Collection. It automatically connects to the parent Collection and updates dynamically as content is added or removed.

**The Collection Pagination and** [**Load More**](load-more.md) **components cannot be used together.** They both control how items are fetched and displayed within a Collection, so enabling both at the same time will cause conflicts. Choose Pagination if you want clear page-based navigation, or Load More if you prefer a progressive, infinite-style experience.

<figure><img src="../../../.gitbook/assets/CleanShot 2025-11-01 at 4 .55.17@2x.png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
**Important:** The Pagination component must be placed inside a Collection component to function. It’s recommended to position it at the bottom of the Collection layout in the "After" area, below the repeating items.
{% endhint %}

{% columns %}
{% column %}
#### Collection Pagination

**Settings**\
These controls let you adjust the appearance and behaviour of the pagination.

*   **Page Range**

    Defines how many page numbers are visible at once. For example, setting this to 2 will display two page numbers before and after the current page.
*   **Show First/Last**

    Toggles whether to display quick links to the first and last pages of the Collection.

You can customise the look of the pagination to match your site’s design.

*   **State**

    Style the Default and Hover states separately to give visual feedback as users interact with the pagination links.
*   **Background / Text**

    Adjust colours for the pagination buttons and text to match your theme.
*   **Spacing**

    Fine-tune the Gap between page numbers and add Padding inside each button for balance and clarity.
*   **Text**

    Choose a Font and Size to match the rest of your sites typography.
*   **Borders**

    Adjust the Style, Radius, and Width to create rounded, outlined, or minimal pagination buttons.
{% endcolumn %}

{% column %}
<figure><img src="../../../.gitbook/assets/CleanShot 2025-11-01 at 4 .50.52@2x.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}
