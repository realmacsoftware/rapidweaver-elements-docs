---
description: Outline basic information about your Element
---

# info

The info.json file outlines the basic information about an Element. The file consists of a series of keys and values. It's required for an Element to function. [View example below](info.json.md#info.json-example).

### Supported Key-Value Pairs <a href="#key-value-pairs-explained" id="key-value-pairs-explained"></a>

The Elements info.json file supports the following key-value pairs.

<table><thead><tr><th>Key</th><th width="100">Type</th><th>Notes</th></tr></thead><tbody><tr><td><code>identifier (Required)</code></td><td>string</td><td>The identifier is the unique ID for your Element. We recommend using a <a href="https://developer.apple.com/library/archive/documentation/FileManagement/Conceptual/understanding_utis/understand_utis_conc/understand_utis_conc.html">reverse DNS format</a>. This should be a string consisting of just lowercase characters and periods without spaces.</td></tr><tr><td><code>author (Required)</code></td><td>string</td><td>The name of the author of the Element. This would usually be the developer name, or the name of the company publishing the Element.</td></tr><tr><td><code>title (Required)</code></td><td>string</td><td>The name of the Element. This will be displayed inside of RapidWeaver. A unique and descriptive name is preferable. Overly long names will get truncated, check inside of the RapidWeaver UI for readability.</td></tr><tr><td><code>group (Required)</code></td><td>string</td><td>Elements are grouped in the Elements Catalogue inside of RapidWever . You can use this key to group your Elements together.</td></tr><tr><td><code>build (Required)</code></td><td>string</td><td>The build number of an Element. The number should be an integer value, like "100". We recommend increasing the value with each release.</td></tr><tr><td><code>version (Required)</code></td><td>string</td><td>The version of an Element. We recommend the following convention (as used by many apps): <em>major.minor.patch. and in practice that might look like</em> "1.0.0" for an initial release.</td></tr><tr><td><code>tags</code></td><td>array</td><td>A list of tags relevant to the Elements.</td></tr><tr><td><code>helpURL</code></td><td>string</td><td>A URL to the location of the help documentation online.</td></tr><tr><td><code>infoURL</code></td><td>string</td><td>A URL to the location of the marketing page online.</td></tr><tr><td><code>missingURL</code></td><td>string</td><td>The URL to redirect users to when this Element is uninstalled or missing.</td></tr><tr><td><code>framework</code></td><td>string</td><td>Elements are grouped in the Elements Catalogue inside of RapidWever . You can use this key to group Elements from the same Framework togther.</td></tr><tr><td><code>assets</code></td><td>array</td><td>A list of required assets for the Element. This can be a mixed list of images and files for example.</td></tr></tbody></table>

### info.json Example

You can use the following code as a starting point for your own info.json file.

```
{
  "identifier": "com.realmac.elementpack.helloworld",
  "author": "Realmac Software",
  "title": "Hello World",
    "tags": [
    "simple",
    "example"
  ],
  "group": "Fun",
  "build": "001",
  "version": "0.0.1",
  "assets": [
    {
      "filename": "assets/image-square.png"
    }
  ]
}

}
```

<figure><img src="../../.gitbook/assets/CleanShot 2023-08-04 at 5.17.44@2x.png" alt=""><figcaption><p>Example info.json file inside of an Element.</p></figcaption></figure>
