# Conditional Statements

### If statment

Elements gives you access to the current RapidWeaver mode inside of conditional statements. This can be particularly useful for showing content in edit mode or in preview when a certain property evaluates to true.

```
@if(edit)
   Show this in edit
@endif
```

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

### Condistional Statement for edit/preview mode

The code example below displays a line of text in the various edit and preview modes.&#x20;

```
@if(edit)   
    Visible in Edit mode (inside Elements)
@elseif(preview)   
    Visible in local preview (in Safari).
@else
    Visible when Published.
@endif
```
