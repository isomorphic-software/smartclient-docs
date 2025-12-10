# Criteria Editing

[← Back to API Index](../reference.md)

---

## KB Topic: Criteria Editing

### Description
DynamicForms may be used to edit [Criteria](../reference_2.md#type-criteria) or [AdvancedCriteria](../reference.md#object-advancedcriteria) for filtering data from a DataSource.

The main APIs for this are [DynamicForm.getValuesAsCriteria](../classes/DynamicForm.md#method-dynamicformgetvaluesascriteria) and [DynamicForm.setValuesAsCriteria](../classes/DynamicForm.md#method-dynamicformsetvaluesascriteria).

`getValuesAsCriteria()` will return an AdvancedCriteria object in the following cases:

*   The form was previously passed AdvancedCriteria via `setValuesAsCriteria()`
*   The form has a specified [DynamicForm.operator](../classes/DynamicForm.md#attr-dynamicformoperator) of `"or"`
*   [FormItem.hasAdvancedCriteria](../classes/FormItem.md#method-formitemhasadvancedcriteria) returns true for some item(s) within the form

Note that at the form item level, individual items can support editing of advanced criteria via overrides to the [FormItem.hasAdvancedCriteria](../classes/FormItem.md#method-formitemhasadvancedcriteria), [FormItem.canEditCriterion](../classes/FormItem.md#method-formitemcaneditcriterion), [FormItem.setCriterion](../classes/FormItem.md#method-formitemsetcriterion) and [FormItem.getCriterion](../classes/FormItem.md#method-formitemgetcriterion) methods.

There is also built-in support for [expression-parsing](../classes/DynamicForm.md#attr-dynamicformallowexpressions) in DynamicForms. This allows expressions, like '>5' (greater than 5) or 'a...c' (between a and c) to be edited and generated automatically by appropriate formItems.

Some FormItems have special behavior - for instance, a [SelectItem](../classes/SelectItem.md#class-selectitem) with [multiple:true](../classes/SelectItem.md#attr-selectitemmultiple) will successfully edit and return criteria with an `inSet` operator.

The common pattern of using nested dynamicForms to edit arbitrary advanced criteria has been implemented via overrides to these methods in the [CanvasItem](../classes/CanvasItem.md#class-canvasitem) class. See [CanvasItem.getCriterion](../classes/CanvasItem.md#method-canvasitemgetcriterion) for details.

For completely user-driven advanced criteria editing see also the [FilterBuilder](../classes/FilterBuilder.md#class-filterbuilder) class.

### Related

- [DynamicForm.getValuesAsCriteria](../classes/DynamicForm.md#method-dynamicformgetvaluesascriteria)
- [DynamicForm.setValuesAsCriteria](../classes/DynamicForm.md#method-dynamicformsetvaluesascriteria)
- [DynamicForm.getValuesAsAdvancedCriteria](../classes/DynamicForm.md#method-dynamicformgetvaluesasadvancedcriteria)
- [FormItem.hasAdvancedCriteria](../classes/FormItem.md#method-formitemhasadvancedcriteria)
- [FormItem.canEditCriterion](../classes/FormItem.md#method-formitemcaneditcriterion)
- [FormItem.getCriterion](../classes/FormItem.md#method-formitemgetcriterion)
- [FormItem.setCriterion](../classes/FormItem.md#method-formitemsetcriterion)
- [CanvasItem.hasAdvancedCriteria](../classes/CanvasItem.md#method-canvasitemhasadvancedcriteria)
- [CanvasItem.canEditCriterion](../classes/CanvasItem.md#method-canvasitemcaneditcriterion)
- [CanvasItem.getCriterion](../classes/CanvasItem.md#method-canvasitemgetcriterion)
- [CanvasItem.setCriterion](../classes/CanvasItem.md#method-canvasitemsetcriterion)
- [ComboBoxItem.hasAdvancedCriteria](../classes/ComboBoxItem.md#method-comboboxitemhasadvancedcriteria)
- [ComboBoxItem.getCriterion](../classes/ComboBoxItem.md#method-comboboxitemgetcriterion)
- [ComboBoxItem.canEditCriterion](../classes/ComboBoxItem.md#method-comboboxitemcaneditcriterion)
- [ComboBoxItem.setCriterion](../classes/ComboBoxItem.md#method-comboboxitemsetcriterion)
- [ValuesManager.getValuesAsCriteria](../classes/ValuesManager.md#method-valuesmanagergetvaluesascriteria)
- [ValuesManager.getValuesAsAdvancedCriteria](../classes/ValuesManager.md#method-valuesmanagergetvaluesasadvancedcriteria)
- [DateRangeItem.hasAdvancedCriteria](../classes/DateRangeItem.md#method-daterangeitemhasadvancedcriteria)
- [DateRangeItem.getCriterion](../classes/DateRangeItem.md#method-daterangeitemgetcriterion)
- [DateRangeItem.canEditCriterion](../classes/DateRangeItem.md#method-daterangeitemcaneditcriterion)
- [DateRangeItem.setCriterion](../classes/DateRangeItem.md#method-daterangeitemsetcriterion)
- [MiniDateRangeItem.hasAdvancedCriteria](../classes/MiniDateRangeItem.md#method-minidaterangeitemhasadvancedcriteria)
- [MiniDateRangeItem.getCriterion](../classes/MiniDateRangeItem.md#method-minidaterangeitemgetcriterion)
- [MiniDateRangeItem.setCriterion](../classes/MiniDateRangeItem.md#method-minidaterangeitemsetcriterion)
- [MiniDateRangeItem.canEditCriterion](../classes/MiniDateRangeItem.md#method-minidaterangeitemcaneditcriterion)
- [FormItem.operator](../classes/FormItem.md#attr-formitemoperator)
- [FormItem.useAdvancedCriteria](../classes/FormItem.md#attr-formitemuseadvancedcriteria)
- [ListGrid.useAdvancedCriteria](../classes/ListGrid_1.md#attr-listgriduseadvancedcriteria)

---
