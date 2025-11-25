# MiniDateRangeItem Documentation

[← Back to API Index](../main.md)

---

## Class: MiniDateRangeItem

*Inherits from:* [StaticTextItem](StaticTextItem.md#class-statictextitem)

### Description
Provides a compact interface for editing a date range, by providing a formatted, read-only display of the current selected date range with an icon to launch a [DateRangeDialog](DateRangeDialog.md#class-daterangedialog) to edit the range.

---
## Attr: MiniDateRangeItem.textBoxStyle

### Description
Base CSS class name for a form item's text box element.

See [formItemStyling](../kb_topics/formItemStyling.md#kb-topic-formitem-styling) for an overview of formItem styling, and the [CompoundFormItem_skinning](../main.md#kb-topic-compoundformitem_skinning) discussion for special skinning considerations.

If the `textBoxStyle` is changed at runtime, [updateState()](FormItem.md#method-formitemupdatestate) must be called to update the visual state of this item.

### Groups

- formItemStyling

### See Also

- [FormItem.cellStyle](FormItem.md#attr-formitemcellstyle)

**Flags**: IRW

---
## Attr: MiniDateRangeItem.pickerIconPrompt

### Description
The prompt to show when the mouse is hovered over the [MiniDateRangeItem.pickerIcon](#attr-minidaterangeitempickericon).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MiniDateRangeItem.dateDisplayFormat

### Description
Format for displaying dates to the user.

If this attribute is unset, the display value is formatted intelligently according to the dates involved. For example, if both dates appear in the same month, the value will be formatted as

`Month date1 - date2, Year`

and, if in different months of the same year,

`Month1 date1 - Month2 date2, Year`.

If either date-value is unset, the display-value is formatted according to [fromDateOnlyPrefix](#attr-minidaterangeitemfromdateonlyprefix) and [toDateOnlyPrefix](#attr-minidaterangeitemtodateonlyprefix).

**Flags**: IR

---
## Attr: MiniDateRangeItem.canTabToIcons

### Description
MiniDateRangeItems rely on their icon being able to receive focus for normal user interaction as they have no other focusable element. `canTabToIcons` is overridden to achieve this even if the property has been set to `false` at the [form level](DynamicForm.md#attr-dynamicformcantabtoicons).

**Flags**: IRWA

---
## Attr: MiniDateRangeItem.allowRelativeDates

### Description
Whether the [DateRangeDialog](DateRangeDialog.md#class-daterangedialog) opened when the [pickerIcon](#attr-minidaterangeitempickericon) is clicked should display [RelativeDateItem](RelativeDateItem.md#class-relativedateitem)s or [DateItem](DateItem.md#class-dateitem)s.

**Flags**: IR

---
## Attr: MiniDateRangeItem.fromDate

### Description
Initial value for the "from" date.

**Flags**: IRW

---
## Attr: MiniDateRangeItem.shouldSaveValue

### Description
Allow miniDateRangeItems' values to show up in the form's values array, or if [DynamicForm.getValuesAsCriteria](DynamicForm.md#method-dynamicformgetvaluesascriteria) is called, for the criterion to be included in the returned AdvancedCriteria object

**Flags**: IR

---
## Attr: MiniDateRangeItem.rangeDialog

### Description
Pop-up [DateRangeDialog](DateRangeDialog.md#class-daterangedialog) for entering a date range.

**Flags**: IR

---
## Attr: MiniDateRangeItem.fromDateOnlyPrefix

### Description
The text to prepend to the formatted date when only a [fromDate](#attr-minidaterangeitemfromdate) is supplied.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MiniDateRangeItem.autoValidate

### Description
If this attribute is set to true, the pop up date range dialog will automatically validate the user-entered _"to"_ and _"from"_ values on `"OK"`\-click, and refuse to dismiss if these items contain invalid values.

**Flags**: IRW

---
## Attr: MiniDateRangeItem.toDateOnlyPrefix

### Description
The text to prepend to the formatted date when only a [toDate](#attr-minidaterangeitemtodate) is supplied.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MiniDateRangeItem.canFocus

### Description
MiniDateRangeItems are marked as canFocus:true, and set up with properties such that focus will always go to the icon to launch the dateRange dialog. Set canFocus to false to suppress this behavior.

**Flags**: IR

---
## Attr: MiniDateRangeItem.pickerIcon

### Description
Icon that launches a [DateChooser](DateChooser.md#class-datechooser) for choosing an absolute date.

**Flags**: IR

---
## Attr: MiniDateRangeItem.toDate

### Description
Initial value for the "to" date.

**Flags**: IRW

---
## Method: MiniDateRangeItem.setCriterion

### Description
Applies the specified criterion to this item for editing. Applies any specified "greaterOrEqual" operator criterion or sub-criterion to our [fromField](DateRangeItem.md#attr-daterangeitemfromfield) and any specified "lessOrEqual" operator criterion or sub-criterion to our [toField](DateRangeItem.md#attr-daterangeitemtofield).

Note that a single "equals" criterion can also be passed. See [canEditCriterion()](DateRangeItem.md#method-daterangeitemcaneditcriterion) for more detail.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criterion | [Criterion](#type-criterion) | false | — | criterion to edit |

### Groups

- criteriaEditing

---
## Method: MiniDateRangeItem.getCriterion

### Description
Returns the Criterion entered in the fields shown in the [MiniDateRangeItem.rangeDialog](#attr-minidaterangeitemrangedialog).

If both dates are entered, a Criterion with an "and" [operator](../main.md#type-operatorid) and both "greaterOrEqual" and "lessOrEqual" sub-criteria will be returned. If either date is omitted, only the "greaterOrEqual" (from date) or "lessOrEqual" (to date) Criterion is returned.

### Returns

`[Criterion](#type-criterion)` — —

### Groups

- criteriaEditing

---
## Method: MiniDateRangeItem.hasAdvancedCriteria

### Description
Overridden to return true: dateRangeItems always generate AdvancedCriteria.

### Returns

`[Boolean](#type-boolean)` — true

### Groups

- criteriaEditing

---
## Method: MiniDateRangeItem.setAutoValidate

### Description
Setter for [MiniDateRangeItem.autoValidate](#attr-minidaterangeitemautovalidate)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| autoValidate | [boolean](../main.md#type-boolean) | false | — | New auto-validate setting. |

---
## Method: MiniDateRangeItem.getValue

### Description
Retrieves the current value of this dateRangeItem. The return value is a [DateRange](../main_2.md#object-daterange) object that excludes start and end values if they aren't set.

### Returns

`[DateRange](#type-daterange)` — the current value of this item

---
## Method: MiniDateRangeItem.canEditCriterion

### Description
Returns true if the specified criterion contains:

*   A single "lessOrEqual" or "greaterOrEqual" criterion on this field
*   An "and" type criterion containing a "lessOrEqual" and a "greaterOrEqual" criterion on this field
*   A single "equals" criterion. Internally, this will be converted into a range by constructing an "and" type criterion containing both a "lessOrEqual" and a "greaterOrEqual" criterion on this field. Note that subsequent calls to [getCriterion()](DateRangeItem.md#method-daterangeitemgetcriterion) will return this more complex criterion.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criterion | [Criterion](#type-criterion) | false | — | criterion to test |

### Returns

`[boolean](../main.md#type-boolean)` — returns true if this criterion can be edited by this item

### Groups

- criteriaEditing

---
## Method: MiniDateRangeItem.setValue

### Description
Sets the value for this miniDateRangeItem. The value parameter is a [DateRange](../main_2.md#object-daterange) object that optionally includes both start and end values.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [DateRange](#type-daterange) | false | — | the new value for this item |

---
