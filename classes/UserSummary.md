# UserSummary Documentation

[← Back to API Index](../reference.md)

---

## Attr: UserSummary.text

### Description
Summary to be evaluated.

There are two contexts where a `UserSummary` is used: [ListGridField.userSummary](ListGridField.md#attr-listgridfieldusersummary) / [DetailViewerField.userSummary](DetailViewerField.md#attr-detailviewerfieldusersummary) and [FormItem.textFormula](FormItem.md#attr-formitemtextformula) or [ListGridField.editorTextFormula](ListGridField.md#attr-listgridfieldeditortextformula). For the grid/detail viewer field summary, all variables used by the summary must be single capital letters surrounded by braces and escaped with a # sign (e.g. #{A}). These are derived from field values for the record in question - see [UserSummary.summaryVars](#attr-usersummarysummaryvars).

In the context of forms and editing, variables are dot-separated (.) names representing the nested hierarchy path to the desired value within the [rule context](Canvas.md#attr-canvasrulescope). No mapping with [UserSummary.summaryVars](#attr-usersummarysummaryvars) is needed.

This attribute is writable only in [ListGrid](ListGrid_1.md#class-listgrid)s. Applications must call either [ListGrid.setUserSummary](ListGrid_2.md#method-listgridsetusersummary) or [ListGrid.setUserSummaryText](ListGrid_2.md#method-listgridsetusersummarytext) to re-evaluate the summary.

**Flags**: IRW

---
## Attr: UserSummary.summaryVars

### Description
Map from the single capital letters used as summary variables in the [UserSummary](../reference.md#object-usersummary) String to the field names these variables should represent.

When used in the context of grid or detail viewer fields, field names are evaluated against the record.

Summaries built by a [SummaryBuilder](SummaryBuilder.md#class-summarybuilder) for a [ListGrid](ListGrid_1.md#class-listgrid) will normally not define this property and the field names will be used directly, unless [useSingleLetterKey](FormulaBuilder.md#attr-formulabuilderusesingleletterkey) is `true`. This property is also not used for summary mapping in [FormItem.textFormula](FormItem.md#attr-formitemtextformula) or [ListGridField.editorTextFormula](ListGridField.md#attr-listgridfieldeditortextformula). Instead, field names are evaluated directly against the current [rule context](Canvas.md#attr-canvasrulescope).

**Flags**: IR

---
