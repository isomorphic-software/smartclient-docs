# JSONSchemaSettings Documentation

[← Back to API Index](../reference.md)

---

## Attr: JSONSchemaSettings.editContext

### Description
Optional EditContext used to influence event/action schema by providing the set of live editing components and their types.

**Flags**: IR

---
## Attr: JSONSchemaSettings.eventMode

### Description
Controls how event handler properties are represented in the generated schema.

**Flags**: IR

---
## Attr: JSONSchemaSettings.annotationPrefix

### Description
Prefix for custom annotation keys added to the schema. Must start with `"x-"` per the JSON Schema specification.

**Flags**: IR

---
## Attr: JSONSchemaSettings.includeHidden

### Description
Whether to include fields marked `hidden:true` in the output schema.

**Flags**: IR

---
## Attr: JSONSchemaSettings.ruleScopeSource

### Description
Optional Canvas that provides a ruleScope. When set, the action binding schema enumerates valid target component IDs from [canvas.getRuleScopeDataBoundComponents](#method-canvasgetrulescopedataboundcomponents), and `*When` rules include valid field names from the ruleScope.

**Flags**: IR

---
## Attr: JSONSchemaSettings.includeDescriptions

### Description
Controls whether and at what granularity descriptions appear on schema properties. If unset, defaults to `"brief"` when brief descriptions are available (checked via `isc.jsdoc.hasBriefDescriptions()`), otherwise `"none"`.

**Flags**: IR

---
## Attr: JSONSchemaSettings.includeAdvanced

### Description
Whether to include fields marked `advanced:true` in the output schema.

**Flags**: IR

---
## Attr: JSONSchemaSettings.autoBindEvents

### Description
When true, event/action binding schemas omit the `"params"` property, relying on automatic parameter binding. Defaults to true when ISC\_Tools.js is loaded and JSDoc data is available.

**Flags**: IR

---
## Attr: JSONSchemaSettings.maxDepth

### Description
Maximum nesting depth for recursive DataSource discovery. Intended as an infinite-recursion guard; a [logWarn()](Class.md#method-classlogwarn) is issued if this depth is exceeded.

**Flags**: IR

---
## Attr: JSONSchemaSettings.cacheSchema

### Description
When true, the generated schema is cached on the DataSource, keyed by the JSON serialization of these settings. Subsequent calls with the same settings return the cached result. An empty settings object is cached by default regardless of this flag.

**Flags**: IR

---
## Attr: JSONSchemaSettings.includeWhenRules

### Description
Whether to include `visibleWhen`, `enableWhen`, `readOnlyWhen` and similar rules in the schema as annotations.

**Flags**: IR

---
## Attr: JSONSchemaSettings.includeValidators

### Description
Whether to output non-translatable validator information (such as custom validators) as annotations. Validators that have direct JSON Schema equivalents (minLength, maxLength, minimum, maximum, pattern, enum) are always translated structurally.

**Flags**: IR

---
## Attr: JSONSchemaSettings.omitDiscriminatedFields

### Description
When true, fields marked with [DataSourceField.typeDiscriminator](DataSourceField.md#attr-datasourcefieldtypediscriminator) whose resolved type is complex (a DataSource relationship) are omitted from the output schema entirely, instead of being expanded.

Intended for a two-step schema-driven flow: request schema with this setting enabled to obtain just the discriminator field(s), let the caller pick a value, then request schema again - without this setting, and now that the discriminator value is known - to obtain the field's full, unambiguous schema.

**Flags**: IR

---
## Attr: JSONSchemaSettings.asString

### Description
When true, `asJSONSchema()` returns the JSON Schema as a formatted JSON string instead of a plain object.

**Flags**: IR

---
## Attr: JSONSchemaSettings.useDefs

### Description
When true (the default), reusable DataSource types are placed in a `$defs` block and referenced via `$ref`. Set to false to use the older `definitions` keyword instead.

**Flags**: IR

---
