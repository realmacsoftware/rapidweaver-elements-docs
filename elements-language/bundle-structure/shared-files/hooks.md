# Hooks

This folder should only contain JS files! There is no restriction on naming.

{% hint style="info" %}
All files in this directory are compressed into a single file and executed prior to executing the [hooks.js file](../components/hooks.js/) within a component.
{% endhint %}

There is no access to component properties or the Elements API directly within these files. However, you may create a function and pass them in as properties.

