# JSON Documentation

[← Back to API Index](../reference.md)

---

## Class: JSON

### Description
Utilities for working with JSON data.

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
