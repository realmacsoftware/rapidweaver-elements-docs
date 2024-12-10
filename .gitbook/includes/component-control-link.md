---
title: 'Component Control: Link'
---

<details>

<summary>Link</summary>

You can invoke the link panel on most components and inline text areas. Add a link click the "Choose Link…" button in the inspector. To clear a link click the "x" icon to the right hand side of the link button.







</details>

<table><thead><tr><th width="136">Link Types</th><th>Description</th></tr></thead><tbody><tr><td>URL</td><td>Link to an external website, a mailto link will automatically be created if an email address is entered.</td></tr><tr><td>Page</td><td>Link to a  page within your project.</td></tr><tr><td>Anchor</td><td>Link to an Anchor on the page. Anchor ID's can be set in the Advanced settings on all built-in Components.</td></tr><tr><td>Resource</td><td>Link to a  resource within your project.</td></tr></tbody></table>



## Link

The link property allows you to link to a page, resource or extrenal website. Elements will keep track and update all internally linked pages and resources.

## Link Panel

{% hint style="info" %}
### Disabling Smooth Scroll for Anchors

Element websites are configured to smooth scroll when navigating to an anchor. Smooth scroll can be disabled by removing the class="scroll-smooth" on the html tag in the site Template code.
{% endhint %}

## Custom Attributes

Custom attributes in an link (anchor tag) provide additional information about how the link behaves, where it directs, and how it interacts with other elements or the browser. Here's a selection of example custom attributes.

<table><thead><tr><th width="106">Name</th><th width="210">Value</th><th>Description</th></tr></thead><tbody><tr><td>title</td><td>Go to Example Website</td><td>Provides additional information about the link, usually displayed as a tooltip when the user hovers over the link.</td></tr><tr><td>rel</td><td>noreferrer</td><td>Ensures that no referrer information (the URL of the current page) is sent to the destination.</td></tr><tr><td>rel</td><td>nofollow</td><td>Tells search engines not to follow this link for SEO purposes.</td></tr><tr><td>type</td><td>application/pdf</td><td>Specifies the MIME type of the linked resource. This is typically used when linking to downloadable files or specific content types. This example is for a pdf document.</td></tr></tbody></table>

# Link UI in Elements

<figure><img src="../assets/CleanShot 2024-10-19 at 9 .21.00@2x.png" alt=""><figcaption><p>RapidWeaver Elements Component Link</p></figcaption></figure>

<figure><img src="../assets/CleanShot 2024-10-19 at 9 .07.39@2x.png" alt=""><figcaption><p>RapidWeaver Elements Link Panel</p></figcaption></figure>
