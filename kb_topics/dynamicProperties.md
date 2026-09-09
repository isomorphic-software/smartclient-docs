# Dynamic Properties

[← Back to API Index](../reference.md)

---

## KB Topic: Dynamic Properties

### Description
Dynamic properties are SmartClient's general-purpose mechanism for keeping any settable property of any component -- or of a FormItem -- automatically synchronized with live application state, using nothing but declarative configuration: no event handlers, no "value changed" wiring, no manual re-render calls to write or maintain.

Every form draws its live values from the same place: the current [rule context](../classes/Canvas.md#attr-canvasrulescope) -- the same aggregated, continuously-updated record that drives other criteria-based rules such as [FormItem.visibleWhen](../classes/FormItem.md#attr-formitemvisiblewhen) and [ListGrid.initialCriteria](../classes/ListGrid_1.md#attr-listgridinitialcriteria). A single dynamic property can:

*   pull a value from a [DataPath](../reference_2.md#type-datapath) anywhere in the rule context
*   compute a numeric [formula](../classes/UserFormula.md#attr-userformulatext) from several rule context values at once
*   build a text [template](../classes/UserSummary.md#attr-usersummarytext) that substitutes rule context values into a string
*   evaluate an [AdvancedCriteria](../reference.md#object-advancedcriteria) business rule against the rule context, producing a boolean
*   pick between several such alternatives, using the first whose criteria currently matches the rule context (the `valueFrom` form)

See [DynamicProperty](../reference_2.md#object-dynamicproperty) for the full set of forms and fields, including a convenient shorthand syntax for each. Whichever form is used, the property is applied immediately when declared, then transparently kept up to date every time any part of the rule context it depends on changes -- across components, across forms, across grids -- with all dependency tracking and re-evaluation handled by the [rules engine](dynamicCriteria.md#kb-topic-dynamiccriteria). The same mechanism scales from a single label that shows a live total, to entire pages of cross-field, cross-component business logic that would otherwise take substantial custom event-handling code to build and keep correct.

A dynamic property is declared either via [dynamicProperties](../classes/Class.md#attr-classdynamicproperties) (several properties at once) or [addDynamicProperty()](../classes/Class.md#method-classadddynamicproperty) (one property, programmatically).

[Dynamic templates](dynamicTemplates.md#kb-topic-dynamic-templates) -- the {expr} syntax embeddable directly in string-typed properties such as [Button.title](../classes/Button.md#attr-buttontitle) -- are syntactic sugar layered on top of dynamic properties: each {expr} template compiles to a dynamic property behind the scenes, so it is tracked and re-evaluated through this exact same mechanism, not a separate one. Reach for a dynamic template for a quick inline string substitution; declare a dynamic property directly, via [dynamicProperties](../classes/Class.md#attr-classdynamicproperties) or [addDynamicProperty()](../classes/Class.md#method-classadddynamicproperty), when the target property is not string-typed, when the source is a criteria/formula/valueFrom rather than a simple template, or when the configuration is more naturally produced as data than typed as an expression (for example when building it visually with Reify).

Because dynamicProperties are entirely declarative -- plain configuration data rather than code -- they are also fully visible and editable visually in [Reify](reify.md#kb-topic-reify-overview): any writable String, numeric, boolean, or enum property exposed in the Reify component editor can be switched to a dynamic property directly from that property's own editor, using the same DataPath / Formula / Template / Criteria / valueFrom choices documented under [DynamicProperty](../reference_2.md#object-dynamicproperty), without writing or generating a single line of code. Reify's AI assistant can produce the same declarations directly from a plain-language description of the desired behavior (for example "show the order total from the line items grid" or "highlight this field when the account is over its credit limit"), because the result is just more dynamicProperties -- indistinguishable from one written by hand.

**Scope and limitations**

*   Any [Class](../classes/Class.md#class-class) can have dynamic properties, not just a [Canvas](../classes/Canvas.md#class-canvas). A non-Canvas class must name its ruleScope explicitly via [Class.ruleScope](../classes/Class.md#attr-classrulescope) — there is no parent chain to search. A [FormItem](../classes/FormItem.md#class-formitem) inherits its form's ruleScope, and its rules are managed by that form.
*   The target property must be runtime settable, since the new value is applied by calling the property's setter. Declaring a dynamic property on a create-time-only property is invalid and has no effect; no error is thrown and no warning is logged.
*   Declaring a dynamic property for a property that is already dynamic replaces the previous declaration. [Class.clearDynamicProperty](../classes/Class.md#method-classcleardynamicproperty) stops further updates but leaves the property at its current value.
*   For showing, hiding, enabling and setting components read-only, prefer the dedicated [visibleWhen](../classes/Canvas.md#attr-canvasvisiblewhen), [enableWhen](../classes/Canvas.md#attr-canvasenablewhen) and [readOnlyWhen](../classes/FormItem.md#attr-formitemreadonlywhen) properties — they express the same idea more directly and carry component-specific behavior.
*   Formulas and templates are compiled to JavaScript functions, so a Content Security Policy that forbids dynamic code generation disables them — see [cspSupport](cspSupport.md#kb-topic-content-security-policy-csp).
*   A [dataPath](../classes/DynamicProperty.md#attr-dynamicpropertydatapath) into the rule context accepts either `.` or `/` as the segment separator, with no difference in behavior — see [Canvas.provideRuleContext](../classes/Canvas.md#method-canvasproviderulecontext). Dot-separated paths are preferred since they read like the equivalent JavaScript property access.

**Examples**

A few of the many practical uses for dynamic properties follow; each is a small, complete, working configuration.

**1\. A value computed live from another component (DataPath)**  
A read-only order-total field that always reflects the sum of a grid's line items, with no code involved at all:

```
 isc.ListGrid.create({
     ID: "lineGrid",
     showGridSummary: true,
     fields: [
         { name: "item", type: "text" },
         { name: "lineTotal", type: "float", showGridSummary: true,
           summaryFunction: "sum" }
     ],
     data: [ { item: "Widget", lineTotal: 10 }, { item: "Gadget", lineTotal: 25 } ]
 });
 isc.DynamicForm.create({
     ID: "orderForm",
     fields: [
         { name: "orderTotal", type: "float", canEdit: false,
           dynamicProperties: {
               defaultValue: { dataPath: "lineGrid.summaryRecord.lineTotal" }
           }
         }
     ]
 });
 
```
Editing any line item recalculates the grid's summary row, which in turn recalculates `orderTotal` -- no "value changed" handler is involved on either component.

**2\. Contextual text driven by another component's selection (template)**  
A panel header that names whichever customer is currently selected in a grid:

```
 isc.Label.create({
     ID: "headerLabel",
     dynamicProperties: {
         contents: { template: "Editing: #{custGrid.selectedRecord.name}" }
     }
 });
 
```
The label's text updates the instant the grid selection changes, with the template able to combine any number of [DataPath](../reference_2.md#type-datapath)s from anywhere in the rule context, not just the one component.

**3\. Tiered business rules with no code at all (valueFrom)**  
A status badge whose text is chosen from a set of business tiers, each guarded by its own [AdvancedCriteria](../reference.md#object-advancedcriteria), evaluated top to bottom:

```
 isc.Label.create({
     ID: "tierBadge",
     dynamicProperties: {
         contents: { valueFrom: [
             { value: "Gold Tier", criteria: {
                 fieldName: "totalForm.values.orderTotal", operator: "greaterOrEqual",
                 value: 1000
             } },
             { value: "Silver Tier", criteria: {
                 fieldName: "totalForm.values.orderTotal", operator: "greaterOrEqual",
                 value: 100
             } },
             { value: "Standard" }
         ] }
     }
 });
 
```
As the order total in `totalForm` changes, the badge automatically reclassifies itself -- the same pattern applies equally well to `backgroundColor`, `icon`, or any other settable property, so a whole family of tiered visual indicators can be built purely declaratively. See also the *Boolean Dynamic Properties* sample, which uses the related `trueWhen` form to drive boolean properties from criteria.

**4\. Driving a plain layout property that has no dedicated shortcut (formula)**  
Dynamic properties are not limited to a component's value or contents -- any settable property can be computed live, including ordinary layout properties like `width` that have no dedicated formula/template/criteria shortcut of their own. Here a plain Canvas becomes a live "budget used" progress bar, with no ProgressBar widget and no code:

```
 isc.DynamicForm.create({
     ID: "budgetForm",
     fields: [
         { name: "spent", type: "float", defaultValue: 400 },
         { name: "budget", type: "float", defaultValue: 1000 }
     ]
 });
 isc.Canvas.create({
     ID: "usageBar",
     height: 16,
     backgroundColor: "#4CAF50",
     dynamicProperties: {
         width: {
             formula: "(#{budgetForm.values.spent} / #{budgetForm.values.budget}) * 200"
         }
     }
 });
 
```
The bar resizes the instant `spent` or `budget` changes, with no "value changed" handler on either component -- this works precisely because dynamicProperties targets `width` directly, rather than a component's value the way a dedicated formula shortcut such as [FormItem.formula](../classes/FormItem.md#attr-formitemformula) would. Note that a bare numeric `formula` like this one is coerced back to `undefined` if it ever evaluates to something non-numeric; see [DynamicProperty.type](../classes/DynamicProperty.md#attr-dynamicpropertytype) for how to opt out of that coercion.

---
