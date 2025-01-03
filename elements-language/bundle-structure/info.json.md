---
icon: file
---

# info.json

The info.json file at the root of your Element Pack defines a few important things.

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
