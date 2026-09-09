# DynamicProperty Documentation

[← Back to API Index](../reference.md)

---

## Attr: DynamicProperty.formula

### Description
A numeric [formula](UserFormula.md#attr-userformulatext) expression, written in terms of `#{path}` references into the current [rule context](Canvas.md#attr-canvasrulescope) (for example `"#{form.values.quantity} * #{form.values.unitPrice}"`). Re-evaluated every time any referenced path changes.

By default the result is assumed to be numeric: if the formula ever evaluates to something else, the property is left unset rather than receiving a bad value. Set [type](#attr-dynamicpropertytype) to accept a non-numeric result -- see [DynamicProperty.type](#attr-dynamicpropertytype) for details.

A [UserFormula](../reference.md#object-userformula) object (`{text, formulaVars}`) is also accepted as shorthand in place of a plain string, with `formulaVars` substituted into the formula text before evaluation.

Formulas (and [templates](#attr-dynamicpropertytemplate)) are compiled to JavaScript functions, so a Content Security Policy that forbids dynamic code generation disables them — see [cspSupport](../kb_topics/cspSupport.md#kb-topic-content-security-policy-csp).

### See Also

- [cspSupport](../kb_topics/cspSupport.md#kb-topic-content-security-policy-csp)

**Flags**: IR

---
## Attr: DynamicProperty.trueWhen

### Description
[AdvancedCriteria](../reference.md#object-advancedcriteria) evaluated against the current [rule context](Canvas.md#attr-canvasrulescope); the property is set to the boolean result (`true` if the criteria matches, `false` otherwise), re-evaluated every time the rule context changes. Always produces a boolean; [type](#attr-dynamicpropertytype) does not apply.

In ComponentXML, the criteria can be nested under any of ``<criteria>``, ``<Criteria>``, ``<advancedCriteria>``, or ``<AdvancedCriteria>`` -- whichever reads most naturally at the call site.

**Flags**: IR

---
## Attr: DynamicProperty.textFormula

### Description
Deprecated legacy form of [template](#attr-dynamicpropertytemplate): a [UserSummary](../reference.md#object-usersummary) object (`{text, summaryVars}`) rather than a plain template string. Use [template](#attr-dynamicpropertytemplate) instead.

**Flags**: IR

---
## Attr: DynamicProperty.name

### Description
Name of the property this source applies to.

Required when [Class.dynamicProperties](Class.md#attr-classdynamicproperties) is declared as an array (`dynamicProperties: [ {name: "...", ...} ]`) or in ComponentXML (``<property name="..."/>``). Not needed -- and ignored if present -- in the map form of [Class.dynamicProperties](Class.md#attr-classdynamicproperties), where the map key already supplies the name, nor when passed to [addDynamicProperty()](Class.md#method-classadddynamicproperty), which takes the property name as a separate leading argument.

**Flags**: IR

---
## Attr: DynamicProperty.dataPath

### Description
A [DataPath](../reference_2.md#type-datapath) into the current [rule context](Canvas.md#attr-canvasrulescope). The property is set to whatever value the path currently resolves to, re-evaluated every time that part of the rule context changes.

Unlike a [component-level dataPath](Canvas.md#attr-canvasdatapath), which is always slash-delimited, a dataPath into the rule context accepts either `.` or `/` as the segment separator with no difference in behavior -- see [Canvas.provideRuleContext](Canvas.md#method-canvasproviderulecontext) for the exact rule. Dot-separated paths such as `"grid.selectedRecord.name"` are preferred: they read like the equivalent JavaScript property access and match the style used throughout [Dynamic Properties](../kb_topics/dynamicProperties.md#kb-topic-dynamic-properties) and its examples.

### See Also

- [Canvas.provideRuleContext](Canvas.md#method-canvasproviderulecontext)

**Flags**: IR

---
## Attr: DynamicProperty.type

### Description
SimpleType name (for example `"text"`, `"boolean"`, `"integer"`, `"float"`, `"date"` -- see [FieldType](../reference_2.md#type-fieldtype) for the full built-in list) that the resolved value is coerced into before being assigned to the property, or the special value `"any"` (alias `"raw"`) to assign the resolved value with its native JavaScript type unchanged, bypassing coercion entirely.

Only meaningful for the [dataPath](#attr-dynamicpropertydatapath), [formula](#attr-dynamicpropertyformula), and [valueFrom](#attr-dynamicpropertyvaluefrom) forms; ignored for [template](#attr-dynamicpropertytemplate) (always a string) and [trueWhen](#attr-dynamicpropertytruewhen) (always a boolean).

For the [formula](#attr-dynamicpropertyformula) form specifically, omitting `type` means the result is assumed to be numeric: a non-numeric result is discarded and the property is left unset, rather than receiving the bad value. Set `type` (to `"text"`, `"boolean"`, `"any"`, or similar) whenever the formula's result is not purely numeric. The [dataPath](#attr-dynamicpropertydatapath) and [valueFrom](#attr-dynamicpropertyvaluefrom) forms have no such default assumption -- their resolved value passes through unchanged when `type` is omitted.

**Flags**: IR

---
## Attr: DynamicProperty.valueFrom

### Description
Ordered list of [ValueFromMapping](../reference.md#object-valuefrommapping) cases, each pairing an optional [AdvancedCriteria](../reference.md#object-advancedcriteria) guard with a value to use when that guard matches. Cases are evaluated in array order; the property is set from the first case whose criteria matches the current [rule context](Canvas.md#attr-canvasrulescope), or the first case with no criteria at all (which therefore always matches, and so serves as the default), re-evaluated every time the rule context changes.

Use [type](#attr-dynamicpropertytype) if the resolved values are not plain strings.

**Flags**: IR

---
## Attr: DynamicProperty.template

### Description
A text [template](UserSummary.md#attr-usersummarytext), written in terms of `#{path}` references into the current [rule context](Canvas.md#attr-canvasrulescope) that are substituted into the surrounding string (for example `"Editing: #{grid.selectedRecord.name}"`). Re-evaluated, and the resulting string reapplied, every time any referenced path changes. Always produces a string; [type](#attr-dynamicpropertytype) does not apply.

A [UserSummary](../reference.md#object-usersummary) object (`{text, summaryVars}`) is also accepted as shorthand in place of a plain string, with `summaryVars` substituted into the template text before evaluation. See [DynamicProperty.textFormula](#attr-dynamicpropertytextformula) for the older, deprecated field name this shorthand is normalized through internally.

Templates (like [formulas](#attr-dynamicpropertyformula)) are compiled to JavaScript functions, so a Content Security Policy that forbids dynamic code generation disables them — see [cspSupport](../kb_topics/cspSupport.md#kb-topic-content-security-policy-csp).

### See Also

- [cspSupport](../kb_topics/cspSupport.md#kb-topic-content-security-policy-csp)

**Flags**: IR

---
