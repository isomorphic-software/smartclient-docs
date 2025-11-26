# ComboBoxItem criteria

[← Back to API Index](../reference.md)

---

## KB Topic: ComboBoxItem criteria

### Description
A ComboBoxItem generates two different types of criteria in different circumstances:

1.  The criteria used against the [optionDataSource](../classes/ComboBoxItem.md#attr-comboboxitemoptiondatasource) to retrieve what is shown in the drop-down [pickList](../classes/ComboBoxItem.md#attr-comboboxitempicklist), and also to retrieve individual display values via the [fetchMissingValues](../classes/TextItem.md#attr-textitemfetchmissingvalues) behavior
2.  The criteria that are generated for searching in some other component when the ComboBoxItem is used as part of a [SearchForm](../classes/SearchForm.md#class-searchform), such as in the [FilterEditor of a ListGrid](../classes/ListGrid_1.md#attr-listgridshowfiltereditor), or in a separate SearchForm (perhaps configured via [ListGrid.searchForm](../classes/ListGrid_1.md#attr-listgridsearchform))

This overview covers the latter case: how a ComboBoxItem creates criteria for searching some in some other component.

**Explicitly selected option:**  
If a user explicitly selects an option from the ComboBox drop down pickList, default behavior is to generate an [advanced criterion](../classes/ComboBoxItem.md#method-comboboxitemhasadvancedcriteria) with [operator:"equals"](../reference.md#type-operatorid) to exactly match the selected option.

This reflects user expectation. If you are, for example, filtering a grid of Orders, and you have a ComboBoxItem as part of a search interface that allows you to pick a specific salesRep, then you expect to see only orders handled by that salesRep.

Exceptions: If the target DataSource does not [support advanced criteria](../classes/DataSource.md#method-datasourcesupportsadvancedcriteria), or [ComboBoxItem.generateExactMatchCriteria](../classes/ComboBoxItem.md#attr-comboboxitemgenerateexactmatchcriteria) has been explicitly set to false, simple criteria will be generated. Also note that if a [ComboBoxItem.operator](../classes/FormItem.md#attr-formitemoperator) has been specified, it will be used instead of setting the operator to `"equals"`.

**Unrecognized value:**  
If, instead of picking an option, a user enters some text into the ComboBoxItem's textbox that does not exactly match one of the available options, the generated filter criterion will not be an advanced criterion by default. Instead it will behave like a normal [TextItem](../classes/TextItem.md#class-textitem), generating a simple criterion value unless advanced criteria were [explicitly requested](../classes/DynamicForm.md#method-dynamicformgetvaluesasadvancedcriteria), or the item also has a specified [ComboBoxItem.operator](../classes/FormItem.md#attr-formitemoperator).

This again reflects user expectation. If you are, for example, filtering a grid of Orders, and you have a ComboBoxItem as part of a search interface that allows you to pick Sales Reps, then if you enter just "John", you would expect to see all orders that were handled by anyone named "John".

**Criterion field**:  
By default, if a specific value has been chosen, the generated Criterion targets the valueField with an exact match (with exceptions explained above).

However, if a search value has been entered without picking a specific record, the generated Criterion targets the displayField if it differs from the valueField. This is correct behavior - if we consider the example of showing all Orders entered by any Sales Rep called "John", we'd need to apply criteria to the display field (containing the Sales Reps' names) rather than the valueField (likely to be an ID or similar).

Developers may override this behavior by specifying an explicit [ComboBoxItem.criteriaField](../classes/FormItem.md#attr-formitemcriteriafield). If specified this will be used in the generated criteria whether the user selected an option from the pickList or entered a new value into the text box.

---
