# Containers

## Named Containers

{% hint style="info" %}
Available from RapidWeaver Elements Beta 6
{% endhint %}

Elements allows you to name any container within your template file giving you a consistant & reliable way to manage child items. To use a named container, add the `name` argument to a `slice` statement.

```
%slice -name="extraItems"%
```

Named containers can also help tidy up conditional statements, making them less error prone and far easier to follow.

```
%[if edit]%
   %slice -name="extraItems"%
%[elseif %( !edit && %id=myCheckbox% )% ]%
   %slice -name="extraItems"%
%[endif]%
```

⚠️ It is the developer's responsibility to ensure multiple containers with the same name are not shown at the same time.
