# UserFormula Documentation

[← Back to API Index](../main.md)

---

## Attr: UserFormula.text

### Description
Formula to be evaluated.

There are two contexts where a `UserFormula` is used: [ListGridField.userFormula](ListGridField.md#attr-listgridfielduserformula) / [DetailViewerField.userFormula](DetailViewerField.md#attr-detailviewerfielduserformula) and [FormItem.formula](FormItem.md#attr-formitemformula) or [ListGridField.editorFormula](ListGridField.md#attr-listgridfieldeditorformula). For the grid/detail viewer field formula, all variables used by the formula must be single capital letters (e.g. A). These are derived from field values for the record in question - see [UserFormula.formulaVars](#attr-userformulaformulavars).

In addition to these variables, the keyword `record` may be used to refer directly to the record for which the formula is being evaluated.

In the context of forms and editing, variables are dot-separated (.) names representing the nested hierarchy path to the desired value within the [rule context](Canvas.md#attr-canvasrulescope). No mapping with [UserFormula.formulaVars](#attr-userformulaformulavars) is needed.

The formula text must be valid JavaScript code and may only call either the built-in [math functions](MathFunction.md#class-mathfunction) or [custom functions](MathFunction.md#classmethod-mathfunctionregisterfunction).

This attribute is writable only in [ListGrid](ListGrid_1.md#class-listgrid)s. Applications must call either [ListGrid.setUserFormula](ListGrid_2.md#method-listgridsetuserformula) or [ListGrid.setUserFormulaText](ListGrid_2.md#method-listgridsetuserformulatext) to re-evaluate the formula.

**Flags**: IRW

---
## Attr: UserFormula.formulaVars

### Description
Object mapping from variable names to field names. All variable names must be single capital letters (e.g. A). For example, for a formula that should divide the field "population" over the field "area", the formula might be "E/L" and formula vars would be:
```
   {
       E: "population",
       L: "area"
   }
 
```

When used in the context of grid or detail viewer fields, field names are evaluated against the record.

When used in the context of forms and editing, this property is not used for formula mapping. Instead, field names are evaluated directly against the current [rule context](Canvas.md#attr-canvasrulescope).

Formulas built by a [FormulaBuilder](FormulaBuilder.md#class-formulabuilder) for a [ListGrid](ListGrid_1.md#class-listgrid) will normally not define this property and the field names will be used directly, unless [useSingleLetterKey](FormulaBuilder.md#attr-formulabuilderusesingleletterkey) is `true`. However, the Builder may add mapping keys to avoid collisions with registered [math functions](MathFunction.md#classmethod-mathfunctionregisterfunction). When directly using field names in a formula, any mapping keys you add to avoid collisions should contain the string "Field" so that the SmartClient Framework can detect when single-letter keys are not in use.

So, for example, if your grid contains a field "max" and you want to use it in a formula, your userFormula might look something like:

```
 {
     text: "max(maxField, 1000)",
     formulaVars: {
         maxField: "max"
     }
 }
```
.. where the formula also uses the built-in [math function](MathFunction.md#class-mathfunction) max().

**Flags**: IR

---
