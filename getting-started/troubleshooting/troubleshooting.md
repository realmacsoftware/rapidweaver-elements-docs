---
description: Reset Elements by clearing its application preferences
---

# Reset Elements

To reset Elements, remove the preferences file by following these steps.

{% hint style="warning" %}
To clear the preferences automatically, hold down the Option key and choose **Help → Clear Application Preferences**.
{% endhint %}

{% stepper %}
{% step %}
#### Quit Elements

Ensure Elements is not running.
{% endstep %}

{% step %}
#### Locate Preferences File

In Finder, press Command-Shift-G to open the **Go to Folder** window, then paste in the following path:

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
