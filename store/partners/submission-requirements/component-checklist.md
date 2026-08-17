# Component Checklist

If you are building components for Elements, they must meet the following criteria:

* [ ] **Do no modify the look of the Editor:**
  * [ ] Do not change the look of other components in the editor.
* [ ] **Component is WYSIWYG in the Editor:**
  * [ ] The Editor looks the same (or as close as technically possible) to Preview.
  * [ ] Settings and Admin options are not visible in the Editor. Place these in the Inspector, or include a toggle to hide in the Editor.
* [ ] **Component MUST use Tailwind CSS:**
  * [ ] Component styling should always use Tailwind classes found in the Theme Studio
  * [ ] Component should always use Theme based UI Controls where possible
  * [ ] Avoid generating custom CSS, always prefer Tailwind CSS
  * [ ] Do not use !important statements for generated CSS
* [ ] **Component should be Performant:**
  * [ ] Component should not parse @text or @typography data in their hooks.js files
  * [ ] Component UI should not slow down Editor
* [ ] Do not include HTML comments in code output
