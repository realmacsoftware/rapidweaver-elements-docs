---
description: How to make a sticky menu and change it's visual properties on scroll
---

# Build a Sticky Menu

To make a menu sticky, you need to put the menu and all contents in a container (site wrapper) along with making the following changes to the menu settings:

Layout > Position set to Sticky.

Layout > Z-Index > Custom set to 100.

Layout > Type > Uniform > Inset 0.

Watch the following tutorial to see how to build a Sticky Menu, along with adding a drop shadow and frosted glass effect.

{% embed url="https://youtu.be/E7lQCiPmuQo" %}

## Advanced Sticky Menu Tutorial - Part 2

In this advanced tutorial we use some Javascript to adjust the look of the menu when the user scrolls down the page.&#x20;

You can [click here to open the Space Demo Project](elementsapp://downloadDocument/sDsH9PgNy9uG) in Elements.

{% embed url="https://youtu.be/Wv7J6BpHoEA" %}

### Code Examples

Adding and Removing Standard CSS Classes:

```javascript
<script>
	const menu = document.getElementById('fancymenu');
	window.addEventListener('scroll', () => {
	  if (window.scrollY > 800) {
		menu.style.setProperty("width", "100%");
		menu.style.setProperty("height", "80px");
		menu.style.setProperty("margin-top", "0");
		menu.style.setProperty("background", "#ffffff");
	  } else {
		menu.style.removeProperty("width");
		menu.style.removeProperty("height");
		menu.style.removeProperty("margin-top");
		menu.style.removeProperty("background");
	  }
	});
</script>
```

Adding and Removing Tailwind Classes:

```javascript

	<script>
	const menu = document.getElementById('fancymenu');
	window.addEventListener('scroll', () => {
	  if (window.scrollY > 500) {
		menu.classList.add('w-auto');
		menu.classList.remove('w-[1000px]', 'mt-10');
	  } else {
		menu.classList.add('w-[1000px]', 'mt-10');
		menu.classList.remove('w-auto');
	  }
	});
 </script>
```

