# JSON Documentation

[← Back to API Index](../reference.md)

---

## Class: JSON

### Description
Utilities for working with JSON data.

---
## ClassMethod: JSON.decodeSafe

### Description
Decodes strict JSON using native browser JSON parsing APIs. This API will not work with pseudo-JSON that must be parsed as JavaScript (such as that produced by encoding with [JSONEncoder.dateFormat](JSONEncoder.md#attr-jsonencoderdateformat) "dateConstructor" or "logicalDateConstructor").

This API is called "safe" because using a JavaScript eval() to decode JSON is potentially unsafe if the data being decoded is untrusted. For example, if users are able to save data as JSON for other uses to see (such as sharing [ListGrid.viewState](ListGrid_1.md#attr-listgridviewstate)) and there is no validation of the saved data to ensure safety and some users are untrusted, then saved JSON could be used similarly to an XSS attack, allowing one user to execute JavaScript code in another user's browser.

Note that, because JSON has no way of representing dates, serializing a structure that contains dates and then deserializing with decodeSafe() necessarily results in any Dates becoming strings. Use [JSONEncoder.dateFormat](JSONEncoder.md#attr-jsonencoderdateformat) "logicalDateString" in combination with [JSON.decodeSafeWithDates](#classmethod-jsondecodesafewithdates) to round-trip date, time and datetime values accurately.

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
Serialize an object as a JSON-like string by creating a [JSONEncoder](JSONEncoder.md#class-jsonencoder) and calling [JSONEncoder.encode](JSONEncoder.md#method-jsonencoderencode). The resulting string, which by default is **not** strict JSON, may be decoded back to objects via [JSON.decode](#classmethod-jsondecode).

There is an important caveat regarding Date values: for Date values to be decoded properly by decode(), it is required to use [dateFormat](JSONEncoder.md#attr-jsonencoderdateformat) "dateConstructor" or "logicalDateConstructor"; this causes Date values to be represented in the encoded string as JavaScript `new Date(...)` or [DateUtil.createLogicalDate](DateUtil.md#classmethod-dateutilcreatelogicaldate) calls, respectively.

**Strict JSON output**: to ensure output conforms to strict JSON (no unquoted keys or embedded JavaScript), pass settings like:

- isc.JSON.encode(data, {
- strictQuoting: true,          // quote all property names
- dateFormat: "xmlSchema",      // or "logicalDateString" for use with [JSON.decodeSafeWithDates](#classmethod-jsondecodesafewithdates)
- serializeInstances: "skip",   // skip instances of SmartClasses
- showDebugOutput: false        // avoid placeholders that are not valid JSON
- });
When strict JSON is desired, avoid dateFormats "dateConstructor" and "logicalDateConstructor", which embed JavaScript in the string output and therefore do not produce strict JSON.

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
Uses [JSON.decodeSafe](#classmethod-jsondecodesafe) to decode strict JSON using native browser JSON parsing APIs, with settings to correctly process formatted date values created with [JSONEncoder.dateFormat](JSONEncoder.md#attr-jsonencoderdateformat) "logicalDateString".

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| jsonString | [String](#type-string) | false | — | JSON data to be de-serialized |

---
