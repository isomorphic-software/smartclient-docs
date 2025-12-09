# CoTTransition Documentation

[← Back to API Index](../reference.md)

---

## Attr: CoTTransition.label

### Description
Optional UI label override. If omitted, the target's [description](CoTTask.md#attr-cottaskdescription) is used if present, otherwise [CoTTask.title](#cottasktitle).

**Flags**: IR

---
## Attr: CoTTransition.visibleWhen

### Description
Conditional visibility for this transition, evaluated with the same semantics as [Canvas.visibleWhen](Canvas.md#attr-canvasvisiblewhen). When false, the transition is treated as unavailable: it is omitted from prompt fragments (see ["transitions"](CoTProcess.md#method-cotprocessgetpromptpart)) and hidden from any UI that lists transitions. If the AI attempts to use a non-visible transition (e.g., emits {goTo} to this target) resulting in a validation error and a retry.

**Evaluation context**  
The expression is evaluated against the process [ruleScope](Process.md#attr-processrulescope). In addition, the special identifier `state` is prebound to `process.state`

**Examples**

```
 // Only show "addField" while total fields < 50
 visibleWhen: {
   operator:"lessThan",
   fieldName:"state.currentDS.fields.length",
   value:50
 }

 // Hide "done" unless we've added at least one field in this run
 visibleWhen: {
   operator:"isNotNull",
   fieldName:"state.lastCreatedField"
 }

 // Require both a DataSource and at least 1 field
 visibleWhen: {
   operator:"and",
   criteria:[
     { fieldName:"state.currentDS", operator:"isNotNull" },
     { fieldName:"state.currentDS.fields.length", operator:"greaterThan", value:0 }
   ]
 }
 
```

**Flags**: IR

---
## Attr: CoTTransition.to

### Description
ID of the target task.

**Flags**: IR

---
