---
description: Link a component to a page, resource, anchor, email address, or website
---

# Link

The Link control makes a supported component clickable. Elements tracks internal pages, anchors, and resources so their published destinations stay current when the project changes.

{% embed url="https://youtu.be/mt-5Zhk3M7E" %}

### Link Panel

Choose **To** or **Choose Link…** to open the Link panel. An unset link is the default. Use the Clear button to remove an existing destination.

{% columns %}
{% column width="50%" %}
Available link types include:

* **URL** — Links to an external URL. Entering an email address creates a `mailto:` link.
* **Plain** — Uses the entered destination without Elements resolving it; useful for specialised or generated URLs.
* **Page** — Links to a page in the project.
* **Anchor** — Links to a component ID on a selected page.
* **Resource** — Links to a file stored in Resources.
{% endcolumn %}

{% column width="50%" %}
<figure><img src="../../../.gitbook/assets/CleanShot 2025-11-01 at 4 .16.10@2x.png" alt="The Elements Link panel with destination options"><figcaption><p>The Link panel selects and manages destinations.</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

### Email Links

Entering an email address creates a `mailto:` destination. Test it in a browser because the visitor must have an email application configured.

### Custom Attributes

Where the Link panel provides Custom Attributes, add a Name and Value for attributes such as:

| Name | Example value | Purpose |
| --- | --- | --- |
| `title` | `Go to Example Website` | Supplies additional advisory text. |
| `rel` | `noreferrer` | Prevents the destination receiving referrer information. |
| `rel` | `nofollow` | Asks search engines not to follow the link. |
| `type` | `application/pdf` | Identifies the linked resource’s MIME type. |

Use one `rel` attribute with space-separated values when more than one relationship is required, for example `nofollow noreferrer`.

### Linking to an Anchor

1. Select the destination component.
2. Enter a unique value under **Advanced → ID**.
3. Open the Link panel on the source component or selected inline text.
4. Choose the destination page.
5. Choose the component ID from the Anchor list.

On the same page, the published destination uses a fragment such as `#about-section`.

{% embed url="https://youtu.be/VEqrlcXydTs" %}

{% hint style="warning" %}
Elements sites use smooth anchor scrolling by default. To disable it site-wide, remove `class="scroll-smooth"` from the `html` tag in the site Template code.
{% endhint %}

### Accessibility

Use link text that describes the destination. Avoid making a Container clickable when it contains Buttons, links, form fields, or other interactive controls.
