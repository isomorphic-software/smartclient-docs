# ValueFromMapping Documentation

[← Back to API Index](../reference.md)

---

## Attr: ValueFromMapping.value

### Description
Literal value to use when this case's [criteria](#attr-valuefrommappingcriteria) matches (or when this case has no criteria and so is the default). Ignored if [dataPath](#attr-valuefrommappingdatapath), [formula](#attr-valuefrommappingformula), or [template](#attr-valuefrommappingtemplate) is also set on this case.

**Flags**: IR

---
## Attr: ValueFromMapping.template

### Description
Text template to evaluate, when this case matches. See [DynamicProperty.template](DynamicProperty.md#attr-dynamicpropertytemplate).

**Flags**: IR

---
## Attr: ValueFromMapping.formula

### Description
Numeric formula to evaluate, when this case matches. See [DynamicProperty.formula](DynamicProperty.md#attr-dynamicpropertyformula).

**Flags**: IR

---
## Attr: ValueFromMapping.dataPath

### Description
DataPath to read the value from, when this case matches. See [DynamicProperty.dataPath](DynamicProperty.md#attr-dynamicpropertydatapath).

**Flags**: IR

---
## Attr: ValueFromMapping.criteria

### Description
Criteria that must match the current [rule context](Canvas.md#attr-canvasrulescope) for this case to apply. Omit to declare the default case -- the one used when no earlier case in the [valueFrom](DynamicProperty.md#attr-dynamicpropertyvaluefrom) array matches.

**Flags**: IR

---
