---
description: Add a configurable Google map to a page
---

# Map (Free)

{% hint style="success" %}
Map is available as a **free download via the Elements Store**. Install the current version of Elements before adding it to a project.
{% endhint %}

Map embeds a Google map for a street address or a pair of coordinates. You can choose the map style, zoom level, height, and which visitor controls are available.

The component requires a Google Maps Platform API key. The key is added to the page in the browser, so it should be restricted to your websites and to the APIs the component needs.

<a href="elementsapp://storeProduct/com.elementsplatform.mappack" class="button primary" data-icon="store">Get Map</a>

{% embed url="https://youtu.be/hsNlz7-abd0?si=GdUJB8TqHNtGwXkm" %}

### Features

* **Address or coordinates** — Centre the map using a postal address or latitude and longitude.
* **Four map types** — Choose Roadmap, Satellite, Hybrid, or Terrain.
* **Responsive height** — Size the map with theme spacing controls.
* **Adjustable zoom** — Set the initial zoom from 1 to 20.
* **Optional visitor controls** — Enable or disable Zoom, Map Type, Street View, and Fullscreen controls.

### Requirements

Before using Map, make sure you have:

* The Map pack installed from the Elements Store.
* A Google Cloud project and Google Maps Platform API key.
* Maps JavaScript API enabled.
* Geocoding API enabled when using a street address.
* Website referrer restrictions that include both your published domain and any local preview address you use.

{% hint style="warning" %}
Google controls account, billing, quota, and usage requirements for Maps Platform. Restrict your API key before publishing and review the current terms in your Google Cloud account.
{% endhint %}

### Supported Content and File Types

Map supports:

* Street addresses.
* Coordinates in `latitude, longitude` format.
* Roadmap, Satellite, Hybrid, and Terrain views.

### How to Use Map

You’ll find Map under **Media** in the Components list.

1. Create or select a project in the [Google Cloud Console](https://console.cloud.google.com/).
2. Enable Maps JavaScript API and, for street addresses, Geocoding API.
3. Create an API key and restrict it to your websites and the required APIs.
4. Drag **Map** onto the page and paste the key into **API Key**.
5. Choose Street Address or Coordinates and enter the location.
6. Set the map type, zoom, height, and available controls.
7. Preview locally and test the published site.

### Create and Configure the Google Maps API Key

#### 1. Create or select a Google Cloud project

Sign in to the [Google Cloud Console](https://console.cloud.google.com/), open the project selector, and create a project if you do not already have one for the site.

#### 2. Enable the required APIs

1. Open **APIs & Services**.
2. Choose **Enable APIs and Services**.
3. Find and enable **Maps JavaScript API**.
4. Find and enable **Geocoding API** if the component will use a street address.

<figure><img src="../../.gitbook/assets/enable-maps-javascript-api-and-geocoding-api.png" alt="Google Cloud API Library showing Maps JavaScript API and Geocoding API enabled"><figcaption><p>Enable Maps JavaScript API and Geocoding API for address-based maps.</p></figcaption></figure>

#### 3. Create and restrict the key

1. Open **APIs & Services → Credentials**.
2. Choose **Create Credentials → API key**.
3. Open the new key and set **Application restrictions** to **Websites**.
4. Add your live domains as HTTP referrers.
5. Under **API restrictions**, limit the key to Maps JavaScript API and Geocoding API when used.
6. Save the changes.

For a site at `www.mydomain.com`, add both:

`https://www.mydomain.com/`

`https://www.mydomain.com/*`

#### 4. Allow local preview

Set a fixed preview port in Elements so the local address does not keep changing.

<figure><img src="../../.gitbook/assets/CleanShot 2025-11-13 at 8 .25.51@2x.png" alt="Advanced Project Settings with a fixed local web server port highlighted"><figcaption><p>A fixed preview port gives you a stable local referrer.</p></figcaption></figure>

Add the preview address and its wildcard form to the key. For example:

`http://127.0.0.1:61109/`

`http://127.0.0.1:61109/*`

<figure><img src="../../.gitbook/assets/google-maps-api-key-credentials-settings.png" alt="Google Maps API key settings with website and API restrictions configured"><figcaption><p>Example website and API restrictions for a Google Maps key.</p></figcaption></figure>

### Component Settings

#### Map Settings

**API Key**

Paste the restricted Google Maps Platform API key.

**Type**

* **Street Address** — Enter a complete address. This is the default and requires Geocoding API.
* **Coordinates** — Enter latitude followed by longitude, separated by a comma, such as `37.33182, -122.03118`.

**Map Type**

* **Roadmap** — Standard road and place view. This is the default.
* **Satellite** — Satellite imagery.
* **Hybrid** — Satellite imagery with roads and labels.
* **Terrain** — Physical terrain and elevation details.

**Zoom Level**

Sets the initial zoom from 1 to 20. The default is 15. Lower values show a wider area.

**Height**

Sets the responsive height using the theme spacing scale. The default is 96.

#### Map Controls

Enable or disable the controls visitors can use:

* **Zoom** — Shows zoom buttons.
* **Map Type** — Lets visitors switch map views.
* **Street View** — Provides access to Street View where Google supports it.
* **Fullscreen** — Lets the map fill the screen.

All four controls are enabled by default.

#### Advanced

Use **Classes** to add custom CSS classes and **ID** to assign a unique HTML identifier.

### Accessibility

* Include the address and a normal text link to directions near the map. Do not make the map the only way to find the location.
* Keep useful controls enabled and test keyboard navigation in the published map.
* Give the surrounding section a clear heading so visitors understand what the map represents.
* Check that the component’s height leaves enough room for controls and labels at small breakpoints.

### Tips and Best Practices

* **Prefer coordinates for exact placement:** They avoid ambiguity when an address covers a large site or is formatted differently by region.
* **Restrict the key twice:** Apply both website referrer and API restrictions.
* **Use separate keys when appropriate:** Development and production keys can have different referrer lists and quotas.
* **Test the live domain:** A key that works locally can still fail after publishing if the live referrer is missing.

### Troubleshooting

#### The map says it cannot load correctly

Check that the API key is valid, Maps JavaScript API is enabled, the Google Cloud project is active, and the current domain matches an allowed website referrer.

#### A street address does not resolve

Enable Geocoding API, confirm the key is allowed to use it, and enter a complete address. Alternatively, switch Type to Coordinates.

#### The map works after publishing but not in preview

Set a fixed preview port in Elements and add both the local address and wildcard address to the key’s website restrictions.

#### The map works in preview but not on the live site

Add the published domain to the allowed referrers, including the correct `http` or `https` scheme and any `www` variant used by the site.

### Related Components

* [Container](../components/container.md) — Place the map inside a structured location or contact section.
* [Text](../components/text.md) — Add an accessible address, opening details, and directions link alongside the map.

{% include "../../.gitbook/includes/common-controls.md" %}
