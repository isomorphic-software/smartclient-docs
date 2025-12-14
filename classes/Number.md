# Number Documentation

[← Back to API Index](../reference.md)

---

## Method: Number.isBetween

### Description
Returns true if the number parameter falls between the 'first' and 'second' paramters.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| number | [number](#type-number) | false | — | Number object to be evaluated |
| first | [number](#type-number) | true | — | Number at the lower boundary |
| second | [number](#type-number) | true | — | Number at the upper boundary |
| inclusive | [number](#type-number) | true | — | Whether or not the numbers at either end of the boundary should be included in the comparison |

### Returns

`[Boolean](#type-boolean)` — True if the given `number` falls inside the given range, false otherwise @example n = 3; bool = n.isBetween(3, 3, 6, true); // true @example n = 3; bool = n.isBetween(3, 3, 6); // false

---
## Method: Number.toCurrencyString

### Description
Return this number as a currency-formatted string.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| currencyChar | [String](#type-string) | true | — | Currency symbol, can be set to an empty string. If unset `"$"` will be used. |
| decimalChar | [String](#type-string) | true | — | Decimal separator symbol. If unset `"."` will be used. |
| padDecimal | [boolean](../reference.md#type-boolean) | true | — | Should decimal portion be padded out to two digits? True by default. |
| currencyCharLast | [boolean](../reference.md#type-boolean) | true | — | Should currency symbol come at the end of the string? If unspecified, currency symbol will be shown at the beginning of the string. |

### Returns

`[String](#type-string)` — Currency-formatted string version of the number

### Groups

- stringProcessing

**Deprecated**

---
## Method: Number.stringify

### Description
Return this number as a string padded out to digits length.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| digits | [number](#type-number) | true | 2 | Number of digits to pad to. (Default is 2) |

### Returns

`[String](#type-string)` — Padded string version of the number

### Groups

- stringProcessing

**Deprecated**

---
