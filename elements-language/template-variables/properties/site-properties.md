---
description: Access the users project settings
---

# Site Properties

The users site site settings can be accessed as properties from all templates files.



**Title**&#x20;

Plain text value.

```
%rw:projectTitle%
```

**Slogan**&#x20;

Plain text value.

```
%rw:projectSlogan%
```

**Footer**

Plain text value.

```
%rw:projectFooter%
```

**Email**

Plain text value.

```
%rw:projectEmail%
```

**Contact Text**

Plain text value.

```
%rw:projectContactText%
```

**Base URL**

Plain text value.

```
%rw:projectBaseURL%
```

**Enable Social Tags**

Bool, returns a string of "True" or "False".

```
%rw:projectEnableSocialTags%
```

**Twitter Account**

Plain text value.

```
%rw:projectTwitterAccount%
```

**Project Language**

Plain text value.

```
%rw:projectLanguage%
```

**Banner URL**

Plan text value.

```
%rw:projectBannerURL%
```

**Banner Alt Text**

Plan text value.

```
%rw:projectBannerAltText%
```

**Logo URL**

Plan text value.

```
%rw:projectLogoURL%
```

**Logo Alt Text**

Plan text value.

```
%rw:projectLogoAltText%
```

### Code Example

The following example outputs the project title and slogan.

```
<H1>%rw:projectTitle%</h1>
<h2>%rw:projectSlogan%</h2>
```

