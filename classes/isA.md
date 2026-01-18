# isA Documentation

[← Back to API Index](../reference.md)

---

## StaticMethod: isA.nonemptyString

### Description
Is `object` a non-empty String?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to test |

### Returns

`[boolean](../reference.md#type-boolean)` — true == `object` is a non-empty string

---
## StaticMethod: isA.Date

### Description
Is `object` a Date object?

This method should be used instead of `instanceof Date` when the object may have been created in a different frame (e.g., iframe or popup window), as `instanceof` fails cross-frame. This method includes fallback detection using constructor toString comparison.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to test |

### Returns

`[boolean](../reference.md#type-boolean)` — true == `object` is a Date

---
## StaticMethod: isA.Interface

### Description
Is `object` an interface object?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to test |

### Returns

`[boolean](../reference.md#type-boolean)` — true == `object` is a Interface Object

---
## StaticMethod: isA.Boolean

### Description
Is `object` a Boolean object?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to test |

### Returns

`[boolean](../reference.md#type-boolean)` — true == `object` is a Boolean

---
## StaticMethod: isA.emptyObject

### Description
Is `object` an object with no properties (i.e.: `{}`)?

Note that an object that has properties with null values is considered non-empty, eg `{ propName:null }` is non-empty.

NOTE: if you prefer, you can call this as `isAn.emptyObject()`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to test |

### Returns

`[boolean](../reference.md#type-boolean)` — true == `object` is the empty object

---
## StaticMethod: isA.ClassObject

### Description
Is `object` a class object?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to test |

### Returns

`[boolean](../reference.md#type-boolean)` — true == `object` is a Class Object

---
## StaticMethod: isA.Instance

### Description
Is `object` an instance of some class?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to test |

### Returns

`[boolean](../reference.md#type-boolean)` — true == `object` is an instance of some class

---
## StaticMethod: isA.List

### Description
Does `object` implement the `List` interface?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to test |

### Returns

`[boolean](../reference.md#type-boolean)` — `true` if the object is an Array or belongs to another class that implements the `List` API.

---
## StaticMethod: isA.emptyArray

### Description
Is `object` an Array with no items?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to test |

### Returns

`[boolean](../reference.md#type-boolean)` — true == `object` is an empty array

---
## StaticMethod: isA.nonemptyArray

### Description
Is `object` an array with at least one item?

Note: `null`, `undefined`, and empty slots in an array are still considered an item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Any](#type-any) | false | — | The object or value to test. |

### Returns

`[boolean](../reference.md#type-boolean)` — `true` if `object` is an array with at least one item; `false` otherwise (i.e. `object` isn't an array, or it has no items)

---
## StaticMethod: isA.Object

### Description
Returns whether the passed value is a non-`null` Object.

Returns `false` for values that are numbers, strings, booleans, functions or are `null` or `undefined`. (Note: Returns `true` for the wrapper types, e.g. `new String("some string")`.)

Returns true for Object, Array, Regular Expression, Date and other kinds of native objects which are considered to extend from window.Object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Any](#type-any) | false | — | value to test for whether it's an object |

### Returns

`[boolean](../reference.md#type-boolean)` — whether passed value is an Object

---
## StaticMethod: isA.RegularExpression

### Description
Is `object` a Regular Expression (RegExp) object?

This method should be used instead of `instanceof RegExp` when the object may have been created in a different frame (e.g., iframe or popup window), as `instanceof` fails cross-frame. This method includes fallback detection using constructor toString comparison.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to test |

### Returns

`[boolean](../reference.md#type-boolean)` — true == `object` is a RegExp

---
## StaticMethod: isA.String

### Description
Is `object` a String object?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to test |

### Returns

`[boolean](../reference.md#type-boolean)` — true == `object` is a String

---
## StaticMethod: isA.Number

### Description
Is `object` a Number object?  
  
NOTE: this returns false if `object` is an invalid number (`isNaN(object) == true`)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to test |

### Returns

`[boolean](../reference.md#type-boolean)` — true == `object` is a Number

---
## StaticMethod: isA.Function

### Description
Is `object` a Function object?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to test |

### Returns

`[boolean](../reference.md#type-boolean)` — true == `object` is a Function

---
## StaticMethod: isA.emptyString

### Description
Is `object` the empty string?  
  
NOTE: if you prefer, you can call this as `isAn.emptyString()`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to test |

### Returns

`[boolean](../reference.md#type-boolean)` — true == `object` is a null string

---
## StaticMethod: isA.Array

### Description
Is `object` an Array object?  
  
NOTE: if you prefer, you can call this as `isAn.Array()`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | object to test |

### Returns

`[boolean](../reference.md#type-boolean)` — true == `object` is an Array

---
