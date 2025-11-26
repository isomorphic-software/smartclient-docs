# ValidatorDefinition Documentation

[← Back to API Index](../reference.md)

---

## Attr: ValidatorDefinition.action

### Description
[Callback](../reference.md#type-callback), function, or JavaScript expression called after every validation (i.e. call to [ValidatorDefinition.condition](#attr-validatordefinitioncondition)) whether it passed or failed. This allows the validator perform an operation on the field based on the validation outcome.

An `action()` function is not needed to report an error message only.

For the required parameters, see the documentation for [ValidatorActionCallback](Callbacks.md#method-callbacksvalidatoractioncallback).

**Flags**: IR

---
## Attr: ValidatorDefinition.condition

### Description
[Callback](../reference.md#type-callback), function or JavaScript expression invoked to perform the actual validation of a value.

Because the validator itself is passed as a parameter, you can effectively parameterize it. For example, to create a validator that checks that the value is after a certain date:

```
     { type:"custom", afterDate:new Date(), 
       condition:"value.getTime() > validator.afterDate.getTime()" }
 
```
Note that, if a field is declared with a builtin [FieldType](../reference_2.md#type-fieldtype), the value passed in will already have been converted to the specified type, if possible.

For the required parameters, see the documentation for [ValidatorConditionCallback](Callbacks.md#method-callbacksvalidatorconditioncallback).

**Flags**: IR

---
## Attr: ValidatorDefinition.shortName

### Description
Optional name to be shown in tools that edit validators. If not specified, the tools will derive the short name from the [ValidatorDefinition.type](#attr-validatordefinitiontype) by assuming it is camelCaps similar to [DataSource.getAutoTitle](DataSource.md#method-datasourcegetautotitle).

**Flags**: IR

---
## Attr: ValidatorDefinition.type

### Description
Type of the validator unique in [ValidatorType](../reference.md#type-validatortype).

**Flags**: IR

---
## Attr: ValidatorDefinition.requiresServer

### Description
Does this validator only run server-side?

**Flags**: IR

---
## Attr: ValidatorDefinition.defaultErrorMessage

### Description
Default error message to be shown when validator fails validation. Can be overridden for an individual validator by setting [Validator.errorMessage](Validator.md#attr-validatorerrormessage).

**Flags**: IR

---
