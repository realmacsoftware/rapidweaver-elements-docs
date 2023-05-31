# info.json

The info.json file defines the basic information about about an Element. The file consists of a series of keys and values. [View example below](info.json.md#info.json-example).

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

Elements are grouped inside of RapidWeaver undercollections. You can use this key to group your Elements togther.

### info.json example

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

