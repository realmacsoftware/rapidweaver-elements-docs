---
description: Learn how to report an issue and get effective support
icon: hand-heart
---

# Support Guide

If you encounter a bug or something doesn’t seem to be working correctly in Elements, we’d love to hear about it. You can check our [FAQ guide](../../elements-faq.md) for common questions, but the **best place to get support** is the [Elements Community Forum](https://forums.realmacsoftware.com/c/rapidweaver-elements/beta-feedback/57), where our team and other users can offer help and advice.

{% hint style="danger" %}
Make sure you [**search the forum first**](https://forums.realmacsoftware.com/). Your question or bug may already have been resolved.
{% endhint %}

### Download a Previous Version

To test if an Elements update is causing project issues, downgrade to a previous build via the [release notes page](https://realmacsoftware.com/rapidweaver/releasenotes/). This quickly reveals if the update is the problem or just a coincidence.

## How to Get Help Faster

We’ve seen quite a few posts on the [forum](https://forums.realmacsoftware.com/) where users ask for help without providing enough detail for anyone to solve the problem.

To save everyone time, here’s the **best way to** [**ask for help on the forum**](https://forums.realmacsoftware.com/)**:**

1. **Write a Clear Post Title**\
   Something like _“Need help styling the navigation component”_ works much better than _“Help. It’s broken!”_.
2. **Explain the Issue**\
   Tell us what you’re trying to do, what you expected, and what actually happened.
3. **Share Your Project**\
   Add an [Elements Cloud link](https://docs.realmacsoftware.com/elements-docs/getting-started/elements-cloud) so others can open your project and see what’s going on.
4. **Share a Live URL (if applicable)**\
   If the site is published, include the link. Sometimes issues only show up on a live site.
5. **Add Screenshots or Recordings**\
   A quick screenshot or short video can be a huge help.
6. **Be Specific**\
   The more detail you include, the quicker you’ll get accurate help.
7. **Do Not Post AI-generated Content**\
   AI-generated troubleshooting suggestions can sometimes be a bit off the mark. To help us diagnose things accurately, it’s best to stick to details from your own setup and what you’re seeing directly.

Following this guide will help you get better answers more quickly.

#### Why Details Matter

Asking for [help on the forum](https://forums.realmacsoftware.com/) without sharing the Elements project or live URL is like arriving at a garage and saying, _“My car’s making a funny noise. Can you fix it?”_ without showing the mechanic the actual car.

Sure, they could take a wild guess. They might suggest topping up the oil, tightening a belt, or just turning the radio up so you can’t hear it anymore. But without looking under the bonnet, they’re working blind.

That’s exactly what it’s like when asking for website help without sharing the details. We don’t need the keys, but we do usually need to see the engine.

### How to Report a Bug

When [posting on the forum](https://forums.realmacsoftware.com/c/rapidweaver-elements/beta-feedback/57), you should follow the guidelines below to help us locate and fix your issue much faster.

#### 1. Be as Detailed as Possible

Tell us exactly what you were doing when the issue occurred. The more information you can provide, the better. Try to include:

* What you expected to happen
* What actually happened
* Any error messages or unusual behaviour you noticed

#### 2. Provide Steps to Reproduce the Issue

If you can reliably trigger the problem, let us know how. Write down the exact steps you took leading up to the issue. This is incredibly helpful when we’re trying to track down bugs.

#### 3. Share Your Project via Elements Cloud

Please upload your project to your Elements Cloud account and share the link with us on the forum.

**This is one of the most reliable and fastest ways to get your issue fixed!**

#### 4. Include a Short Video or Screenshot

A video is often the quickest way to show what’s going wrong. You can use QuickTime Player.app (included with macOS) to record your screen.

To create a simple recording, **choose File › New Screen Recording** from the menu. Click the red record button, then follow the instructions on the screen. To save, choose **File › Export** and select the quality.

Alternatively, press Command-Shift-5 to open the onscreen recording controls.

Once you’ve made the recording, upload it to a cloud service like Dropbox or Google Drive, or share it via YouTube, and [post the link in your forum thread](https://forums.realmacsoftware.com/c/rapidweaver-elements/beta-feedback/57).

If you can’t share a video, screenshots can still be very helpful. **Try to capture the whole Elements window so we can see your workspace and any visible settings.** A partial screenshot is less useful because we need to see the full context.

Use the keyboard shortcut Command-Shift-3 to take a screenshot, or Command-Shift-4 to select just a portion of the screen.

***

### Custom HTML Issues

Sometimes using custom HTML on your page can be the source of the problem. Even small mistakes like a missing closing tag, an extra quotation mark, or incorrect nesting can cause layout or publishing errors. Because Elements is built on clean, structured code, any invalid or broken HTML you add manually can disrupt how components render or how the browser interprets the page.

This is often one of the hardest issues to track down, because errors in custom HTML don’t always show up where you expect them. A broken tag in one part of the page might affect the layout or functionality of a completely different section.

If you’re experiencing issues, it’s worth reviewing any custom HTML you’ve added. A good step is to remove it temporarily and check if the issue goes away. That way you’ll know whether the custom code is the root cause or if you should look elsewhere.

### Document Repaired Warning Dialog

If you see the Document Repaired warning when opening a project, don’t panic. **Your project is safe.**

When Elements detects orphaned nodes—content that no longer has a proper location—it moves them to the top of the page instead of deleting them. This prevents content from being lost accidentally.

These nodes can be safely removed using the built-in recovery option.

<figure><img src="../../.gitbook/assets/CleanShot 2025-09-30 at 6 .24.07@2x.png" alt="Elements Help menu with Recovery and Remove Recovered Nodes selected"><figcaption></figcaption></figure>

#### Repair Your Project

{% stepper %}
{% step %}
With the project open, choose **Help › Recovery › Remove Recovered Nodes**.
{% endstep %}

{% step %}
Choose **File › Save As…** to save your project as a new file.
{% endstep %}

{% step %}
Close the project and quit Elements.
{% endstep %}

{% step %}
Relaunch Elements and open the newly saved, repaired project.
{% endstep %}
{% endstepper %}

You can now continue working on your project, right where you left off.

We’re actively working on reducing the chances of these orphaned nodes appearing in the first place.
