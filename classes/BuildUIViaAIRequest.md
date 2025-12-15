# BuildUIViaAIRequest Documentation

[← Back to API Index](../reference.md)

---

## Attr: BuildUIViaAIRequest.maxValidationRetries

### Description
The maximum numnber of re-attempts to have the AI fix a validation error.

**Flags**: IR

---
## Attr: BuildUIViaAIRequest.validationTypes

### Description
The types of validation to use on AI-generated JS code, in the order in which they should be applied.

**Flags**: IR

---
## Attr: BuildUIViaAIRequest.allowedUITypes

### Description
The list of allowed UI types.

A "UI type" string is usually not the same as the corresponding SmartClient component type name.

**Flags**: IR

---
## Attr: BuildUIViaAIRequest.customValidator

### Description
The custom validation routine to use. If this validator is supplied, but `"custom"` is not included among the [BuildUIViaAIRequest.validationTypes](#attr-builduiviaairequestvalidationtypes), then it is implicitly assumed that custom validation will be performed last.

**Flags**: IR

---
## Attr: BuildUIViaAIRequest.userAIRequest

### Description
The request from the user describing what UI they would like the AI to build.

**Flags**: IR

---
