---
icon: cabinet-filing
---

# Assets

Assets can be included per component or [shared in a component pack](../shared-files.md).

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

<figure><img src="../../.gitbook/assets/CleanShot 2024-12-01 at 3 .12.28@2x.png" alt=""><figcaption></figcaption></figure>

