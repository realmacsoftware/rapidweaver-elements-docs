# Conditional Statements

### If Statement

The following example displays the text inside of the IF statment when the switch is on/true. It's worth noting that only non-responsive controls can be used in 'if' statements.

```
@if(switch)
    <li><b>This is only visible when switch is true</b></li>
@endif
```

When performing complex logic like string comparisons, use the [hooks file](../hooks.js/) to perform this logic and provide simple bool values to the template. This helps to keep templates simple and focused on HTML rather than complex conditional logic.

### Else If Statements

Elements allows you to specify a number of else if statements to run before falling back to the else block. An `@elseif` statement works just like a regular `@if` statement and follows the same syntax.

```
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

```
@if(edit)   
    Visible in Edit mode (inside Elements)
@elseif(preview)   
    Visible in local preview (in Safari).
@else
    Visible when Published.
@endif
```
