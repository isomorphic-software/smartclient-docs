# MathFunction Documentation

[← Back to API Index](../main.md)

---

## Class: MathFunction

### Description
The definition of a function for use in the [FormulaBuilder](FormulaBuilder.md#class-formulabuilder). A function consists of a name (what the user actually types to use the function), a description (shown in help) and an actual JavaScript function that executes the calculation.

The built-in functions cover all static functionality on the JavaScript Math object:

*   **max(val1,val2)**: Maximum of two values
*   **min(val1,val2)**: Minimum of two values
*   **round(value,decimalDigits)**: Round a value up or down, optionally providing _decimalDigits_ as the maximum number of decimal places to round to. For fixed or precision rounding, use _toFixed()_ and _toPrecision()_ respectively.
*   **ceil(value)**: Round a value up
*   **floor(value)**: Round a value down
*   **abs(value)**: Absolute value
*   **pow(value1,value2)**: value1 to the power of value2
*   **sqrt(value)**: Square root of a value
*   **dateAdd(value,interval,amount)**: Excel™-compatible dataAdd function: adds quantities of a time interval to a date value. Also supports being passed interval names, like "hour" or "week".
*   **year(value)**: 4-digit integer that represents the year of a date.
*   **month(value)**: 1-12 integer that represents the month of a date.
*   **day(value)**: 1-31 integer that represents the day of month of a date.
*   **toPrecision(value,precision)**: Format a number to a length of _precision_ digits, rounding or adding a decimal point and zero-padding as necessary. Note that the values 123, 12.3 and 1.23 have an equal precision of 3. Returns a formatted string and should be used as the outermost function call in a formula. For rounding, use _round()_.
*   **toFixed(value,digits)**: Round or zero-pad a number to _digits_ decimal places. Returns a formatted string and should be used as the outermost function call in a formula. To round values or restrict precision, use _round()_ and _toPrecision()_ respectively.
*   **sin(value)**: Sine of a value
*   **cos(value)**: Cosine of a value
*   **tan(value)**: Tangent of a value
*   **ln(value)**: natural logarithm of a value
*   **log(base,value)**: logarithm of a value with the specified _base_
*   **asin(value)**: Arcsine of a value
*   **acos(value)**: Arccosine of a value
*   **atan(value)**: Arctangent of a value (-PI/2 to PI/2 radians)
*   **atan2(value1,value2)**: Angle theta of a point (-PI to PI radians)
*   **exp(value)**: The value of Evalue
*   **random()**: Random number between 0 and 1

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

`[int](../main.md#type-int)` — —

### Groups

- formulaFields

---
## ClassMethod: MathFunction.getDefaultFunctionIndex

### Description
Returns an index of all default registered functions by name, ordered by [MathFunction.defaultSortPosition](#attr-mathfunctiondefaultsortposition). (Also includes those user-registered functions with non-default (>= 0) values for that property.)

### Returns

`[int](../main.md#type-int)` — —

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
