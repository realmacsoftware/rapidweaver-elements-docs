---
description: Animate components when they enters the viewport
---

# Reveal

The “Reveal” animation component in Elements allows you to add visually engaging animations to your website. As elements come into view, they can “reveal” themselves with smooth, dynamic effects.

{% embed url="https://www.youtube.com/watch?v=7zZiIZtXf9c" %}

### Helpful Tip: Fixing Horizontal Scroll on iPhone

If your site appears to shift sideways or introduces unexpected horizontal scrolling on mobile (especially iPhone), the issue may be caused by a Reveal component pushing the layout beyond the viewport.

This often happens when an animation or hidden content expands outside the container, triggering a wider layout than expected.

Set the parent Container that wraps the Reveal component(s) to overflow-hidden. This will prevent the hidden/revealed content from extending beyond the bounds of the viewport.

**How to do it in Elements:**

1. Select the Container or Section that wraps the animated content.
2. In the Inspector, set Overflow to Hidden.

This tells the browser to clip any content that exceeds the container’s boundaries fixing the horizontal scroll issue on iOS.

