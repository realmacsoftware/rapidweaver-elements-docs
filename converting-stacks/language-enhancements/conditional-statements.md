# Conditional Statements

## RapidWeaver Current Mode

{% hint style="info" %}
Available from RapidWeaver Elements Beta 5
{% endhint %}

Elements gives you access to the current RapidWeaver mode inside of conditional statements or functions. This can be particularly useful for showing content in edit mode or in preview when a certain property evaluates to true.

```
%[if %( edit || 
        %( !edit && %id=myCheckbox% )% 
     )% 
]%
   Show this in edit, or in preview/publish if myCheckbox is ticked
%[endif]%
```

## Else If Statements

{% hint style="info" %}
Available from RapidWeaver Elements Beta 5
{% endhint %}

Elements allows you to specify a number of else if statements to run before falling back to the else block. An `elseif` statement works just like a regular `if` statement and follows the same syntax.

```
%[if edit]%   
	We’re in edit mode   
%[elseif preview]%   
	And now in preview   
%[elseif %id=checkbox% ]%   
	The checkbox is ticked   
%[else]%   
   Otherwise do this   
%[endif]%  
```
