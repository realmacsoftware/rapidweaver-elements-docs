# Select

{% hint style="success" %}
Supports responsive values
{% endhint %}

Displays a select box, also known as a dropdown menu. A select box can be responsive or non-responsive and has two or more items to choose from.&#x20;

<figure><img src="../../../../../.gitbook/assets/Screenshot 2025-03-10 at 21.11.14.png" alt=""><figcaption></figcaption></figure>

#### Property Schema

<table><thead><tr><th width="156">Key</th><th width="110">Value</th><th>Notes</th></tr></thead><tbody><tr><td><code>title</code></td><td>string</td><td>See <a href="../general-structure/title.md">Title</a> for more information</td></tr><tr><td><code>id</code></td><td>string</td><td>See <a href="../general-structure/id.md">ID</a> for more information</td></tr><tr><td><code>format</code></td><td>string</td><td>See <a href="../general-structure/format.md">Format</a> for more information</td></tr><tr><td><code>visible</code></td><td>string</td><td>See <a href="../general-structure/visible.md">Visible</a> for more information</td></tr><tr><td><code>enabled</code></td><td>string</td><td>See <a href="../general-structure/enabled.md">Enabled</a> for more information</td></tr><tr><td><code>responsive</code></td><td>boolean</td><td>See <a href="../general-structure/responsive.md">Responsive</a> for more information, default: true</td></tr><tr><td><code>select</code></td><td>object</td><td>See <a href="select.md#select-schema">Select Schema</a> below</td></tr></tbody></table>

#### Select Schema

<table><thead><tr><th width="156">Key</th><th width="110">Value</th><th>Notes</th></tr></thead><tbody><tr><td><code>default</code></td><td>string</td><td>Value of the default item to be selected</td></tr><tr><td><code>items</code></td><td>array</td><td>See <a href="select.md#item-schema">Item Schema</a> below</td></tr></tbody></table>

#### Item Schema

<table><thead><tr><th width="156">Key</th><th width="110">Value</th><th>Notes</th></tr></thead><tbody><tr><td><code>title</code></td><td>string</td><td>The item title to be displayed in the dropdown</td></tr><tr><td><code>value</code></td><td>string</td><td>The value to be returned</td></tr></tbody></table>

#### Return Value

The returned value is dependent on the responsive setting and either returns a string of tailwind classes or the raw value.

<table><thead><tr><th width="180">Responsive</th><th width="337">Return Value</th><th data-hidden></th></tr></thead><tbody><tr><td><code>true</code></td><td>string of tailwind classes</td><td>See <a href="../general-structure/title.md">Title</a> for more information</td></tr><tr><td><code>false</code></td><td>raw string value</td><td>See <a href="../general-structure/id.md">ID</a> for more information</td></tr></tbody></table>

#### Example

Below is an example of a typical responsive dropdown that returns one or more tailwind text transform classes, one for each device breakpoint.

{% tabs %}
{% tab title="Control Example" %}
```json
{
    "title": "Case",
    "id": "headingTextTransform",
    "select": {
        "default": "normal-case",
        "items": [{
            "value": "normal-case",
            "title": "None"
        }, {
            "value": "uppercase",
            "title": "Uppercase"
        }, {
            "value": "lowercase",
            "title": "Lowercase"
        }, {
            "value": "capitalize",
            "title": "Capitalize"
        }]
    }
}
```
{% endtab %}

{% tab title="Group Example" %}
```json
{
    "groups": [{
        "title": "Select Example",
        "properties": [{
            "title": "Case",
            "id": "headingTextTransform",
            "select": {
                "default": "normal-case",
                "items": [{
                    "value": "normal-case",
                    "title": "None"
                }, {
                    "value": "uppercase",
                    "title": "Uppercase"
                }, {
                    "value": "lowercase",
                    "title": "Lowercase"
                }, {
                    "value": "capitalize",
                    "title": "Capitalize"
                }]
            }
        }]
    }]
}
```
{% endtab %}
{% endtabs %}
