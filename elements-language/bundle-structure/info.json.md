---
description: Outline basic information about your Element
---

# info.json

The info.json file outlines the basic information about an Element. The file consists of a series of keys and values. It's required for an Element to function. [View example below](info.json.md#info.json-example).

### Supported Key-Value Pairs <a href="#key-value-pairs-explained" id="key-value-pairs-explained"></a>

The Elements info.json file supports the following key-value pairs.

| Key          | Type     | Notes                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------ | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| framework    | string   | The framework key allows you to list Elements under then "Framework" heading in the Elements Library.                                                                                                                                                                                                                                                                                                                      |
| identifier   | string   | The identifier is the unique ID for your Element. We recommend using a [reverse DNS format](https://developer.apple.com/library/archive/documentation/FileManagement/Conceptual/understanding\_utis/understand\_utis\_conc/understand\_utis\_conc.html). This should be a string consisting of just lowercase characters and periods without spaces.                                                                       |
| author       | string   | The name of the author of the Element. This would usually be the developer name, or the name of the company publishing the Element.                                                                                                                                                                                                                                                                                        |
| title        | string   | The name of the Element. This will be displayed inside of RapidWeaver. A unique and descriptive name is preferable. Overly long names will get truncated, check inside of the RapidWeaver UI for readability.                                                                                                                                                                                                              |
| group        | string   | Elements are grouped in the Elements Catalogue inside of RapidWever . You can use this key to group your Elements together.                                                                                                                                                                                                                                                                                                |
| build        | string   | The build number of an Element. The number should be an integer value, like "100". We recommend increasing the value with each release.                                                                                                                                                                                                                                                                                    |
| version      | string   | The version of an Element. We recommend the following convention (as used by many apps): _major.minor.patch. and in practice that might look like_ "1.0.0" for an initial release.                                                                                                                                                                                                                                         |
| icon         | string   | <p>The name of the <code>.icns</code> file to be used for the icon in the Elements Library. The corresponding <code>.icns</code> file should sit in the same directory as the <code>info.json</code> file.</p><p>RapidWeaver Elements will automatically look for an <code>.icns</code> file based on a key-value pair. For example; setting a value of "myIcon" would look for a file named <code>myIcon.icns</code>.</p> |
| helpURL      | string   | A URL to the location of the help documentation online.                                                                                                                                                                                                                                                                                                                                                                    |
| infoURL      | string   | A URL to the location of the marketing page online.                                                                                                                                                                                                                                                                                                                                                                        |
| `missingURL` | string   | The URL to redirect users to when this Element is uninstalled or missing.                                                                                                                                                                                                                                                                                                                                                  |
| `framework`  | `string` | Elements are grouped in the Elements Catalogue inside of RapidWever . You can use this key to group Elements from the same Framework togther.                                                                                                                                                                                                                                                                              |
|              |          |                                                                                                                                                                                                                                                                                                                                                                                                                            |

### info.json Example

You can use the following code as a starting point for your own info.json file.

```
{
  "identifier": "com.realmac.elementpack.helloworld",
  "author": "Realmac Software",
  "title": "Hello World",
  "group": "Fun",
  "build": "001",
  "version": "0.0.1",
  "icon": "icon"
}
```

<figure><img src="../../.gitbook/assets/CleanShot 2023-08-04 at 5.17.44@2x.png" alt=""><figcaption><p>Example info.json file inside of an Element.</p></figcaption></figure>
