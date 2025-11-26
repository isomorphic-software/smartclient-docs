# AIFieldRequest Documentation

[← Back to API Index](../reference.md)

---

## Attr: AIFieldRequest.valueClass

### Description
The class of value that AI will be asked to generate for the field.

**Flags**: IR

---
## Attr: AIFieldRequest.minValue

### Description
If the [AIFieldRequest.valueClass](#attr-aifieldrequestvalueclass) is "interval" or "ratio", the minimum value that can be generated. If `null`, then there is no minimum.

**Flags**: IR

---
## Attr: AIFieldRequest.relevantFieldNames

### Description
The names of fields that are relevant to each [SummarizeRecordsRequest](#object-summarizerecordsrequest).

**Flags**: IR

---
## Attr: AIFieldRequest.maxValue

### Description
If the [AIFieldRequest.valueClass](#attr-aifieldrequestvalueclass) is "interval" or "ratio", the maximum value that can be generated. If `null`, then there is no maximum.

**Flags**: IR

---
## Attr: AIFieldRequest.categories

### Description
If the [AIFieldRequest.valueClass](#attr-aifieldrequestvalueclass) is "categorical" or "ordinal" , the list of available categories.

**Flags**: IR

---
## Attr: AIFieldRequest.sortDirection

### Description
The suggested initial sort direction for the field.

**Flags**: IR

---
