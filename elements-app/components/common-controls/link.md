---
description: Link to a page, resource or website.
---

# Link

The link property allows you to link to a page, resource or extrenal website. Elements will keep track and update all internally linked pages and resources.

{% embed url="https://youtu.be/mt-5Zhk3M7E" %}

### Link Panel

You can envoke the link panel on most components and inline text areas. Add a link click the "Choose Link…" button in the inspector. To clear a link click the "x" icon to the right hand side of the link button.

<table><thead><tr><th width="136">Link Types</th><th>Description</th></tr></thead><tbody><tr><td>URL</td><td>Link to an external website, a mailto link will automatically be created if an email address is entered.</td></tr><tr><td>Page</td><td>Link to a  page within your project.</td></tr><tr><td>Anchor</td><td>Link to an Anchor on the page. Anchor ID's can be set in the Advanced settings on all built-in Components.</td></tr><tr><td>Resource</td><td>Link to a  resource within your project.</td></tr></tbody></table>

{% hint style="info" %}
#### Disabling Smooth Scroll for Anchors

Element websites are configured to smooth scroll when navigating to an anchor. Smooth scroll can be disabled by removing the class="scroll-smooth" on the html tag in the site Template code.
{% endhint %}

### Custom Attributes

Custom attributes in an link (anchor tag) provide additional information about how the link behaves, where it directs, and how it interacts with other elements or the browser. Here's a selection of example custom attributes.

<table><thead><tr><th width="106">Name</th><th width="210">Value</th><th>Description</th></tr></thead><tbody><tr><td>title</td><td>Go to Example Website</td><td>Provides additional information about the link, usually displayed as a tooltip when the user hovers over the link.</td></tr><tr><td>rel</td><td>noreferrer</td><td>Ensures that no referrer information (the URL of the current page) is sent to the destination.</td></tr><tr><td>rel</td><td>nofollow</td><td>Tells search engines not to follow this link for SEO purposes.</td></tr><tr><td>type</td><td>application/pdf</td><td>Specifies the MIME type of the linked resource. This is typically used when linking to downloadable files or specific content types. This example is for a pdf document.</td></tr></tbody></table>

### Linking to an Anchor

1. You first need to add an ID to the component that will serve as your anchor. The ID can be found in the Advanced section in the settings for the selected component.
2. Then where you want to create your link in the text. Select the text, which will display the inline text&#x20;
   * Click the LINK button in the inline text editor to open the link dialog.
   * If your anchor is on the same page, choose the page from the dropdown next to the link field.
   * This will display all available anchors in the Anchor popup.
   * Select the desired anchor, and you're done.

{% embed url="https://youtu.be/VEqrlcXydTs" %}



