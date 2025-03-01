---
icon: face-scream
---

# Troubleshooting



## Removing Preferences

Before deleting your preferences file, ensure you have a copy of your license number. You will need to re-enter it when launching Elements. To reset Elements, remove the preferences file by following these steps.

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

You can now safely re-launch Elements and re-register.
{% endstep %}
{% endstepper %}

