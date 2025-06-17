---
icon: cabinet-filing
---

# Assets

Assets can be included per component or [shared in a component pack](shared-files/). Assets are additional files that should be deployed when a project is published. They are not processed in any way and are simply copied during publish.

### Directory structure

All assets should be placed inside a directory named page and will be deployed once to the page's files directory during publish. Here's an example showing where to place the snowstorm.js file.

```
components
    com.domain.weatherpack.snowmachine
        assets
            page
                snowstorm.js
```

{% hint style="info" %}
Currently, page is the only area currently supported. If you need to deploy assets to another area, please visit the [forum and let us know](https://forums.realmacsoftware.com/c/rapidweaver-elements/developer/).&#x20;
{% endhint %}

### Usage

To link to an asset in a single component you'll need to do the following;

1. Use the \{{assetPath\}} macro inside of the index.html Template file. If you need the include to appear in the head (or other areas) of the page you can [use the Portal Function](templates/portal.md).

<pre><code>@portal(headEnd)
<strong>    &#x3C;script src="{{assetPath}}/snowstorm.js">&#x3C;/script>
</strong>@endportal
</code></pre>

2. Include the following code in the [hooks.js](hooks.js/) to return the assetPath to the page template:

```
const transformHook = (rw) => {

	// Extract the slider property
	const { assetPath } = rw.component;
	
	// Set slider and message properties in our template data
	rw.setProps({
		assetPath
	});
}

exports.transformHook = transformHook;
```

<figure><img src="../../../.gitbook/assets/CleanShot 2024-12-01 at 3 .12.28@2x.png" alt=""><figcaption></figcaption></figure>

