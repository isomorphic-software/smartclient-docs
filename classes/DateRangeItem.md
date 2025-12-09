# DateRangeItem Documentation

[← Back to API Index](../reference.md)

---

## Class: DateRangeItem

*Inherits from:* [CanvasItem](CanvasItem.md#class-canvasitem)

### Description
Allows a user to select an absolute or relative range of dates via two [RelativeDateItem](RelativeDateItem.md#class-relativedateitem)s (if [DateRangeItem.allowRelativeDates](#attr-daterangeitemallowrelativedates) is true) or two [DateItems](DateItem.md#class-dateitem).

The item's [data type](FormItem.md#attr-formitemtype) is expected to be one of "date" or "datetime" and dictates whether the dates in the range include a time portion. If unset and the item's form is databound, the data type is detected from the associated [dataSource field](../reference_2.md#object-datasourcefield). If there is no such field, or the form is not databound, the default data type value is "date".

DateRangeItem is just a convenience relative to using two [RelativeDateItem](RelativeDateItem.md#class-relativedateitem) or [DateItem](DateItem.md#class-dateitem) controls in a form, then using [FormItem.operator](FormItem.md#attr-formitemoperator) and [FormItem.criteriaField](FormItem.md#attr-formitemcriteriafield) to cause them to produce a date range. If you need more control over layout, validation, event handling or any other aspect of appearance or behavior, stop using DateRangeItem and use two DateItem/RelativeDateItem controls directly instead.

---
## Attr: DateRangeItem.fromTitle

### Description
The title for the [from](#attr-daterangeitemfromfield) part of the range.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: DateRangeItem.toDate

### Description
Initial value for the "to" date.

**Flags**: IRW

---
## Attr: DateRangeItem.fromField

### Description
The field for the "from" date - a [RelativeDateItem](RelativeDateItem.md#class-relativedateitem) or [DateItem](DateItem.md#class-dateitem) according to [DateRangeItem.allowRelativeDates](#attr-daterangeitemallowrelativedates).

**Flags**: IR

---
## Attr: DateRangeItem.relativeItemConstructor

### Description
The [FormItem](FormItem.md#class-formitem) class to create when [DateRangeItem.allowRelativeDates](#attr-daterangeitemallowrelativedates) is true.

**Flags**: R

---
## Attr: DateRangeItem.absoluteDateTimeItemConstructor

### Description
The [FormItem](FormItem.md#class-formitem) class to create when [DateRangeItem.allowRelativeDates](#attr-daterangeitemallowrelativedates) is false, and the [DateRangeItem](#class-daterangeitem)'s type is "datetime".

### See Also

- [FieldType](../reference_2.md#type-fieldtype)

**Flags**: R

---
## Attr: DateRangeItem.allowRelativeDates

### Description
Whether to allow the user to specify relative dates (via [RelativeDateItem](RelativeDateItem.md#class-relativedateitem)s) or whether dates are absolute (via [DateItem](DateItem.md#class-dateitem)s).

**Flags**: IR

---
## Attr: DateRangeItem.toTitle

### Description
The title for the [to](#attr-daterangeitemtofield) part of the range.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: DateRangeItem.fieldLayout

### Description
Controls the placement of the [DateRangeItem.toField](#attr-daterangeitemtofield) and [DateRangeItem.fromField](#attr-daterangeitemfromfield) in the [DateRangeItem.dateRangeForm](#attr-daterangeitemdaterangeform).

Note that we don't recommend "horizontal" placement for mobile, and we also don't recommend it for [DateRangeItem.allowRelativeDates](#attr-daterangeitemallowrelativedates) mode, since [RelativeDateItem](RelativeDateItem.md#class-relativedateitem) changes width drastically during editing, which causes a lot of unpleasant side-to-side shifting of controls.

**Flags**: IR

---
## Attr: DateRangeItem.absoluteItemConstructor

### Description
The [FormItem](FormItem.md#class-formitem) class to create when [DateRangeItem.allowRelativeDates](#attr-daterangeitemallowrelativedates) is false, but the [DateRangeItem](#class-daterangeitem) does not have type "datetime".

### See Also

- [FieldType](../reference_2.md#type-fieldtype)

**Flags**: R

---
## Attr: DateRangeItem.fromDate

### Description
Initial value for the "from" date.

**Flags**: IRW

---
## Attr: DateRangeItem.validateCriteria

### Description
If this attribute is set to `true` when [getCriterion()](FormItem.md#method-formitemgetcriterion) is called, the item will validate the _"to"_ and _"from"_ fields and return null if either field fails validation. See [DateRangeItem.validateRange](#method-daterangeitemvalidaterange)

**Flags**: IRW

---
## Attr: DateRangeItem.textFormula

### Description
Not applicable to a DateRangeItem.

**Flags**: IR

---
## Attr: DateRangeItem.shouldSaveValue

### Description
Allow dateRangeItems' values to show up in the form's values array, or if [DynamicForm.getValuesAsCriteria](DynamicForm.md#method-dynamicformgetvaluesascriteria) is called, for the criterion to be included in the returned AdvancedCriteria object

**Flags**: IR

---
## Attr: DateRangeItem.inputFormat

### Description
For fields of type `"date"`, if this is an editable field such as a [TextItem](TextItem.md#class-textitem), this property allows you to specify the [inputFormat](DateItem.md#attr-dateiteminputformat) applied to the item.

### See Also

- [FormItem.dateFormatter](FormItem.md#attr-formitemdateformatter)

**Flags**: IR

---
## Attr: DateRangeItem.toField

### Description
The field for the "to" date - a [RelativeDateItem](RelativeDateItem.md#class-relativedateitem) or [DateItem](DateItem.md#class-dateitem) according to [DateRangeItem.allowRelativeDates](#attr-daterangeitemallowrelativedates).

**Flags**: IR

---
## Attr: DateRangeItem.invalidRangeErrorMessage

### Description
Error message to display if the user enters a date range where the "To" field value is earlier than the "From" field value.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: DateRangeItem.formula

### Description
Not applicable to a DateRangeItem.

**Flags**: IR

---
## Attr: DateRangeItem.dateRangeForm

### Description
[DynamicForm](DynamicForm.md#class-dynamicform) [AutoChild](../reference.md#type-autochild) automatically created by the dateRangeItem and applied to the item as [this.canvas](CanvasItem.md#attr-canvasitemcanvas).

This DynamicForm contains the "from" and "to" fields the user will interact with to actually select a date-range. Note that as a standard autoChild, developers may customize this form by modifying `dateRangeProperties`.

**Flags**: R

---
## Attr: DateRangeItem.innerTitleOrientation

### Description
The title orientation for the to / from sub-items. If unset this will be derived from [this.titleOrientation](FormItem.md#attr-formitemtitleorientation) or [this.form.titleOrientation](DynamicForm.md#attr-dynamicformtitleorientation).

**Flags**: IR

---
## Method: DateRangeItem.canEditCriterion

### Description
Returns true if the specified criterion contains:

*   A single "lessOrEqual" or "greaterOrEqual" criterion on this field
*   An "and" type criterion containing a "lessOrEqual" and a "greaterOrEqual" criterion on this field
*   A single "equals" criterion. Internally, this will be converted into a range by constructing an "and" type criterion containing both a "lessOrEqual" and a "greaterOrEqual" criterion on this field. Note that subsequent calls to [getCriterion()](#method-daterangeitemgetcriterion) will return this more complex criterion.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criterion | [Criterion](#type-criterion) | false | — | criterion to test |

### Returns

`[boolean](../reference.md#type-boolean)` — returns true if this criterion can be edited by this item

### Groups

- criteriaEditing

---
## Method: DateRangeItem.validateRange

### Description
Validate both _"to"_ and _"from"_ date-fields.

### Returns

`[Boolean](#type-boolean)` — false if either _to_ or _from_ field contains an invalid date value.

---
## Method: DateRangeItem.setFromDate

### Description
Sets the [DateRangeItem.fromDate](#attr-daterangeitemfromdate) for this DateRangeItem.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fromDate | [Date](#type-date)|[RelativeDateString](../reference_2.md#type-relativedatestring)|[TimeUnit](../reference_2.md#type-timeunit) | false | — | the date from which this item should start it's range |

---
## Method: DateRangeItem.setValue

### Description
Sets the value for this dateRangeItem. The value parameter is a [DateRange](../reference_2.md#object-daterange) object that optionally includes both start and end values. If passed null, both start- and end-range values are cleared.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [DateRange](#type-daterange) | false | — | the new value for this item |

---
## Method: DateRangeItem.setCriterion

### Description
Applies the specified criterion to this item for editing. Applies any specified "greaterOrEqual" operator criterion or sub-criterion to our [fromField](#attr-daterangeitemfromfield) and any specified "lessOrEqual" operator criterion or sub-criterion to our [toField](#attr-daterangeitemtofield).

Note that a single "equals" criterion can also be passed. See [canEditCriterion()](#method-daterangeitemcaneditcriterion) for more detail.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criterion | [Criterion](#type-criterion) | false | — | criterion to edit |

### Groups

- criteriaEditing

---
## Method: DateRangeItem.setToDate

### Description
Sets the [DateRangeItem.toDate](#attr-daterangeitemtodate) for this DateRangeItem.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fromDate | [Date](#type-date)|[RelativeDateString](../reference_2.md#type-relativedatestring)|[TimeUnit](../reference_2.md#type-timeunit) | false | — | the date at which this item should end it's range |

---
## Method: DateRangeItem.getCriterion

### Description
Returns the Criterion entered in the date field.

A Criterion with an "and" [operator](../reference.md#type-operatorid) will be returned with both a "greaterOrEqual" and "lessOrEqual" sub-criteria. If either date is omitted, only the "greaterOrEqual" (from date) or "lessOrEqual" (to date) Criterion is included.

### Returns

`[Criterion](#type-criterion)` — —

### Groups

- criteriaEditing

---
## Method: DateRangeItem.getValue

### Description
Retrieves the current value of this dateRangeItem. The return value is a [DateRange](../reference_2.md#object-daterange) object that excludes start and end values if they aren't set.

### Returns

`[DateRange](#type-daterange)` — the current value of this item

---
## Method: DateRangeItem.hasAdvancedCriteria

### Description
Overridden to return true: dateRangeItems always generate AdvancedCriteria.

### Returns

`[Boolean](#type-boolean)` — true

### Groups

- criteriaEditing

---
