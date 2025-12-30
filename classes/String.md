# String Documentation

[← Back to API Index](../reference.md)

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
