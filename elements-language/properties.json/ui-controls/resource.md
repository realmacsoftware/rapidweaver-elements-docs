# Resource



{% tabs %}
{% tab title="Single Example" %}
The following code example for the Resources control should be placed inside of the main ‘properties’ array which is inside of groups, see [Grouping Controls](../grouping-controls.md).

```
{
            "title": "Resource",
            "id": "resource",
            "resource": {}
        }
```
{% endtab %}

{% tab title="Group Example" %}
In this example, the Resource control is placed within a group titled “Resource Example”. The configuration is defined as follows:

```
{
    "groups": [{
        "title": "Resource Example",
        "properties": [{
            "title": "Resource",
            "id": "resource",
            "resource": {}
        }]
    }]
}
```
{% endtab %}
{% endtabs %}





