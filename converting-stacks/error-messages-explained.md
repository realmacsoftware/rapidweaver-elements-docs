---
description: Stacks conversion error messages explained
---

# Error Messages Explained

#### `🛑 Pimary Stack Failed to Convert`

The main stack failed to convert for some reason which prevented any child stack from converting. Check the error on the main stack to see what happened.

**`💥 Parsing Error in File`**

This can happen for a number of reasons, but often it's because of unexpected characters in a template, either not handled, or in the wrong sequence.

#### `🔑 The Stacks contain encrypted data`

Some of the stacks data is encryped. This is often caused by the info.plist file containing encrypted data. Try conversion again with a fully unencrypted stack.

