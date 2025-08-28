---
icon: arrow-down-to-bracket
---

# Importing Projects

{% hint style="danger" %}
Please note this documentation is a work-in-progress!
{% endhint %}

{% hint style="warning" %}
**The Classic Project Importer does not yet read Partials.** To work around this, you may want to unpack any partials and save a copy of your Classic project before you import it into Elements.&#x20;

In Elements [we use Globals](../editor/global-templates.md) instead, these are a highly modern and customisable way to include global content throughtout your website.
{% endhint %}

### Stacks Resources

Elements will import all Stack Page Resources, it will then optimise the resources by de-duping files to ensure your Elements project and new site is smaller and faster!

### Supported Stacks Content

Elements currently imports the raw text and image content from a pre-determined list stacks, they are imported with minimal properties (i.e. no colours, or links, etc…).

Elements will attempt to import content from the following stacks. Unknown stacks will be converted into named Containers.

#### Built-in Stacks

* Text > Text
* Markdown > Text
* HTML > Text
* Header > Text
* Quote > Text
* Image & Site Image > Image
* Button > Button
* Column stacks will be converted into the Grid Component and use the corresponding number of columns.

#### Foundry 2

* Button > Button
* Container > Container
* Vertical Center > Container
* Header > Text
* Header Plus > Text
* Paragraph > Typography
* Grid Content > Grid
* Image > Image
* Banner > Container
* Margins > Container

#### Foundry 3

* Container > Container
* Columns Grid
* Col > Grid
* Header > Text
* Paragraph > Typography
* Image > Image

#### Foundation 6

* Container > Container
* 1col > Grid
* Header > Text
* Header Pro > Text
* Text > Text
* Picture > Image\


{% hint style="warning" %}
This documenation is currently being written…
{% endhint %}
