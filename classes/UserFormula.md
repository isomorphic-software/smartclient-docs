# UserFormula Documentation

[← Back to API Index](../reference.md)

---

## Attr: UserFormula.text

### Description
Formula to be evaluated.

There are two contexts where a UserFormula is used: [ListGridField.userFormula](ListGridField.md#attr-listgridfielduserformula) and [FormItem.formula](FormItem.md#attr-formitemformula) or [ListGridField.editorFormula](ListGridField.md#attr-listgridfieldeditorformula). For the grid field formula all variables used by the formula must be single-letter capital characters (eg A). These are derived from field values for the record in question - see [UserFormula.formulaVars](#attr-userformulaformulavars).

In addition to these variables, the keyword `record` may be used to refer directly to the record for which the formula is being displayed.

In the second usage context variables are dot-separated (.) names representing the nested hierarchy path to the desired value within the [rule context](Canvas.md#attr-canvasrulescope). No mapping with [UserFormula.formulaVars](#attr-userformulaformulavars) is needed.

The formula text must be valid JavaScript code and may only call either the built-in [MathFunctions](MathFunction.md#class-mathfunction) or a [custom\\n function](MathFunction.md#classmethod-mathfunctionregisterfunction).

**Flags**: IRW

---
## Attr: UserFormula.formulaVars

### Description
Object mapping from variable names to fieldNames. All variable names must be single-letter capital characters (eg A). For example, for a formula that should divide the field "population" over the field "area", the formula might be "E/L" and formula vars would be:
```
   {
       E: "population",
       L: "area"
   }
 
```

When used in [ListGridField.userFormula](ListGridField.md#attr-listgridfielduserformula) context, field names are evaluated against the grid record.

When used in [FormItem.formula](FormItem.md#attr-formitemformula) or [ListGridField.editorFormula](ListGridField.md#attr-listgridfieldeditorformula) this property is not used for formula mapping. Instead, field names are evaluated directly against the current [rule context](Canvas.md#attr-canvasrulescope).

**Flags**: IR

---
