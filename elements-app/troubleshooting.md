---
description: Learn more about reporting and fixing issues.
icon: face-scream
---

# Troubleshooting

## Reporting an Issue

If you run into a bug or something doesn’t seem to be working quite right in Elements, we’d love to hear about it.  The best place to report issues is on the [Elements Community Forum](https://forums.realmacsoftware.com/c/rapidweaver-elements/beta-feedback/57), where our team and other users can offer help and advice. Make sure to search the forum first—your question or bug might already have been resolved.

By following the guidelines below, you’ll help us locate and fix the issue much faster:

#### Be as detailed as possible

Tell us exactly what you were doing when the issue occurred. The more information you can provide, the better. Try to include:

* What you expected to happen
* What actually happened
* Any error messages or unusual behavior you noticed

#### Steps to reproduce the issue

If you can reliably trigger the problem, let us know how. Write down the exact steps you took leading up to the issue. This is incredibly helpful when we’re trying to track down bugs.

#### Video recordings (highly recommended!)

A video is often the quickest way to show what’s going wrong. You can use QuickTime Player.app (included with macOS) to record your screen.

To create a simple recording, **choose File › New Screen Recording** from the menu. Click the red record button, then follow the instructions on the screen. To save, choose **File › Export** and select the quality.

Alternatively, you can use the keyboard shortcut command-shift-5 to bring up the onscreen Screen Recording controls.

Once you’ve made the recording, upload it to a cloud service like Dropbox or Google Drive, or share it via YouTube, and [post the link in your forum thread](https://forums.realmacsoftware.com/c/rapidweaver-elements/beta-feedback/57).

#### Screenshots (if video isn’t possible)

If you can’t share a video, screenshots can still be very helpful. Try to capture the whole Elements window so we can see your workspace and any visible settings.

Use the keyboard shortcut Command-Shift-3 to take a screenshot, or Command-Shift-4 to select just a portion of the screen.

## Removing Preferences

To reset Elements, remove the preferences file by following these steps.

{% hint style="info" %}
For an automatica way to remove the Preferences you can do the following. Hold down the option key and go to Help > Clear Applications Preferences.
{% endhint %}



{% stepper %}
{% step %}
### Quit Elements

Ensure Elements is not running.
{% endstep %}

{% step %}
### Locate Preferences File

In the finder press press “Command-Shift-G” to bring up the "Go To Folder" Window and paste in the following path:

{% code overflow="wrap" %}
```
~/Library/Containers/com.realmacsoftware.rapidweaverelements/Data/Library/Preferences/com.realmacsoftware.rapidweaverelements.plist
```
{% endcode %}
{% endstep %}

{% step %}
### Delete Preferences Plist

Delete the file: `com.realmacsoftware.rapidweaverelements.plist`
{% endstep %}

{% step %}
### Re-launch Elements

You can now safely re-launch Elements.
{% endstep %}
{% endstepper %}

