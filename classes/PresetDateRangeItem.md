# PresetDateRangeItem Documentation

[← Back to API Index](../main.md)

---

## Class: PresetDateRangeItem

*Inherits from:* [PresetCriteriaItem](PresetCriteriaItem.md#class-presetcriteriaitem)

### Description
Allows the user to pick from pre-set date ranges or choose a custom date range via a [DateRangeDialog](DateRangeDialog.md#class-daterangedialog).

To use this item in the [FilterEditor](ListGrid_1.md#attr-listgridshowfiltereditor) or [FilterBuilder](FilterBuilder.md#class-filterbuilder), create a trivial [subclass](ClassFactory.md#classmethod-classfactorydefineclass) which defines [preset options](PresetCriteriaItem.md#attr-presetcriteriaitemoptions), then set [ListGridField.filterEditorType](ListGridField.md#attr-listgridfieldfiltereditortype) to use this class with the FilterEditor, or define a custom operator and set [Operator.editorType](Operator.md#attr-operatoreditortype) to use it with the FilterBuilder.

See the *Date Range (Presets)* example for sample code.

---
## Method: PresetDateRangeItem.getCriterion

### Description
Get the criterion based on the value selected by the user.

### Returns

`[Criterion](#type-criterion)|[AdvancedCriteria](#type-advancedcriteria)` — the criteria for the selected option

---
