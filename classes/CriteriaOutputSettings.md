# CriteriaOutputSettings Documentation

[← Back to API Index](../reference.md)

---

## Attr: CriteriaOutputSettings.quoteTextValues

### Description
When set, values of substring-style operators such as "contains" or "startsWith" (including their case-insensitive and negated variants - any operator declaring [textMatch](Operator.md#attr-operatortextmatch)) are surrounded with double quotes in the output, so a value containing the words "and" or "or" cannot read as a further clause of the sentence. When unset, values appear unquoted.

**Flags**: IR

---
## Attr: CriteriaOutputSettings.suffix

### Description
Suffix to be appended to each criterion description.

**Flags**: IR

---
## Attr: CriteriaOutputSettings.textMatchStyle

### Description
[TextMatchStyle](../reference_2.md#type-textmatchstyle) to use if converting from a simple criteria. This property, if specified, is passed to [convertCriteria](DataSource.md#classmethod-datasourceconvertcriteria) to override the default.

**Flags**: IR

---
## Attr: CriteriaOutputSettings.prefix

### Description
Prefix to be prepended to each criterion description.

**Flags**: IR

---
## Attr: CriteriaOutputSettings.escapeHTML

### Description
By default HTML characters such as `"`<br>`"` will be written into the output description to format the result. Setting `escapeHTML` true will instead force HTML values in the output to be displayed to the user instead.

**Flags**: IR

---
