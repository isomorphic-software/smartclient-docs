# GridEditRecordTask Documentation

[← Back to API Index](../reference.md)

---

## Class: GridEditRecordTask

*Inherits from:* [ComponentTask](ComponentTask.md#class-componenttask)

### Description
Edit an existing record in a grid or start editing a new one. A new record is added unless [criteria](#attr-grideditrecordtaskcriteria) is specified. Alternatively, if [editFirstRecord](#attr-grideditrecordtaskeditfirstrecord) is specified, the first record is edited.

If criteria is provided and the criteria matches more than one record, the first matched record is edited. Additionally, if the record to be edited is not visible, the record will be scrolled into view.

Note that the record to be matched must already be loaded in the grid - no fetch will be performed.

### See Also

- [ListGrid.editExistingRecord](ListGrid_2.md#method-listgrideditexistingrecord)
- [ListGrid.startEditingNew](ListGrid_2.md#method-listgridstarteditingnew)

---
## Attr: GridEditRecordTask.initialValues

### Description
Initial values for a new edit record.

Data values prefixed with "$" will be treated as a [TaskInputExpression](../reference_2.md#type-taskinputexpression) excluding "$input" and "$inputRecord" references.

**Flags**: IR

---
## Attr: GridEditRecordTask.editFirstRecord

### Description
When neither [GridEditRecordTask.initialValues](#attr-grideditrecordtaskinitialvalues) nor [Criteria](../reference_2.md#type-criteria) are provided should the first record in the grid be edited? If not set, a new record is added.

**Flags**: IR

---
## Attr: GridEditRecordTask.criteria

### Description
Criteria (including AdvancedCriteria) used to locate the record to be edited. If criteria matches more than one record, the first record is edited.

Data values in this criteria prefixed with "$" will be treated as dynamic expressions which can access the inputs to this task as $input - see [TaskInputExpression](../reference_2.md#type-taskinputexpression). Specifically, this means that for simple criteria, any property value that is a String and is prefixed with "$" will be assumed to be an expression, and for AdvancedCriteria, the same treatment will be applied to [Criterion.value](Criterion.md#attr-criterionvalue).

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Process.ruleScope](Process.md#attr-processrulescope).

**Flags**: IR

---
