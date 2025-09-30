---
description: Follow our guide on getting your issue resolved FAST!
icon: hand-heart
---

# Support Guide

If you run into a bug or something doesn’t seem to be working quite right in Elements, we’d love to hear about it.  You can check out our [FAQ guide](../elements-faq.md) for general support issues, but the **best place to get support** is on the [Elements Community Forum](https://forums.realmacsoftware.com/c/rapidweaver-elements/beta-feedback/57), where our team and other users can offer help and advice!

{% hint style="danger" %}
Make sure to [**search the forum first**](https://forums.realmacsoftware.com/), your question or bug might already have been resolved.
{% endhint %}

## How to Get Help (and get it faster)

To save everyone time, here’s the **best way to ask for help on the forum:**

1. **Create a Clear Post Title**\
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

#### Why Details Matter

Asking for help without sharing the Elements Project or live URL is a bit like rolling up to a garage and saying, _“My car’s making a funny noise, can you fix it?”_ but then not showing the mechanic the actually car.

Sure, they could take a wild guess. They might suggest topping up the oil, tightening a belt, or just turning the radio up so you can’t hear it anymore. But without looking under the bonnet, they’re working blind.

That’s exactly what it’s like when asking for website help without sharing the details. We don’t need the keys, but we do usually need to see the engine.

### How to get design help

If you’d like some design help with your Elements website, we’re more than happy to jump in. The best way to get feedback is to [post your request on the forum](https://forums.realmacsoftware.com/c/rapidweaver-elements/how-do-i/62) so the whole community can see it and share ideas.

When posting, **please include an Elements Cloud link to your project**. That way we can open it up directly in Elements and give you accurate, practical suggestions rather than guessing from a text description or partial screenshot.

The more context you can provide (what you’re aiming for, where you’re stuck, or examples of sites you like), the better the feedback you’ll get.

### How to report a bug

When [posting on the forum](https://forums.realmacsoftware.com/c/rapidweaver-elements/beta-feedback/57), you should follow the guidelines below to help us locate and fix your issue much faster.

#### 1. Be as detailed as possible:

Tell us exactly what you were doing when the issue occurred. The more information you can provide, the better. Try to include:

* What you expected to happen
* What actually happened
* Any error messages or unusual behavior you noticed

#### 2. Steps to reproduce the issue:

If you can reliably trigger the problem, let us know how. Write down the exact steps you took leading up to the issue. This is incredibly helpful when we’re trying to track down bugs.

#### 3. Share your Project via Elements Cloud (highly recommended!)

Please upload your project to your Elements Cloud account and share the link with us on the forum.&#x20;

**This is one of the most reliable and fastest ways to get your issue fixed!**

#### 4. Include a short video or screenshot:

A video is often the quickest way to show what’s going wrong. You can use QuickTime Player.app (included with macOS) to record your screen.

To create a simple recording, **choose File › New Screen Recording** from the menu. Click the red record button, then follow the instructions on the screen. To save, choose **File › Export** and select the quality.

Alternatively, you can use the keyboard shortcut command-shift-5 to bring up the onscreen Screen Recording controls.

Once you’ve made the recording, upload it to a cloud service like Dropbox or Google Drive, or share it via YouTube, and [post the link in your forum thread](https://forums.realmacsoftware.com/c/rapidweaver-elements/beta-feedback/57).

If you can’t share a video, screenshots can still be very helpful. **Try to capture the whole Elements window so we can see your workspace and any visible settings.** A partial screenshot is not very helpful, we need to see the entire context.

Use the keyboard shortcut Command-Shift-3 to take a screenshot, or Command-Shift-4 to select just a portion of the screen.

### Custom HTML Issues

Sometimes using custom HTML on your page can be the source of the problem. Even small mistakes like a missing closing tag, an extra quotation mark, or incorrect nesting can cause layout or publishing errors. Because Elements is built on clean, structured code, any invalid or broken HTML you add manually can disrupt how components render or how the browser interprets the page.

This is often one of the hardest issues to track down, because errors in custom HTML don’t always show up where you expect them. A broken tag in one part of the page might affect the layout or functionality of a completely different section.

If you’re experiencing issues, it’s worth reviewing any custom HTML you’ve added. A good step is to remove it temporarily and check if the issue goes away. That way you’ll know whether the custom code is the root cause or if you should look elsewhere.

### Document Repaired Warning Dialog

If you see the "Document Repaired Warning Dialog" dialog when opening a project, Don't panic! This is nothing to be alarmed about. **Your project(s) are safe.**

When Elements detects any orphaned nodes (bits of content that no longer have a proper home), it moves them to the top of the page rather than deleting them outright. That way, nothing important ever gets lost by mistake.

These nodes can be safely removed using the built-in recovery option.

<figure><img src="../.gitbook/assets/CleanShot 2025-09-30 at 6 .24.07@2x.png" alt=""><figcaption></figcaption></figure>

#### Follow these steps to Repair your Project:

{% stepper %}
{% step %}
With the project open, select the  `Help > Recovery > Remove Recovered Nodes` option.


{% endstep %}

{% step %}
Then, select the `File > Save As…` command to save your project as a new file.


{% endstep %}

{% step %}
Close the project and Quit Elements.


{% endstep %}

{% step %}
Re-launch Elements and open the newly saved (and repaired) project.


{% endstep %}
{% endstepper %}

You can now continue working on your project, right where you left off.

We’re actively working on reducing the chances of these orphaned nodes appearing in the first place.

### How to Reset Elements

To reset Elements, remove the preferences file by following these steps.

{% hint style="warning" %}
For an automatica way to remove the Preferences you can do the following. Hold down the option key and go to Help > Clear Applications Preferences.
{% endhint %}

{% stepper %}
{% step %}
#### Quit Elements

Ensure Elements is not running.
{% endstep %}

{% step %}
#### Locate Preferences File

In the finder press press “Command-Shift-G” to bring up the "Go To Folder" Window and paste in the following path:

{% code overflow="wrap" %}
```
~/Library/Containers/com.realmacsoftware.rapidweaverelements/Data/Library/Preferences/com.realmacsoftware.rapidweaverelements.plist
```
{% endcode %}
{% endstep %}

{% step %}
#### Delete Preferences Plist

Delete the file: `com.realmacsoftware.rapidweaverelements.plist`
{% endstep %}

{% step %}
#### Re-launch Elements

You can now safely re-launch Elements.
{% endstep %}
{% endstepper %}
