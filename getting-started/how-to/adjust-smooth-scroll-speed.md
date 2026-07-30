---
description: Set the scrolling Anchor speed using Smooth Scroll JS Library.
---

# Adjust Smooth Scroll Speed

If you want to control the scroll timing (and other options such as easing) when scrolling to an anchor  then you can use the [Smooth Scroll](https://github.com/cferdinandi/smooth-scroll) js library.

To add Smooth Scroll to yoru project, put the following in your project’s Template, just before the closing `</head>` tag.

```html
  <!-- Load the Smooth Scroll library -->
  <script src="https://cdn.jsdelivr.net/gh/cferdinandi/smooth-scroll@15/dist/smooth-scroll.polyfills.min.js"></script>

  <!-- Initialize Smooth Scroll -->
  <script>
    document.addEventListener('DOMContentLoaded', function () {
      var scroll = new SmoothScroll('a[href*="#"]', {
        speed: 1000
      });
    });
  </script>
```

Note the **speed** option in the docs say this:

> \[speed] is a number representing the amount of time in milliseconds that it should take to scroll 1000px. Scroll distances shorter than that will take less time, and scroll distances longer than that will take more time. The default is 300ms.

<figure><img src="../../.gitbook/assets/CleanShot 2024-11-27 at 10 .46.50@2x.png" alt="Smooth Scroll JavaScript added to the site template editor"><figcaption></figcaption></figure>
