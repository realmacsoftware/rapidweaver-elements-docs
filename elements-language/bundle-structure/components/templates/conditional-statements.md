---
description: Display content based on dynamic conditions.
---

# Conditional Statements

Conditional statements in Elements allow you to control when content is displayed based on certain conditions. Using @if, @else if, and @else, you can define different outcomes depending on the values of variables. This is useful for showing or hiding content based on user settings, mode (edit or preview), or other dynamic conditions.

{% hint style="info" %}
When performing complex logic like string comparisons, use the [hooks file](../hooks.js/) to perform this logic and provide simple bool values to the template. This helps to keep templates simple and focused on HTML rather than complex conditional logic!
{% endhint %}

### If Statement

The following example displays the text inside of the IF statment when the switch is on/true. It's worth noting that only non-responsive controls can be used in 'if' statements.

```html
@if(switch)
    <li><b>This is only visible when switch is true</b></li>
@endif
```

### If Not Statement

Elements lets you use the ! symbol to check if something is false. For example, @if(!edit) means ‘if edit mode is not active.’ This is useful when you only want to show something when a condition is not true. The ! can be used with any true or false value.

```html
@if(!edit)
    We're in preview mode or the site is Published.
@endif
```

### Else If Statements

Elements allows you to specify a number of else if statements to run before falling back to the else block. An `@elseif` statement works just like a regular `@if` statement and follows the same syntax.

```html
@if(edit)   
    We’re in edit mode   
@elseif(preview)   
    And now in preview   
@elseif(checkbox)   
    The checkbox is ticked   
@else
    Otherwise do this   
@endif
```

### Conditional Statement for Edit/Preview Modes

Elements gives you access to the current RapidWeaver mode inside of conditional statements. This can be particularly useful for showing content in edit mode or in preview.

```html
@if(edit)   
    Visible in Edit mode (inside Elements)
@elseif(preview)   
    Visible in local preview (in Safari).
@else
    Visible when Published.
@endif
```

