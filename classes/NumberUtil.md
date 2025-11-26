# NumberUtil Documentation

[← Back to API Index](../reference.md)

---

## Class: NumberUtil

### Description
Static singleton class containing APIs for interacting with Numbers.

---
## ClassAttr: NumberUtil.groupingFormat

### Description
The grouping-format for numbers

### Groups

- i18nMessages

**Flags**: IR

---
## ClassAttr: NumberUtil.negativeSymbol

### Description
The negative symbol to use when formatting numbers

### Groups

- i18nMessages

**Flags**: IR

---
## ClassAttr: NumberUtil.currencySymbolLast

### Description
If true, show any currency symbol after the number when formatting numbers. If false, show any currency symbol before the number

**Flags**: IR

---
## ClassAttr: NumberUtil.decimalSymbol

### Description
The decimal symbol to use when formatting numbers

### Groups

- i18nMessages

**Flags**: IR

---
## ClassAttr: NumberUtil.currencySymbol

### Description
The currency symbol to use when formatting numbers

### Groups

- i18nMessages

**Flags**: IR

---
## ClassAttr: NumberUtil.negativeFormat

### Description
The format to use when formatting negative numbers. Supported values are: 1 = before, 2 = after, 3 = beforeSpace, 4 = afterSpace, 5 = parens

### Groups

- i18nMessages

**Flags**: IR

---
## ClassAttr: NumberUtil.groupingSymbol

### Description
The grouping symbol, or thousands separator, to use when formatting numbers

### Groups

- i18nMessages

**Flags**: IR

---
## ClassMethod: NumberUtil.format

### Description
Return the parameter number formatted according to the parameter [FormatString](../reference.md#type-formatstring). This method is used to implement the [DataSourceField.format](DataSourceField.md#attr-datasourcefieldformat) functionality, but it can also be used to format arbitrary numbers programmatically.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| number | [Number](#type-number) | false | — | The number to format |
| format | [FormatString](../reference.md#type-formatstring) | false | — | The format to apply |

### Returns

`[String](#type-string)` — formatted number string

---
## ClassMethod: NumberUtil.toUSString

### Description
Format the passed number as a US string. Returns empty string if not passed a number.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| number | [Number](#type-number) | false | — | the number object to format |
| decimalPrecision | [number](#type-number) | true | — | — |

### Returns

`[String](#type-string)` — formatted number or empty string if not passed a number

---
## ClassMethod: NumberUtil.toCurrencyString

### Description
Return the passed number as a currency-formatted string, or an empty string if not passed a number.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| number | [Number](#type-number) | false | — | the number to convert |
| currencyChar | [String](#type-string) | true | — | Currency symbol, default taken from the locale and can be set to an empty string. If not passed and missing from the locale, defaults to `"$"`. |
| decimalChar | [String](#type-string) | true | — | Decimal separator symbol, default taken from the locale. If if not passed and missing from the locale, defaults to `"."`. |
| padDecimal | [boolean](../reference.md#type-boolean) | true | — | Should decimal portion be padded out to two digits? True by default. |
| currencyCharLast | [boolean](../reference.md#type-boolean) | true | — | Should the currency symbol be shown at the end of the string? If unspecified, and not defined in the locale, it will prefix the number. |

### Returns

`[String](#type-string)` — Currency-formatted string version of the number

### Groups

- stringProcessing

---
## ClassMethod: NumberUtil.parseIfNumeric

### Description
If given a numeric string (that is, a non-empty string which converts to a number), will return the equivalent integer. Otherwise, returns the parameter unchanged. Useful for dealing with values that can be numbers or strings, but which you want to coerce to a numeric type if possible.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| numberOrString | [Any](#type-any) | false | — | the string or number to parse |

### Returns

`[Any](#type-any)` — an integer, if possible, otherwise the input unchanged

---
## ClassMethod: NumberUtil.parseInt

### Description
Parse string that contains integer number. This method correctly handles locale based separators and currency symbol.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| string | [String](#type-string) | false | — | the string to parse |

### Returns

`[Number](#type-number)` — parsed number as a Number

---
## ClassMethod: NumberUtil.stringify

### Description
Return the passed number as a string padded out to digits length.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| number | [number](#type-number) | false | — | Number object to stringify |
| digits | [number](#type-number) | true | — | Number of digits to pad to. (Default is 2) |

### Returns

`[String](#type-string)` — Padded string version of the number

### Groups

- stringProcessing

---
## ClassMethod: NumberUtil.isBetween

### Description
Returns true if the number parameter falls between the 'first' and 'second' parameters.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| number | [number](#type-number) | false | — | Number object to be evaluated |
| first | [number](#type-number) | true | — | Number at the lower boundary |
| second | [number](#type-number) | true | — | Number at the upper boundary |
| inclusive | [number](#type-number) | true | — | Whether or not the numbers at either end of the boundary should be included in the comparison |

### Returns

`[Boolean](#type-boolean)` — True if the given `number` falls inside the given range, false otherwise @example n = 3; bool = n.isBetween(3, 3, 6, true); // true

### Groups

- stringProcessing

---
## ClassMethod: NumberUtil.clamp

### Description
Returns a clamped number between a min and max.

```
 var clamped = isc.NumberUtil.clamp(10, 0, 5); // Returns 5 because 10 is greater than 5
 var clamped = isc.NumberUtil.clamp(-3, 0, 5); // Returns 0 because -3 is less than 0
 var clamped = isc.NumberUtil.clamp(4, 0, 5); // Returns 4 because 4 is between 0 and 5
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| number | [Number](#type-number) | false | — | the number to clamp |
| min | [Number](#type-number) | false | — | the number to return if the number is lower than min |
| max | [Number](#type-number) | false | — | the number to return if the number is higher than max |

### Returns

`[Number](#type-number)` — the clamped number

---
## ClassMethod: NumberUtil.parseFloat

### Description
Parse string that contains float number. This method correctly handles locale based separators, decimal points and currency symbol.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| string | [String](#type-string) | false | — | the string to parse |

### Returns

`[float](../reference.md#type-float)` — parsed number as a Number

---
## ClassMethod: NumberUtil.toUSCurrencyString

### Description
Format the passed number as a US Dollar currency string. Returns empty string if not passed a number.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| number | [Number](#type-number) | false | — | the number object to format |
| decimalPrecision | [number](#type-number) | true | — | — |

### Returns

`[String](#type-string)` — formatted number

---
## ClassMethod: NumberUtil.toLocalizedString

### Description
Format the passed number for readability, with:

*   separators between three-digit groups
*   optional fixed decimal precision (so decimal points align on right-aligned numbers)
*   localized decimal, grouping, and negative symbols

[Decimal symbol](#classattr-numberutildecimalsymbol), [grouping symbol](#classattr-numberutilgroupingsymbol), and [negative symbol](#classattr-numberutilnegativesymbol) will normally come from SmartClient locale settings (which may come from either client OS or application locale settings), but they are also supported as arguments for mixed-format applications (eg normalize all currency to [US format](#classmethod-numberutiltouscurrencystring), but use the current locale format for other numbers).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| number | [Number](#type-number) | false | — | the number object to convert |
| decimalPrecision | [number](#type-number) | true | — | decimal-precision for the formatted value |
| decimalSymbol | [String](#type-string) | true | — | the symbol that appears before the decimal part of the number |
| groupingSymbol | [String](#type-string) | true | — | the symbol shown between groups of 3 non-decimal digits |
| negativeSymbol | [String](#type-string) | true | — | the symbol that indicate a negative number |

### Returns

`[String](#type-string)` — formatted number or empty string if not passed a number.

---
