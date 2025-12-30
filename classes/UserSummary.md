# UserSummary Documentation

[← Back to API Index](../reference.md)

---

## Attr: UserSummary.text

### Description
Summary to be evaluated.

There are two contexts where a UserSummary is used: [ListGridField.userSummary](ListGridField.md#attr-listgridfieldusersummary) and [FormItem.textFormula](FormItem.md#attr-formitemtextformula) or [ListGridField.editorTextFormula](ListGridField.md#attr-listgridfieldeditortextformula). For the grid field summary all variables used by the summary must be all-capital letter names surrounded by braces and escaped with a # sign (eg #{A}). These are derived from field values for the record in question - see [UserSummary.summaryVars](#attr-usersummarysummaryvars).

In the second usage context variables are dot-separated (.) names representing the nested hierarchy path to the desired value within the [rule context](Canvas.md#attr-canvasrulescope). No mapping with [UserSummary.summaryVars](#attr-usersummarysummaryvars) is needed.

**Flags**: IRW

---
## Attr: UserSummary.summaryVars

### Description
Map from the all-capital letter names used as summary variables in the [UserSummary](../reference_2.md#object-usersummary) String to the fieldNames these variables should represent in the context where the summary is evaluated.

When used in [ListGridField.userSummary](ListGridField.md#attr-listgridfieldusersummary) context, field names are evaluated against the grid record.

When used in [FormItem.textFormula](FormItem.md#attr-formitemtextformula) or [ListGridField.editorTextFormula](ListGridField.md#attr-listgridfieldeditortextformula) this property is not used for summary mapping. Instead, field names are evaluated directly against the current [rule context](Canvas.md#attr-canvasrulescope).

**Flags**: IR

---
