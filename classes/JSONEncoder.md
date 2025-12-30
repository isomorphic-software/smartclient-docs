# JSONEncoder Documentation

[← Back to API Index](../reference.md)

---

## Class: JSONEncoder

### Description
Class for encoding objects as JSON strings.

---
## Attr: JSONEncoder.strictQuoting

### Description
Whether all property names should be quoted, or only those property names that are not valid identifiers or are JavaScript reserved words (such as "true").

Encoding only where required produces slightly shorter, more readable output which is still compatible with JavaScript's eval():

```
 {
     someProp : "someValue",
     "true" : "otherValue",
     otherProp : "otherValue"
 }
 
```
.. but is not understood by many server-side JSON parser implementations.

**Flags**: IR

---
## Attr: JSONEncoder.prettyPrint

### Description
Whether to add indentation to the returned JSON string. This makes the returned JSON much easier to read but adds size. Note that when delivering JSON responses compressed, the size difference between prettyPrinted JSON and normal JSON is negligible.

**Flags**: IR

---
## Attr: JSONEncoder.circularReferenceMode

### Description
What the JSONEncoder should do if it encounters a circular reference.

**Flags**: IR

---
## Attr: JSONEncoder.dateFormat

### Description
Format for encoding JavaScript Date values in JSON. See [JSONDateFormat](../reference.md#type-jsondateformat) for valid options, or override [JSONEncoder.encodeDate](#method-jsonencoderencodedate) to do something custom.

**Flags**: IR

---
## Attr: JSONEncoder.serializeInstances

### Description
Controls the output of the JSONEncoder when instances of SmartClient classes (eg a ListGrid) are included in the data to be serialized. See [JSONInstanceSerializationMode](../reference.md#type-jsoninstanceserializationmode).

Note that the JSONEncoder does not support a format that will recreate the instance if passed to decode() or eval().

**Flags**: IR

---
## Attr: JSONEncoder.showDebugOutput

### Description
If objects that cannot be serialized to JSON are encountered during serialization, show a placeholder rather than just omitting them.

The resulting String will not be valid JSON and so cannot be decoded/eval()'d

**Flags**: IR

---
## Attr: JSONEncoder.skipInternalProperties

### Description
If true, don't show SmartClient internal properties when encoding and object.

**Flags**: IR

---
## Attr: JSONEncoder.escapeNonPrintable

### Description
By default, obscure non-printable characters such as DC3 (Device Control 3, U+0013 hexadecimal) will be escaped according to JSON standards. ECMA-404 / The JSON Data Interchange Format requires the quotation mark (U+0022), reverse solidus (U+005C), and control characters (U+0000 through U+001F) to be escaped.

These characters are very rarely used in JSON data in web applications. If you know that your application does not use such characters in JSON data, there can be a performance advantage to setting `escapeNonPrintable` to false in order to disable the logic for escaping these characters. This is a detectable difference only when dealing with very large JSON structures on older browsers that do not provide native support (for example, Internet Explorer 8).

**Flags**: IRW

---
## Attr: JSONEncoder.circularReferenceMarker

### Description
The string marker used to represent circular references. See [JSONEncoder.circularReferenceMode](#attr-jsonencodercircularreferencemode).

**Flags**: IR

---
## Method: JSONEncoder.encodeDate

### Description
Encode a JavaScript Date value.

By default, follows the [JSONEncoder.dateFormat](#attr-jsonencoderdateformat) setting. Override to do custom encoding.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| theDate | [Date](#type-date) | false | — | JavaScript date object to be serialized |

### Returns

`[String](#type-string)` — value to be included in result. **If this value is intended to appear as a String it should include quotes (")**

---
## Method: JSONEncoder.encode

### Description
Serialize an object as a JSON string.

Automatically handles circular references - see [JSONEncoder.circularReferenceMode](#attr-jsonencodercircularreferencemode).

Note that using the String produced by this API with [JSON.decode](JSON.md#classmethod-jsondecode) **will not successfully preserve dates**. Use [JSONEncoder.dateFormat](#attr-jsonencoderdateformat) "dateConstructor" or "logicalDateConstructor" to have dates round-trip properly.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Any](#type-any) | false | — | object to serialize |

### Returns

`[String](#type-string)` — object encoded as a JSON String

---
