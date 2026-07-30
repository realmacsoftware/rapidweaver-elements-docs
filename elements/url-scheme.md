---
description: Open projects, resources and developer packs with Elements URL schemes
icon: link-horizontal
---

# Deep Linking

Deep linking is a way to open a specific screen, action, or workflow inside Elements. Instead of just launching the app, the link takes the user straight to the right place and can often pass data along with it.

In app terms, deep links can make setup faster and reduce friction. They are commonly used for onboarding, authentication, importing data, or opening a precise feature without making the user navigate there manually.

In **Elements**, deep linking uses the `elementsapp://` URL scheme. This lets a link trigger specific actions inside the app, such as importing a custom component or creating a publishing destination with predefined settings. In practice, that means one link can open Elements, jump to the right task, and automate part of the setup process.

### Import Custom Component

You can use the following URL scheme to import/create custom components.

**URL Format:**

```
elementsapp://import-custom-component/
```

Consider URL-safe base64 (replacing + with -, / with \_, stripping = padding) to avoid path encoding issues. Alternatively, use a query parameter: elementsapp://import-custom-component?data=.

**Payload Format:**

The base64 string decodes to UTF-8 plain text with two sections identified by header keywords on their own line:

```
TITLE
A profile card

HTML
<div class="profile-card">
  <img src="{{avatar}}" alt="{{name}}" />
  <h2>{{name}}</h2>
  <p>{{bio}}</p>
</div>
```

**Options:**

* TITLE header line followed by the component title on the next non-empty line.
* HTML header line followed by all remaining content (the template HTML).
* Whitespace-only lines between sections are ignored.
* If TITLE is missing or empty, default to "Custom Element".

**Requirements:**

Import Custom Components requires RapidWeaver Elements 2.1.1 or newer on macOS.

### Create Publishing Destination

Magic publishing links provide a quick way to configure a publishing destination within an Elements project. Most settings can be included in the link, reducing user error and making setup a simple one-click process.

To create a magic link, use the `elementsapp://` url scheme with `createPublishingDestination` followed by query parameters for the settings.

**URL format:**

```
elementsapp://createPublishingDestination?[options]
```

**Payload example:**

{% code fullWidth="false" %}
```
elementsapp://createPublishingDestination?name=Chillidog%20Hosting&method=SFTP&server=123.123.123.123:8080&path=/my/cool/site&username=my-user-name&website=https://www.magic.com
```
{% endcode %}

**Options:**\
The available options are as follows

* method: SFTP, FTP, FTPS
* server: IP address or url of server, including the port
* path: Publishing path
* username: Username
* website: Website address of published content

Please note that Password is not supported for security reasons.

### Store Product Link <a href="#deep-linking-to-element-products" id="deep-linking-to-element-products"></a>

Elements supports deep linking to products within its built-in Store, allowing you to send users directly to a specific product page inside RapidWeaver Elements. This makes it easy to connect marketing websites, documentation, onboarding flows, emails, or companion apps straight to the exact pack you want to showcase, without requiring users to manually search the Store.

When a deep link is triggered, Elements opens and navigates directly to the relevant product, creating a fast and seamless experience. This is especially useful for upgrade prompts, cross-promotion between packs, launch announcements, and partner integrations where precision and convenience matter.

Deep linking helps reduce friction, improves conversion, and ensures your customers land exactly where you intend inside the Elements ecosystem.

**Requirements:**

Store links require RapidWeaver Elements 2.0 or newer on macOS.

To link to the Elements Store, use: `elementsapp://storeProduct/`. To link to your product, append the reverse domain name from your `info.json` file in your devpack.

For example, consider this `info.json` for the Essentials pack:

```
{
  "author": "Elements Platform",
  "identifier": "com.elementsplatform.essentials",
  "version": 1,
  "build": 1
}
```

Take the `identifier` value: `com.elementsplatform.essentials`, and append it to the store link: `elementsapp://storeProduct/com.elementsplatform.essentials`.

**Link Example:**

👉 [View Essentials Pack in the Elements Store](elementsapp://storeProduct/com.elementsplatform.essentials) (Elements Required)
