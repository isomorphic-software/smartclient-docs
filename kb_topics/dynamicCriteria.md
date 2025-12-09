# dynamicCriteria

[← Back to API Index](../reference.md)

---

## KB Topic: dynamicCriteria

### Description
If a property indicates it has support for "dynamic criteria" it means that values in the criteria may be dynamically derived from the current [Canvas.ruleScope](../classes/Canvas.md#attr-canvasrulescope) using [Criterion.valuePath](../classes/Criterion.md#attr-criterionvaluepath).

In other words, it allows criteria to be declared using values from nearby drawn components, via the [Canvas.ruleScope](../classes/Canvas.md#attr-canvasrulescope). Values are pulled from the ruleScope via setting [Criterion.valuePath](../classes/Criterion.md#attr-criterionvaluepath) When values drawn from the ruleScope change, the component where dynamicCriteria is declared will be notified and automatically use the new value

```
 isc.DynamicForm.create({
    ID: "theForm",
    items:[{
        name: "lifeSpan",
        type: "text",
        title: "LifeSpan",
        defaultValue: "45"}]
 });

 isc.ListGrid.create({
    width:300, height: 400, top: 50,
    dataSource: "animals",
    initialCriteria: { fieldName:"lifeSpan", operator:"greaterThan", valuePath:"theForm.values.lifeSpan"}
 });

 
```

---
