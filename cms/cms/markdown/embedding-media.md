---
description: Inline Images and Video using Markdown and the Typography Component
---

# Embedding Media

This document explains how to add **images** and **videos** to your Markdown files. These are particularly useful when writing long-form content such as blog posts, guides, or documentation.

When working with media, it’s important to note that **inline media embedding only works with the Typography Component**, not the Text Component. The Typography Component supports rich inline elements like images, videos, and code blocks, allowing your content to flow naturally with surrounding text.

### Images

You can include both **local** and **remote** images in your Markdown files using the standard Markdown syntax:

```markdown
![Image alt text](images/bot.jpg)
```

f you reference a local file, Elements CMS will automatically detect it and prefix the correct path to your project’s `resources` folder during publishing. This ensures that your image links always remain valid, both locally and when uploaded to your web host.

Remote images (hosted externally) can also be embedded by using a full URL:

```markdown
![Image alt text](https://example.com/path/to/image.jpg)
```

Images displayed within the Typography Component are automatically set to a **maximum width of 100%**, meaning they’ll scale down to fit smaller screens but will never be enlarged beyond their actual pixel size. This ensures your content remains sharp and visually consistent across all devices.

{% hint style="danger" %}
#### File Naming Best Practices

When working with local images, always use **lowercase filenames** and **avoid spaces or special characters**.&#x20;

Instead of `Images/My-Image.jpg` use all lowercase, like this: `images/my-image.jpg`.



Elements automatically converts filenames to lowercase and replaces spaces or non-standard characters with underscores to make them web-safe. For example:

* `my~file.png` would become `my_file.png`.
* `my file has spaces.png` would become `my_file_has_spaces.png`.
* `myFile.png` would become `myfile.png`.

Many web servers (Linux/Unix based) treat File.jpg and file.jpg as two different files. However, on Windows or macOS (i.e. Elements), the filesystem often isn’t case-sensitive, so it _looks_ fine locally, but when uploaded, it can cause broken links and 404 errors.

By using lowercase files, you’ll ensure they will ALWAYS work on different environments (Windows, Linux, macOS), this could be very important depending on the hosting platform you have chosen.
{% endhint %}

#### Using Inline CSS to style images (not recommend)

You can also use basic HTML and inline CSS to position or style images, though it’s generally best to avoid this unless absolutely necessary. If you do choose to use HTML, make sure you reference the full, correct path to your image files.

The following example **floats the image to the left** to allow text to wrap around it:

{% code overflow="wrap" %}
```html
<figure style="float: left; margin: 1em 1em 0 0; width: 40%;">
  <img src="/resources/blog/build-website-mac.jpg" alt="Album cover" style="width: 100%">
  <figcaption style="text-align: center; font-size: 0.9em; color: #555;">
    This is the image caption.
  </figcaption>
</figure>
```
{% endcode %}

### YouTube Videos

To embed a YouTube video, copy the embed code from the video’s “Share → Embed” option. It should look something like this:

{% code overflow="wrap" %}
```html
<iframe width="560" height="315" src="https://www.youtube.com/embed/zas7L3rMX18?si=k5fjpisqbHb8Ibgv" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
```
{% endcode %}

You can paste this HTML directly into your Markdown file. Elements CMS will render the video inline when displayed within the Typography Component.

If you’d like the video to **fill the width of the container**, remove the `width` and `height` attributes and use Tailwind utility classes on the parent component to make it responsive:

{% code overflow="wrap" %}
```html
<iframe src="https://www.youtube.com/embed/zas7L3rMX18?si=k5fjpisqbHb8Ibgv" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
```
{% endcode %}

Add the following classes to the component displaying your Markdown:

```css
[&_iframe]:w-full [&_iframe]:aspect-video
```

This ensures that the embedded video maintains a proper aspect ratio while scaling fluidly across screen sizes.

<figure><img src="../../../.gitbook/assets/CleanShot 2025-11-07 at 10 .49.35@2x.png" alt=""><figcaption></figcaption></figure>

### Common Issues

**Image not showing up?**\
Make sure the file exists in your project’s `resources` folder and that the path is correct. For example, if your resource file is in a `/blog/` folder, your image should be referenced as `blog/filename.jpg`.

**Video cut off or not scaling correctly?**\
Check that you’ve removed the fixed `width` and `height` attributes from the `<iframe>` and that your parent component includes the Tailwind classes: `[&_iframe]:w-full [&_iframe]:aspect-video`

**File path case mismatch**\
If you’re developing on macOS or Windows and everything works locally but breaks after upload, check for mismatched uppercase/lowercase letters in file names. Web servers treat `Image.jpg` and `image.jpg` as different files.
