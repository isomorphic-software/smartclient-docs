# FilterBuilder Documentation

[← Back to API Index](../reference.md)

---

## Class: FilterBuilder

*Inherits from:* [Layout](Layout.md#class-layout)

### Description
A form that allows the user to input advanced search criteria, including operators on field values such as "less than", and sub-clauses using "AND" and "OR" operators.

A FilterBuilder produces an [AdvancedCriteria](../reference.md#object-advancedcriteria) object, which the [DataSource](DataSource.md#class-datasource) subsystem can use to filter datasets, including the ability to perform such filtering within the browser for datasets that are completely loaded.

The operators available for each field can be customized at the DataSource level via [DataSourceField.validOperators](DataSourceField.md#attr-datasourcefieldvalidoperators), [DataSource.setTypeOperators](DataSource.md#method-datasourcesettypeoperators) and related APIs.

---
## Attr: FilterBuilder.operatorPickerWidth

### Description
Width for the operator picker formItem displayed in clauses within this FilterBuilder.

**Flags**: IR

---
## Attr: FilterBuilder.operatorPickerProperties

### Description
Properties to combine with the [FilterBuilder.operatorPicker](#attr-filterbuilderoperatorpicker) autoChild FormItem.

**Flags**: IR

---
## Attr: FilterBuilder.fieldDataSource

### Description
If specified, the FilterBuilder will dynamically fetch DataSourceField definitions from this DataSource rather than using [FilterBuilder.dataSource](#attr-filterbuilderdatasource). The [FieldPicker](FieldPicker.md#class-fieldpicker) will default to being a [ComboBoxItem](ComboBoxItem.md#class-comboboxitem) rather than a [SelectItem](SelectItem.md#class-selectitem) so that the user will have type-ahead auto-completion.

The records returned from the `fieldDataSource` must have properties corresponding to a [DataSourceField](../reference_2.md#object-datasourcefield) definition, at a minimum, ["name"](DataSourceField.md#attr-datasourcefieldname) and ["type"](DataSourceField.md#attr-datasourcefieldtype). Any property legal on a DataSourceField is legal on the returned records, including [valueMap](DataSourceField.md#attr-datasourcefieldvaluemap).

Even when a `fieldDataSource` is specified, [FilterBuilder.dataSource](#attr-filterbuilderdatasource) may still be specified in order to control the list of [valid operators](DataSource.md#method-datasourcesettypeoperators) for each field.

**Flags**: IR

---
## Attr: FilterBuilder.showLastRemoveButton

### Description
If set to false and showing clause [remove buttons](#attr-filterbuildershowremovebutton) and [the last clause cannot be removed](#attr-filterbuilderallowempty) the remove clause button will be hidden.

**Flags**: IR

---
## Attr: FilterBuilder.inlineAndTitle

### Description
Title for the "And" operator (only applicable to the "inline" appearance)

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterBuilder.defaultSubClauseOperator

### Description
Default operator for subclauses added via the [FilterBuilder.subClauseButton](#attr-filterbuildersubclausebutton).

**Flags**: IR

---
## Attr: FilterBuilder.radioOptions

### Description
Logical operators to allow if we have a [TopOperatorAppearance](../reference.md#type-topoperatorappearance) of "radio".

**Deprecated**

**Flags**: IR

---
## Attr: FilterBuilder.radioOperatorTitle

### Description
The title for the Operator RadioGroupItem displayed in the [FilterBuilder.radioOperatorForm](#attr-filterbuilderradiooperatorform).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterBuilder.topOperatorAppearance

### Description
How to display and edit the [top-level operator](#attr-filterbuildertopoperator) for this FilterBuilder.

See [TopOperatorAppearance](../reference.md#type-topoperatorappearance) for a list of options.

**Flags**: IRW

---
## Attr: FilterBuilder.showHiddenFields

### Description
By default only non-hidden fields are shown for selection. To include hidden fields for selection set this property to `true`.

**Flags**: IR

---
## Attr: FilterBuilder.removeButton

### Description
The removal ImgButton that appears before each clause if [FilterBuilder.showRemoveButton](#attr-filterbuildershowremovebutton) is set.

**Flags**: IR

---
## Attr: FilterBuilder.allowedFields

### Description
List of explicit fields for user field selection. If not specified, the list of fields is derived from the [dataSource](#attr-filterbuilderdatasource).

Note: this property is not a security feature as it only controls the UI. To consistently limit searchability for certain fields use [canFilter](DataSourceField.md#attr-datasourcefieldcanfilter).

### See Also

- [FilterBuilder.showHiddenFields](#attr-filterbuildershowhiddenfields)

**Flags**: IR

---
## Attr: FilterBuilder.rangeSeparator

### Description
For operators that check that a value is within a range, text to show between the start and end input fields for specifying the limits of the range.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterBuilder.topOperator

### Description
Default logical operator for all top-level clauses in the FilterBuilder.

May be able to be changed by the user via the UI, according to [TopOperatorAppearance](../reference.md#type-topoperatorappearance).

**Flags**: IRW

---
## Attr: FilterBuilder.topOperatorOptions

### Description
Logical operators to allow for [TopOperatorAppearance](../reference.md#type-topoperatorappearance)s of "radio" and "bracket".

Note that this list may be further limited according to the [available operators](DataSource.md#method-datasourcegettypeoperatormap) returned by the [DataSource](DataSource.md#class-datasource).

**Flags**: IR

---
## Attr: FilterBuilder.operatorPickerTitle

### Description
The title for the operator-picker select-item.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterBuilder.showSubClauseButton

### Description
Whether to show a button that allows the user to add subclauses. Defaults to false if the [TopOperatorAppearance](../reference.md#type-topoperatorappearance) is "radio" or "inline", true in all other cases.

**Flags**: IR

---
## Attr: FilterBuilder.fieldPickerTitle

### Description
The title for the [field-picker](#attr-filterbuilderfieldpicker) select-item.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterBuilder.missingFieldPrompt

### Description
The message to display next to fieldNames that do not exist in the available dataSource.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterBuilder.modeSwitcherSimpleMessage

### Description
Title for the "Simple Mode.." mode switcher label (only applicable to the "bracket" appearance).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterBuilder.clauseStack

### Description
VStack of all clauses that are part of this FilterBuilder

**Flags**: IR

---
## Attr: FilterBuilder.showAddButton

### Description
If set, a button will be shown underneath all current clauses allowing a new clause to be added.

**Flags**: IR

---
## Attr: FilterBuilder.saveOnEnter

### Description
If true, when the user hits the Enter key while focused in a text-item in this FilterBuilder, we automatically invoke the user-supplied [FilterBuilder.search](#method-filterbuildersearch) method.

**Flags**: IR

---
## Attr: FilterBuilder.addButtonPrompt

### Description
The hover prompt text for the add button.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterBuilder.validateOnChange

### Description
If true (the default), validates each entered value when it changes, to make sure it is a a valid value of its type (valid string, number, and so on). No other validation is carried out. If you switch this property off, it is still possible to validate the `FilterBuilder` by calling [FilterBuilder.validate](#method-filterbuildervalidate) from your own code.

**Flags**: IR

---
## Attr: FilterBuilder.showSelectionCheckbox

### Description
If true, causes a CheckboxItem to appear to the left of each clause in "inline" [appearance](../reference.md#type-topoperatorappearance). This checkbox allows the user to select individual clauses so that, for example, clauses can be removed from the filterBuilder by application code. This property is ignored for appearances other than "inline".

**Flags**: IR

---
## Attr: FilterBuilder.lastClausePrompt

### Description
The hover prompt text for the remove button in the last remaining clause, when [allowEmpty](#attr-filterbuilderallowempty) is false.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: FilterBuilder.subClauseButtonTitle

### Description
The title of the subClauseButton

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterBuilder.allowEmpty

### Description
If set to false, the last clause cannot be removed.

**Flags**: IR

---
## Attr: FilterBuilder.modeSwitcher

### Description
Label to change between simple and advanced mode. When clicked the filter mode is switched to the other mode. This label is only shown if [showModeSwitcher](#attr-filterbuildershowmodeswitcher) is true.

Shows either [modeSwitcherSimpleMessage](#attr-filterbuildermodeswitchersimplemessage) or [modeSwitcherAdvancedMessage](#attr-filterbuildermodeswitcheradvancedmessage) depending on the current state of the filter.

**Flags**: IR

---
## Attr: FilterBuilder.dataSource

### Description
DataSource this filter should use for field definitions and available [Operator](../reference.md#object-operator)s.

**Flags**: IRW

---
## Attr: FilterBuilder.modeSwitcherAdvancedMessage

### Description
Title for the "Advanced.." mode switcher label (only applicable to the "radio" appearance).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterBuilder.modeSwitcherFlattenWarningMessage

### Description
Message displayed when switching to "radio" mode if the criteria will be logically changed.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterBuilder.matchNoneTitle

### Description
Title for the "Match None" (not) operator when using [topOperatorAppearance](../reference.md#type-topoperatorappearance):"radio".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterBuilder.bracket

### Description
Widget used as a "bracket" to hint to the user that a subclause groups several field-by-field filter criteria under one logical operator.

By default, a simple CSS-style Canvas with borders on three sides. A vertical StretchImg could provide a more elaborate appearance.

**Flags**: IR

---
## Attr: FilterBuilder.criteria

### Description
Initial criteria.

When initialized with criteria, appropriate clauses for editing the provided criteria will be automatically generated.

Note that empty or partial criteria are allowed, for example, criteria that specify [Criterion.fieldName](Criterion.md#attr-criterionfieldname) only will generate an expression with the operator not chosen yet, and a [Criterion](../reference_2.md#object-criterion) with a logical operator ("and" or "or") but not [subcriteria](Criterion.md#attr-criterioncriteria) defined will generate an empty subclause.

**Flags**: IRW

---
## Attr: FilterBuilder.topOperatorItemWidth

### Description
Width for the [FilterBuilder.topOperatorItem](#attr-filterbuildertopoperatoritem) autoChild.

**Flags**: IR

---
## Attr: FilterBuilder.subClauseButton

### Description
Button allowing the user to add subclauses grouped by a [LogicalOperator](../reference_2.md#type-logicaloperator).

**Flags**: IR

---
## Attr: FilterBuilder.addButton

### Description
An ImgButton that allows new clauses to be added if [FilterBuilder.showAddButton](#attr-filterbuildershowaddbutton) is set.

**Flags**: IR

---
## Attr: FilterBuilder.sortFields

### Description
Should the [FieldPicker](FieldPicker.md#class-fieldpicker) items be sorted alphabetically in the drop down list.

**Flags**: IR

---
## Attr: FilterBuilder.operatorPicker

### Description
AutoChild for the [FormItem](FormItem.md#class-formitem) that allows a user to select the operator when creating filter clauses. Each clause will create an operatorPicker automatically. To customize this item, use [FilterBuilder.operatorPickerProperties](#attr-filterbuilderoperatorpickerproperties)

**Flags**: IR

---
## Attr: FilterBuilder.radioOperatorForm

### Description
With [TopOperatorAppearance](../reference.md#type-topoperatorappearance):"radio", form that appears above the stack of clauses and allows picking the [LogicalOperator](../reference_2.md#type-logicaloperator) for the overall FilterBuilder.

By default, consists of a simple RadioGroupItem.

**Flags**: IR

---
## Attr: FilterBuilder.fieldPickerProperties

### Description
Properties to combine with the [FieldPicker](FieldPicker.md#class-fieldpicker) autoChild FormItem.

**Flags**: IR

---
## Attr: FilterBuilder.radioOperatorLayout

### Description
HLayout of radioOperationForm and optional modeSwitcher.

**Flags**: IR

---
## Attr: FilterBuilder.topOperatorTitle

### Description
The title for the left-aligned Operator selectItem in the [FilterBuilder.topOperatorForm](#attr-filterbuildertopoperatorform).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterBuilder.matchAllTitle

### Description
Title for the "Match All" (and) operator when using [topOperatorAppearance](../reference.md#type-topoperatorappearance):"radio".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterBuilder.showModeSwitcher

### Description
When enabled allows FilterBuilder in `topOperatorAppearance:"radio"` or `topOperatorAppearance:"bracket"` mode to be switch to the other view by the user. "radio" mode is considered simple where "bracket" mode is advanced mode.

Note that when switching from "bracket" to "radio" mode any entered criteria will be flattened by calling [DataSource.flattenCriteria](DataSource.md#classmethod-datasourceflattencriteria). If the criteria cannot be flattened without losing symantics (see [DataSource.canFlattenCriteria](DataSource.md#classmethod-datasourcecanflattencriteria)) the user is prompted to confirm.

If showModeSwitcher is set and topOperatorAppearance is unset:

*   when first drawn, the filterBuilder will choose which mode to use based on the provided [FilterBuilder.criteria](#attr-filterbuildercriteria) if any: advanced mode ("bracket") will be used if AdvancedCriteria are provided which cannot be flattened without loss of data (see [DataSource.canFlattenCriteria](DataSource.md#classmethod-datasourcecanflattencriteria)), otherwise simple mode ("radio") will be used.
*   for any calls to [FilterBuilder.setCriteria](#method-filterbuildersetcriteria) after draw, the FilterBuilder will switch to advanced mode if the criteria cannot be shown in simple mode without losing information, but will never automatically switch to simple mode, but an explicit call [setTopOperatorAppearance("radio")](#method-filterbuildersettopoperatorappearance) can be used to do so.

### See Also

- [FilterBuilder.modeSwitcherSimpleMessage](#attr-filterbuildermodeswitchersimplemessage)
- [FilterBuilder.modeSwitcherAdvancedMessage](#attr-filterbuildermodeswitcheradvancedmessage)
- [FilterBuilder.modeSwitcherFlattenWarningMessage](#attr-filterbuildermodeswitcherflattenwarningmessage)

**Flags**: IR

---
## Attr: FilterBuilder.inlineOrTitle

### Description
Title for the "Or" operator (only applicable to the "inline" appearance)

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterBuilder.showRemoveButton

### Description
If set, a button will be shown for each clause allowing it to be removed.

**Flags**: IR

---
## Attr: FilterBuilder.retainValuesAcrossFields

### Description
Dictates whether values entered by a user should be retained in the value fields when a different field is selected. Default value is true.

Note that, when switching between fields that have an optionDataSource or valueMap, this property is ignored and the values are never retained.

**Flags**: IRW

---
## Attr: FilterBuilder.matchAnyTitle

### Description
Title for the "Match Any" (or) operator when using [topOperatorAppearance](../reference.md#type-topoperatorappearance):"radio".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterBuilder.topOperatorForm

### Description
With [TopOperatorAppearance](../reference.md#type-topoperatorappearance) "bracket" and "inline", a form that appears to the left of the stack of clauses and allows picking the [LogicalOperator](../reference_2.md#type-logicaloperator) for the overall FilterBuilder (or for that specific FilterClause, in the case of "inline")

By default, consists of a CheckboxItem if [FilterBuilder.showSelectionCheckbox](#attr-filterbuildershowselectioncheckbox) is true, and a simple SelectItem containing the available logical operators.

If this FilterBuilder shows nested sub-clauses, the same defaults will be applied to the top-operator item for each sub-clause.

**Flags**: IR

---
## Attr: FilterBuilder.showFieldTitles

### Description
If true (the default), show field titles in the drop-down box used to select a field for querying. If false, show actual field names instead.

**Flags**: IR

---
## Attr: FilterBuilder.fieldPickerWidth

### Description
Width for the field picker formItem displayed in clauses within this FilterBuilder.

**Flags**: IR

---
## Attr: FilterBuilder.topOperatorItem

### Description
Automatically generated SelectItem autoChild shown in the [FilterBuilder.topOperatorForm](#attr-filterbuildertopoperatorform). Developers may customize this item using the standard autoChild pattern (by modifying `topOperatorItemDefaults` and `topOperatorItemProperties`).

If this FilterBuilder shows nested sub-clauses, the same defaults will be applied to the top-operator item for each sub-clause.

**Flags**: IR

---
## Attr: FilterBuilder.fieldPicker

### Description
AutoChild for the [FormItem](FormItem.md#class-formitem) that allows a user to pick a DataSource field when creating filter clauses.

This will be a [SelectItem](SelectItem.md#class-selectitem) by default, or a [ComboBoxItem](ComboBoxItem.md#class-comboboxitem) if [FilterBuilder.fieldDataSource](#attr-filterbuilderfielddatasource) has been specified.

**Flags**: IR

---
## Attr: FilterBuilder.inlineAndNotTitle

### Description
Title for the "And Not" operator (only applicable to the "inline" appearance)

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterBuilder.removeButtonPrompt

### Description
The hover prompt text for the remove button.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterBuilder.subClauseButtonPrompt

### Description
The hover prompt text for the subClauseButton.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FilterBuilder.valueItemWidth

### Description
Width for the value-chooser formItem displayed in clauses within this FilterBuilder. Note that depending on the selected operator type, this item may not be displayed, or may have different characteristics. See [FilterBuilder.getValueFieldProperties](#method-filterbuildergetvaluefieldproperties) for information on customizing the value item.

**Flags**: IR

---
## ClassMethod: FilterBuilder.getFilterDescription

### Description
Returns a human-readable string describing the clauses in this advanced criteria or criterion.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [AdvancedCriteria](#type-advancedcriteria)|[Criterion](#type-criterion) | false | — | Criteria to convert to a readable string |
| dataSource | [DataSource](#type-datasource) | false | — | DataSource to provide definitions of operators |

### Returns

`[String](#type-string)` — Human-readable string describing the clauses in the passed criteria

---
## Method: FilterBuilder.clearCriteria

### Description
Clear all current criteria.

---
## Method: FilterBuilder.filterChanged

### Description
Handler fired when there is a change() event fired on any FormItem within the filterBuilder.

---
## Method: FilterBuilder.addCriterion

### Description
Add a new criterion, including recursively adding sub-criteria for a criterion that contains other criteria.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criterion | [Criterion](#type-criterion) | false | — | new criterion to be added |

---
## Method: FilterBuilder.search

### Description
A StringMethod that is automatically invoked if [FilterBuilder.saveOnEnter](#attr-filterbuildersaveonenter) is set and the user presses Enter whilst in a text-item in any clause or subclause.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [AdvancedCriteria](#type-advancedcriteria) | false | — | The criteria represented by the filterBuilder |

---
## Method: FilterBuilder.getFieldOperators

### Description
Get the list of [operatorIds](../reference.md#type-operatorid) that are valid for the passed field. By default, all operators returned by [DataSource.getFieldOperators](DataSource.md#method-datasourcegetfieldoperators) are used.

Called automatically by the default implementation of the same method on each [clause](FilterClause.md#method-filterclausegetfieldoperators), whenever its fieldName is changed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | the name of the field for which to return the set of available operators |

### Returns

`[Array of OperatorId](#type-array-of-operatorid)` — valid operators for this field

---
## Method: FilterBuilder.getCriteria

### Description
Get the criteria entered by the user.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| includeEmptyValues | [boolean](../reference.md#type-boolean) | true | — | By default if a user has selected a field and operator type, but has failed to enter a value for the field it will be skipped. This optional parameter allows you to retrieve all criteria, including those with an empty `value` attribute. |

### Returns

`[AdvancedCriteria](#type-advancedcriteria)` — —

---
## Method: FilterBuilder.getEditorType

### Description
Returns the type of editor to use for the field.

Default behavior is to use the [Operator.editorType](Operator.md#attr-operatoreditortype) for a custom operator, otherwise, use [RelativeDateItem](RelativeDateItem.md#class-relativedateitem) for before/after/between operators on date fields, otherwise, use the same editor as would be chosen by a [SearchForm](SearchForm.md#class-searchform).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [DataSourceField](#type-datasourcefield) | false | — | DataSourceField definition |
| operatorId | [OperatorId](../reference.md#type-operatorid) | false | — | [OperatorId](../reference.md#type-operatorid) for the chosen operator |

### Returns

`[SCClassName](../reference.md#type-scclassname)` — SmartClient class to use (must be subclass of FormItem)

---
## Method: FilterBuilder.setTopOperator

### Description
Programmatically change the [FilterBuilder.topOperator](#attr-filterbuildertopoperator) for this FilterBuilder.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| operator | [LogicalOperator](../reference_2.md#type-logicaloperator) | false | — | new top-level operator |

---
## Method: FilterBuilder.addClause

### Description
Add a new [FilterClause](FilterClause.md#class-filterclause) to this FilterBuilder.

This API is intended for the rare use case of adding a highly customized FilterClause component that does not include the standard field/operator/value picking interface, instead providing a custom interface and returning a criterion via [FilterClause.getCriterion](FilterClause.md#method-filterclausegetcriterion).

If you just want to programmatically add a new FilterClause showing a specific Criterion use [FilterBuilder.addCriterion](#method-filterbuilderaddcriterion).

If you want to use the standard field/operator/value interface but provide a custom control for editing the value, see [DataSource.addSearchOperator](DataSource.md#method-datasourceaddsearchoperator) and [Operator.editorType](Operator.md#attr-operatoreditortype).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| filterClause | [FilterClause](#type-filterclause) | false | — | A [FilterClause](FilterClause.md#class-filterclause) instance |

---
## Method: FilterBuilder.getFilterDescription

### Description
Returns a human-readable string describing the clauses in this filterBuilder.

### Returns

`[String](#type-string)` — Human-readable string describing the clauses in the passed criteria

---
## Method: FilterBuilder.setCriteria

### Description
Set new criteria for editing.

An interface for editing the provided criteria will be generated identically to what happens when initialized with [Criteria](../reference_2.md#type-criteria).

Any existing criteria entered by the user will be discarded.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [AdvancedCriteria](#type-advancedcriteria) | false | — | new criteria. Pass null or {} to effectively reset the filterBuilder to it's initial state when no criteria are specified |

---
## Method: FilterBuilder.setTopOperatorAppearance

### Description
Modify [TopOperatorAppearance](../reference.md#type-topoperatorappearance) at runtime.

Note that when changing from "bracket" to "radio" mode the criteria will be flattened by calling [DataSource.flattenCriteria](DataSource.md#classmethod-datasourceflattencriteria) which could result in a logical change to the criteria.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| appearance | [TopOperatorAppearance](../reference.md#type-topoperatorappearance) | false | — | new topOperatorAppearance |

### Groups

- formTitles

---
## Method: FilterBuilder.validate

### Description
Validate the clauses of this FilterBuilder.

### Returns

`[Boolean](#type-boolean)` — true if all clauses are valid, false otherwise

---
## Method: FilterBuilder.removeClause

### Description
Remove a clause this FilterBuilder is currently showing.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| clause | [FilterClause](#type-filterclause) | false | — | clause as retrieved from filterBuilder.clauses |

---
## Method: FilterBuilder.getSelectedClauses

### Description
Returns the list of this FilterBuilder's FilterClauses that are currently selected. A clause is "selected" if the user has checked the checkbox next to it; therefore, this method always returns an empty list unless the [showSelectionCheckbox](#attr-filterbuildershowselectioncheckbox) property is set. This method is only applicable where [TopOperatorAppearance](../reference.md#type-topoperatorappearance) is "inline" (because that is the only appearance that supports `showSelectionCheckbox`)

### Returns

`[Array of FilterClause](#type-array-of-filterclause)` — The list of selected clauses

---
## Method: FilterBuilder.getChildFilters

### Description
Returns an array of child [FilterBuilder](#class-filterbuilder)s, representing the list of complex clauses, or an empty array if there aren't any.

### Returns

`[Array of FilterBuilder](#type-array-of-filterbuilder)` — The list of complex clauses for this filterBuilder

---
## Method: FilterBuilder.getValueFieldProperties

### Description
Override to return properties for the FormItem(s) used for the "value" field displayed within clauses within this filterBuilder.

Note that the [Operator.valueType](Operator.md#attr-operatorvaluetype) impacts when this method is called. For operators with valueType `"fieldType"` or `"custom"`, a single value field is displayed. For operators with valueType `"valueRange"` two value-field items are displayed (one for the start and one for the end position). The `valueItemType` parameter may be used to determine which form item is being generated.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| type | [FieldType](../reference_2.md#type-fieldtype) | false | — | type of the DataSource field for this filter row |
| fieldName | [String](#type-string) | false | — | name of the DataSource field for this filter row |
| operatorId | [OperatorId](../reference.md#type-operatorid) | false | — | [OperatorId](../reference.md#type-operatorid) for the chosen operator |
| itemType | [ValueItemType](../reference.md#type-valueitemtype) | false | — | What valueItem is being generated. |

### Returns

`[FormItem Properties](#type-formitem-properties)` — properties for the value field

---
