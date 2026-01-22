# JSON Documentation

[← Back to API Index](../reference.md)

---

## Class: JSON

### Description
Utilities for working with JSON data.

#### Native JSON.stringify() vs isc.JSON.encode()

For maximum performance when serializing large datasets, consider using the native `JSON.stringify()` when your data meets certain criteria. Native serialization is approximately **6-10x faster** than `isc.JSON.encode()`, but lacks several features that SmartClient provides:

**Use native `JSON.stringify()` when ALL of these conditions are met:**

*   Data contains **no circular references** - native throws an error on cycles rather than handling them gracefully. If your data might have cycles (e.g., parent/child back-references in tree structures), you must use `isc.JSON.encode()`.
*   Data contains **no Date values**, OR you accept JSON's default date handling. Native `JSON.stringify()` converts Dates to ISO 8601 strings (e.g., "2024-01-15T14:30:00.000Z"). This loses:
    *   **Logical Date distinction**: SmartClient's logical dates (date-only, no time component) are serialized identically to datetimes by native JSON
    *   **Logical Time distinction**: SmartClient's logical times (time-only, no date component) become full datetime strings
    *   **Timezone handling**: Native always outputs UTC; SmartClient can preserve local timezone context for logical dates/timesUse [JSONEncoder.dateFormat](JSONEncoder.md#attr-jsonencoderdateformat) with values like "logicalDateConstructor" to preserve these distinctions when round-tripping data.
*   Data contains **no SmartClient class instances** - native JSON cannot serialize SmartClient widgets or other framework objects meaningfully
*   You do **not need pretty-printed output** - native JSON.stringify's optional formatting is less flexible than [JSONEncoder.prettyPrint](JSONEncoder.md#attr-jsonencoderprettyprint)
*   You do **not need custom serialization** via object `_serialize()` methods

**Use `isc.JSON.encode()` when ANY of these apply:**

*   Data might contain circular references (automatically detected and handled)
*   You need to preserve SmartClient's logical date/time/datetime distinctions
*   You're serializing SmartClient components or class instances
*   You need back-reference paths for reconstructing object graphs
*   You want configurable date formats ([JSONDateFormat](../reference.md#type-jsondateformat))
*   You need readable, pretty-printed output

---
## ClassMethod: JSON.decodeSafe

### Description
Decodes strict JSON using native browser JSON parsing APIs. This API will not work with pseudo-JSON that must be parsed as JavaScript (such as that produced by encoding with [JSONDateFormat](../reference.md#type-jsondateformat) logicalDateConstructor).

This API is called "safe" because using a JavaScript eval() to decode JSON is potentially unsafe if the data being decoded is untrusted. For example, if users are able to save data as JSON for other uses to see (such as sharing [ListGrid.viewState](ListGrid_1.md#attr-listgridviewstate)) and there is no validation of the saved data to ensure safety and some users are untrusted, then saved JSON could be used similarly to an XSS attack, allowing one user to execute JavaScript code in another user's browser.

Note that, because JSON has no way of representing dates, serializing a structure that contains dates and then deserializing with decodeSafe() necessarily results in any Dates becoming strings. Use [JSONDateFormat](../reference.md#type-jsondateformat) "logicalDateString" in combination with [JSON.decodeSafeWithDates](#classmethod-jsondecodesafewithdates) to round-trip date, time and datetime values accurately.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| jsonString | [String](#type-string) | false | — | JSON data to be de-serialized |
| jsonReviver | [Function](#type-function) | false | — | optional setting |

### Returns

`[Object](../reference.md#type-object)` — object derived from JSON String

---
## ClassMethod: JSON.encode

### Description
Serialize an object as a JSON string by creating a [JSONEncoder](JSONEncoder.md#class-jsonencoder) and calling [JSONEncoder.encode](JSONEncoder.md#method-jsonencoderencode).

Note that using the String produced by this API with [JSON.decode](#classmethod-jsondecode) **will not successfully preserve dates**. Use [JSONEncoder.dateFormat](JSONEncoder.md#attr-jsonencoderdateformat) "dateConstructor" or "logicalDateConstructor" to have dates round-trip properly.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Any](#type-any) | false | — | object to serialize |
| settings | [JSONEncoder Properties](#type-jsonencoder-properties) | true | — | optional settings for encoding |

### Returns

`[String](#type-string)` — object encoded as a JSON String

---
## ClassMethod: JSON.decode

### Description
De-serialize an object from JSON. Currently, this is simply a JavaScript eval() and should be used for trusted data only.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| jsonString | [String](#type-string) | false | — | JSON data to be de-serialized |

### Returns

`[Object](../reference.md#type-object)` — object derived from JSON String

---
## ClassMethod: JSON.decodeSafeWithDates

### Description
Uses [JSON.decodeSafe](#classmethod-jsondecodesafe) to decode strict JSON using native browser JSON parsing APIs, with settings to correctly process formatted date values created with [JSONDateFormat](../reference.md#type-jsondateformat) logicalDateConstructor.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| jsonString | [String](#type-string) | false | — | JSON data to be de-serialized |

---
