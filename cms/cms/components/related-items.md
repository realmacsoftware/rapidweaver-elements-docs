---
description: Displays content that’s similar or connected to the current CMS item
---

# Related Items

The Related Items component automatically displays content that’s similar or connected to the current CMS item. It’s ideal for blog posts, articles, or products where you want to show visitors additional relevant content without manual linking.

{% hint style="success" %}
The **Related Items Component** must be placed inside the **Items Component**. It won’t display content when used outside of the CMS context.
{% endhint %}

### Component Settings



{% columns %}
{% column width="50%" %}
#### Settings

These controls define how related content is found and how many items are displayed.

*   **By Tags**

    When enabled, the component will show items that share one or more tags with the current item.
*   **By Author**

    When enabled, it will include items written by the same author as the current item.
*   **Limit**

    Sets the maximum number of related items to display. Adjust this value to control how many results appear in the layout.

{% hint style="warning" %}
When both options are selected, the component only displays posts that match **both** the same tags **and** the same author.
{% endhint %}
{% endcolumn %}

{% column width="50%" %}
<figure><img src="../../../.gitbook/assets/CleanShot 2025-11-06 at 09.50.53@2x.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}
