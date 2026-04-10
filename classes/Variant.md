# Variant Documentation

[← Back to API Index](../reference.md)

---

## Class: Variant

### Description
Singleton class with static (class-level) APIs for managing the skin variant registry. Variants are named sets of property overrides applied to a base SmartClient class to change its visual appearance without altering behavior.

See [skinVariant](#groupdef-skinvariant) for an overview of the variant system and [VariantDefinition](../reference.md#object-variantdefinition) for the definition format.

---
## ClassMethod: Variant.getVariants

### Description
Get all variant definitions registered for a given target class.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| targetClass | [String](#type-string) | false | — | SmartClient class name |

### Returns

`[Array of VariantDefinition](#type-array-of-variantdefinition)` — matching definitions

---
## ClassMethod: Variant.getVariantNames

### Description
Get the names of all registered variants.

### Returns

`[Array of String](#type-array-of-string)` — variant names

---
## ClassMethod: Variant.getVariant

### Description
Get a registered variant definition by name.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | variant name |

### Returns

`[VariantDefinition](#type-variantdefinition)` — the definition, or null

---
## ClassMethod: Variant.createSubclasses

### Description
Create subclasses from all registered variant definitions. Called automatically after all definitions are registered.

For each variant, creates a named subclass of the target class. Grid variants with multiple target classes create a subclass for each (e.g. `CompactGrid` and `CompactTreeGrid`).

Properties ending in `"Defaults"` or `"Properties"` are merged via [Class.changeDefaults](Class.md#classmethod-classchangedefaults) to preserve superclass AutoChild settings.

---
## ClassMethod: Variant.register

### Description
Register a [VariantDefinition](../reference.md#object-variantdefinition). The variant's subclass is created immediately if framework classes are available, otherwise during [Variant.createSubclasses](#classmethod-variantcreatesubclasses).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| definition | [VariantDefinition](#type-variantdefinition) | false | — | variant to register |

---
## ClassMethod: Variant.registerAll

### Description
Register multiple [VariantDefinitions](../reference.md#object-variantdefinition) at once.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| definitions | [Array of VariantDefinition](#type-array-of-variantdefinition) | false | — | variants |

---
