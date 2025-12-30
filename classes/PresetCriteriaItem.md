# PresetCriteriaItem Documentation

[← Back to API Index](../reference.md)

---

## Class: PresetCriteriaItem

*Inherits from:* [SelectItem](SelectItem.md#class-selectitem)

### Description
A FormItem for use with the [FilterBuilder](FilterBuilder.md#class-filterbuilder), allows the user to pick from a set of pre-configured search criteria such as specific ranges in numeric or date data, and provide user friendly titles for such criteria, such as "within the next two weeks" or "High (0.75 - 0.99)".

---
## Attr: PresetCriteriaItem.shouldSaveValue

### Description
Should this item's value be saved in the form's values and hence returned from [form.getValues()](DynamicForm.md#method-dynamicformgetvalues)?

`shouldSaveValue:false` is used to mark formItems which do not correspond to the underlying data model and should not save a value into the form's [values](DynamicForm.md#attr-dynamicformvalues). Example includes visual separators, password re-type fields, or checkboxes used to show/hide other form items.

A `shouldSaveValue:false` item should be given a value either via [FormItem.defaultValue](FormItem.md#attr-formitemdefaultvalue) or by calling [form.setValue(item, value)](DynamicForm.md#method-dynamicformsetvalue) or [formItem.setValue(value)](FormItem.md#method-formitemsetvalue). Providing a value via [form.values](DynamicForm.md#attr-dynamicformvalues) or [form.setValues()](DynamicForm.md#method-dynamicformsetvalues) will automatically switch the item to `shouldSaveValue:true`.

Note that

*   if an item is shouldSaveValue true, but has no name, a warning is logged, and shouldSaveValue will be set to false.

### Groups

- formValues

**Flags**: IR

---
## Attr: PresetCriteriaItem.options

### Description
An object whose properties are user-visible titles for the preset ranges, and whose values are Criteria / AdvancedCriteria objects representing the criteria to be used if the user selects that choice.

**Flags**: IR

---
## Attr: PresetCriteriaItem.customOptionTitle

### Description
The title to show for the [custom option](#attr-presetcriteriaitemshowcustomoption).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: PresetCriteriaItem.valueMap

### Description
This attribute is not applicable to the PresetCriteriaItem. See [PresetCriteriaItem.options](#attr-presetcriteriaitemoptions) instead.

**Flags**: IR

---
## Attr: PresetCriteriaItem.showCustomOption

### Description
If set, an additional option will be shown with the title [PresetCriteriaItem.customOptionTitle](#attr-presetcriteriaitemcustomoptiontitle), which will cause [PresetCriteriaItem.getCustomCriteria](#method-presetcriteriaitemgetcustomcriteria) to be called.

**Flags**: IR

---
## Method: PresetCriteriaItem.getCustomCriteria

### Description
This method is called when [PresetCriteriaItem.showCustomOption](#attr-presetcriteriaitemshowcustomoption) is true and the user selects the custom option. Implement this method by allowing the user to enter custom criteria, for example, by opening a modal dialog. Once the user has input custom criteria, fire the callback method with the resulting criteria.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [Callback](../reference.md#type-callback) | false | — | callback to fire when custom criteria has been gathered. Expects parameters "criteria,title". The "title" will be displayed as the currently selected value when custom criteria have been chosen. |

**Flags**: A

---
## Method: PresetCriteriaItem.getCriterion

### Description
Get the criterion based on the value selected by the user.

### Returns

`[Criterion](#type-criterion)|[AdvancedCriteria](#type-advancedcriteria)` — the criteria for the selected option

---
