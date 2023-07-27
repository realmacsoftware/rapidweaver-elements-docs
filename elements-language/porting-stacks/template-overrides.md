# Template Overrides

Template overrides allow you to write an Elements specific template to be used during conversion. The advantage of this is so you can use the simplified and improved [Elements templating language](../../converting-stacks/language-enhancements/). &#x20;

To use template overrides during conversion, simply create a new file with the same name as your existing template and insert `.elements` before the file extension.

```
[filename].elements.[ext]
```

When the converter encounters one of these files, it'll use it in preference of your stacks template file.

Here's an example of how your Resources folder might look after creating a template override for `template.html`

```
template.html
template.elements.html
```

You can of course distribute your stack with this additional file, this will not cause any issues as Stacks will simply ignore it. It's also worth noting that you can still use the stacks language within the template override file.
