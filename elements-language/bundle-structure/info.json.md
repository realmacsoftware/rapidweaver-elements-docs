---
description: Outline basic information about your Element
---

# info.json

The info.json file outlines the basic information about an Element. The file consists of a series of keys and values. It's required for an Element to function. [View example below](info.json.md#info.json-example).

### Supported Key-Value Pairs <a href="#key-value-pairs-explained" id="key-value-pairs-explained"></a>

The Elements info.json file supports the following key-value pairs.

{% hint style="info" %}
**Important:** This documentation is incomplete and missing key-value pairs.

Check back soon for a complete list.
{% endhint %}

#### Framework

**`Key:`**`framework` \
**`Type:`**`string`

Elements are grouped in the Elements Catalogue inside of RapidWever . You can use this key to group Elements from the same Framework togther.

#### Identifier

**`Key:`**`identifier` \
**`Type:`**`string`

The identifier is the unique ID for your Element. We recommend using a [reverse DNS format](https://developer.apple.com/library/archive/documentation/FileManagement/Conceptual/understanding\_utis/understand\_utis\_conc/understand\_utis\_conc.html). This should be a string consisting of just lowercase characters and periods without spaces.

#### Author

**`Key:`**`author`\
**`Type:`**`string`

The name of the author of the Element. This would usually be the developer name, or the name of the company publishing the Element.

#### Title

**`Key:`**`title`\
**`Type:`**`string`

The name of the Element. This will be displayed inside of RapidWeaver. A unique and descriptive name is preferable. Overly long names will get truncated, check inside of the RapidWeaver UI for readability.

#### Group

**`Key:`**`group`\
**`Type:`**`string`

Elements are grouped in the Elements Catalogue inside of RapidWever . You can use this key to group your Elements togther.

#### Build

**`Key:`**`build`\
**`Type:`**`string`

The build number of an Element. The number should be an integer value, like "100". We recommend increasing the value with each release.

#### Version

**`Key:`**`version`\
**`Type:`**`string`

The version of an Element. We recommend the following convention (as used by many apps): _major.minor.patch. and in factice that might look like_ "1.0.0" for an initial release..

#### Icon

**`Key:`**`icon`\
**`Type:`**`string`

The name of the `.icns` file to be used for the icon in the Elements Library. The corresponding `.icns` file should sit in the same directory as the `info.json` file.

RapidWeaver Elements will automatically look for an `.icns` file based on a key-value pair. For example; setting a value of "myIcon" would look for a file named `myIcon.icns`.

#### helpURL

**`Key:`**`helpURL`\
**`Type:`**`string`

A URL to the location of the help documentation online.

#### infoURL

**`Key:`**`infoURL`\
**`Type:`**`string`

A URL to the location of the marketing page online.

#### missingURL

**`Key:`**`missingURL`\
**`Type:`**`string`

The URL to redirect users to when this Element is uninstalled or missing.

### info.json Example

You can use the following code as a starting point for your own info.json file.

```
{
  "identifier": "com.realmac.elementpack.helloworld",
  "author": "Realmac Software",
  "title": "Hello World",
  "group": "Fun",
  "build": "001",
  "framework": "MyAwesomeFramwork",
  "version": "0.0.1",
  "icon": "icon"
}
```

