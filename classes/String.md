# String Documentation

[← Back to API Index](../reference.md)

---

## ClassAttr: String.pluralNounMap

### Description
The `String.pluralNounMap` contains a mapping from common irregular plural nouns to their plural versions.

It is consulted by [String.pluralize](#method-stringpluralize)

The default value for this mapping is as follows:

*   "child": "children"
*   "foot": "feet"
*   "tooth": "teeth"
*   "man": "men"
*   "woman": "women"
*   "person": "people"
*   "goose": "geese"
*   "mouse": "mice"
*   "die": "dice"
*   "leaf": "leaves"
*   "thief": "thieves"
*   "wife": "wives"
*   "life": "lives"
*   "elf": "elves"
*   "loaf": "loaves"
*   "potato": "potatoes"
*   "tomato": "tomatoes"
*   "cactus": "cacti"
*   "focus": "foci"
*   "fungus": "fungi"
*   "nucleus": "nuclei"
*   "syllabus": "syllabi"
*   "analysis": "analyses"
*   "basis": "bases"
*   "crisis": "crises"
*   "diagnosis": "diagnoses"
*   "thesis": "theses"
*   "criterion": "criteria"
*   "phenomenon": "phenomena"
*   "appendix": "appendices"
*   "index": "indices"
*   "matrix": "matrices"
*   "radius": "radii"
*   "deer": "deer"
*   "fish": "fish"
*   "sheep": "sheep"
*   "swine": "swine"
*   "moose": "moose"
*   "goat": "goats"
*   "ox": "oxen"
*   "louse": "lice"
*   "mouse": "mice"
*   "house": "houses"
*   "blouse": "blouses"
*   "scarf": "scarves"
*   "roof": "roofs"
*   "chief": "chiefs"
*   "belief": "beliefs"
*   "chef": "chefs"
*   "thief": "thieves"
*   "cliff": "cliffs"
*   "proof": "proofs"
*   "reef": "reefs"
*   "wolf": "wolves"
*   "knife": "knives"
*   "wife": "wives"
*   "life": "lives"
*   "elf": "elves"
*   "loaf": "loaves"
*   "shelf": "shelves"
*   "calf": "calves"
*   "half": "halves"
*   "leaf": "leaves"
*   "thief": "thieves"
*   "knife": "knives"
*   "wife": "wives"
*   "elf": "elves"
*   "loaf": "loaves"
*   "potato": "potatoes"
*   "tomato": "tomatoes"
*   "cactus": "cacti"
*   "focus": "foci"
*   "fungus": "fungi"
*   "nucleus": "nuclei"
*   "syllabus": "syllabi"
*   "analysis": "analyses"
*   "basis": "bases"
*   "crisis": "crises"
*   "diagnosis": "diagnoses"
*   "thesis": "theses"
*   "criterion": "criteria"
*   "phenomenon": "phenomena"
*   "appendix": "appendices"
*   "index": "indices"
*   "matrix": "matrices"
*   "radius": "radii"
*   "deer": "deer"
*   "fish": "fish"
*   "sheep": "sheep"
*   "swine": "swine"
*   "moose": "moose"
*   "goat": "goats"
*   "ox": "oxen"
*   "louse": "lice"
*   "mouse": "mice"
*   "house": "houses"
*   "blouse": "blouses"
*   "scarf": "scarves"
*   "roof": "roofs"
*   "chief": "chiefs"
*   "belief": "beliefs"
*   "chef": "chefs"
*   "thief": "thieves"
*   "cliff": "cliffs"
*   "proof": "proofs"
*   "reef": "reefs"
*   "wolf": "wolves"
*   "knife": "knives"
*   "wife": "wives"
*   "life": "lives"
*   "elf": "elves"
*   "loaf": "loaves"
*   "shelf": "shelves"
*   "calf": "calves"
*   "half": "halves"

### Groups

- i18nMessages

**Flags**: IRW

---
## Method: String.pluralize

### Description
Given a number, this method will return the plural version of the string if appropriate.

The plural value will be derived from [String.pluralNounMap](#classattr-stringpluralnounmap) if present, otherwise the plural value will be created by adding a lower or upper case `"s"` character to the string.

### Returns

`[String](#type-string)` — plural version of the string

---
## Method: String.startsWith

### Description
Returns `true` if this string starts with another string, or if the other string occurs at the given `position` within this string.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| substring | [String](#type-string) | false | — | other string to check |
| position | [int](../reference.md#type-int) | true | — | optional position in this string. Defaults to 0. |

### Returns

`[boolean](../reference.md#type-boolean)` — `true` if `substring` occurs within this string at position `position`.

### Groups

- stringProcessing

---
## Method: String.endsWith

### Description
Returns `true` if this string ends with another string, or if the other string occurs in this string beginning at `position - substring.length`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| substring | [String](#type-string) | false | — | other string to check |
| position | [int](../reference.md#type-int) | true | — | optional position in this string. Defaults to the length of this string. |

### Returns

`[boolean](../reference.md#type-boolean)` — `true` if `substring` occurs within this string ending with `position - 1`.

### Groups

- stringProcessing

---
## Method: String.contains

### Description
Returns true if this string contains the specified substring.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| substring | [String](#type-string) | false | — | string to look for |

### Returns

`[boolean](../reference.md#type-boolean)` — true == this string contains the substring

### Groups

- stringProcessing

---
## Method: String.asHTML

### Description
Convert plain text into into displayable HTML.

This prevents HTML-special characters like '<' and '>' from being interpreted as tags, and preserves line breaks and extra spacing.

```
    converts         to
    --------         ---------------------------
    &                &amp;
    <                &lt;
    >                &gt;
    \r,\n,\r\n1space <BR>&nbsp;
    \r,\n,\r\n       <BR>
    \t               &nbsp;&nbsp;&nbsp;&nbsp;
    2 spaces         1space&nbsp;
 
```

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — string of HTML with tags in the original HTML escaped.

### Groups

- stringProcessing

---
## StaticMethod: String.isValidID

### Description
Tests whether the given string is a valid JavaScript identifier.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| string | [String](#type-string) | false | — | the string to test. |

### Returns

`[boolean](../reference.md#type-boolean)` — true if string is a valid JavaScript identifier; false otherwise.

---
