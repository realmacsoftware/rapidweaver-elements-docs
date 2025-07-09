---
icon: box-taped
---

# Distribution

This section covers everything you need to know about preparing your components for release. Whether you’re sharing your work with clients or publishing it on the Marketplace, it’s essential to package and protect your components correctly. You’ll learn the difference between Dev Packs and Element Packs, how to compile and encrypt your components, and why only compiled Element Packs should ever be distributed.

### Element Dev Packs

Element Dev Packs are for internal use only. **Do not distribute or sell them.**

An Element Dev Pack (.devpack) is designed strictly for local development. These are uncompiled and unencrypted versions of your components that allow for live editing and testing during development.&#x20;

Every file inside a Dev Pack is actively monitored by Elements and the system, which enables real-time updates as you work in third-party editors, a huge benefit while building components.

However, this live monitoring comes at a cost. If too many Dev Packs accumulate over time, Elements (and macOS) can run out of file handles, leading to components failing to load or update. **To avoid performance issues and ensure system stability, Dev Packs must never be shared or sold.**

Before distribution, all Dev Packs must be compiled and encrypted into standard .elementpack files. This process protects your code, improves load times (down from seconds to milliseconds), and ensures the pack is safe and optimised for use by others.

### Element Packs

Compiled Element Packs are intended for distribution and sale.

An Element Pack is a compiled and encrypted version of your component. It contains only the essential files, optimised for performance and security. These packs are what you’ll use when sharing or selling your work via the Marketplace or elsewhere.

Information on converting your Dev Pack into a distributable Element Pack will be available soon.

***

I you need a help while developing your next great addon for Elements or you have questions about distribution, [Please visit the Support Form](https://forums.realmacsoftware.com/c/rapidweaver-elements/43).

