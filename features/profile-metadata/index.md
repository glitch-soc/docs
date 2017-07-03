---
title: Profile metadata
---

##  Profile metadata  ##

`glitch-soc` allows users to input optional `key: value` pairs as YAML-esque frontmatter at the beginning of their bios, which is then rendered in a table by the frontend and on static pages.
An example of a bio with this frontmatter is as follows:

```yaml
---
Name: Biff
Occupation: Example person
...
Here is my incredibly enlightening bio!
```

###  Syntax

The syntax for profile frontmatter matches that used for single-line YAML implicit keys.
Strings may be provided in single-quoted, double-quoted or plain (unquoted) styles.

Although `glitch-soc` borrows the *syntax* of YAML for its profile frontmatter, it does not borrow the *semantics*: Ordering and duplicate keys are preserved, and every value is interpreted as a string.
Links, hashtags, and mentions are all valid inside of frontmatter keys or values.
