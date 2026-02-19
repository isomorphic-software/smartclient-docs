# MathFunction Documentation

[← Back to API Index](../reference.md)

---

## Class: MathFunction

### Description
Represents a mathematical function that can be used in [UserFormula](../reference.md#object-userformula) expressions. A library of standard functions is registered by default; additional functions can be added via [MathFunction.registerFunction](#classmethod-mathfunctionregisterfunction).

### Groups

- formulaFields

---
## Attr: MathFunction.description

### Description
A short description of this function

### Groups

- formulaFields

**Flags**: IR

---
## Attr: MathFunction.defaultSortPosition

### Description
Indicates the sort-order of this [MathFunction](#class-mathfunction) in an index returned from static method [MathFunction.getDefaultFunctionIndex](#classmethod-mathfunctiongetdefaultfunctionindex). A lower value (>= 0) will cause a function to appear before a [MathFunction](#class-mathfunction) with a higher value of the property. The default of -1 means to exclude the MathFunction from the index entirely.

### Groups

- formulaFields

### See Also

- [MathFunction.getDefaultFunctionIndex](#classmethod-mathfunctiongetdefaultfunctionindex)

**Flags**: IR

---
## Attr: MathFunction.name

### Description
Name of the function (what the user actually types). For example, a name of "min" would indicate that the user types "min(someValue)" to use this function.

Mixed-case names may be used. As a convenience, a few aliases are registered by [MathFunction.registerFunction](#classmethod-mathfunctionregisterfunction) (see that method for details).

### Groups

- formulaFields

### See Also

- [MathFunction.registerFunction](#classmethod-mathfunctionregisterfunction)

**Flags**: IR

---
## Attr: MathFunction.jsFunction

### Description
Javascript method to perform the calculation associated with this function

### Groups

- formulaFields

**Flags**: IR

---
## ClassMethod: MathFunction.getRegisteredFunctionIndex

### Description
Returns an index of all registered functions by name

### Returns

`[int](../reference.md#type-int)` — —

### Groups

- formulaFields

---
## ClassMethod: MathFunction.getDefaultFunctionIndex

### Description
Returns an index of all default registered functions by name, ordered by [MathFunction.defaultSortPosition](#attr-mathfunctiondefaultsortposition). (Also includes those user-registered functions with non-default (>= 0) values for that property.)

### Returns

`[int](../reference.md#type-int)` — —

### Groups

- formulaFields

### See Also

- [Array.makeIndex](Array.md#method-arraymakeindex)
- [MathFunction.defaultSortPosition](#attr-mathfunctiondefaultsortposition)

---
## ClassMethod: MathFunction.registerFunction

### Description
Registers a new math function for use with FormulaFields. Mixed-case names are allowed, and as a convenience, the following aliases are also available:

*   name in all lowercase
*   name in all uppercase
*   name with first letter uppercase, and the rest unchanged

Note: The aliases are shallow copies of each other, so be aware that if [MathFunction.jsFunction](#attr-mathfunctionjsfunction) depends on instance state, objects accessed by instance properties will be shared by all copies.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newFunction | [MathFunction](#type-mathfunction) | false | — | — |

### Groups

- formulaFields

---
