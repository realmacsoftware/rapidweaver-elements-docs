---
icon: file
---

# info.json

The info.json file at the root of your Element Pack defines important information about the pack.

* title: The name of the element pack
* identifier: A unique id for the pack, should be a reverse domain identifier
* author: The author of the pack
* version: (Integer) The major version number, ie v1, v2
* build: (Integer) A number identifying a particular build within the current version. This should increase with each release.

```json
{
  "title": "Pack Name",
  "identifier": "com.companyname.packname",
  "author": "Realmac Software",
  "version": 1,
  "build": 31
}
```

### Version Numbers

When you create a new pack the version number should be set to 1 and build should also be 1. As you make changes to components and release an update, the build number should increase. This allows you to identify the particular release a user has, identify issues, and supply fixes or add new features.

When you need to make breaking changes, or you'd like to release a chargeable upgrade, it's best to increment the version number and reset the build to 1.
