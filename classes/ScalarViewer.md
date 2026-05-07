# ScalarViewer Documentation

[← Back to API Index](../reference.md)

---

## Class: ScalarViewer

*Inherits from:* [DynamicForm](DynamicForm.md#class-dynamicform)

### Description
A DynamicForm subclass for displaying a single value from a data object.

The ScalarViewer creates a single item based on the specified [FieldName](../reference.md#type-fieldname) and [title](#title) in order to display the value for a single field to the user.

The item may be customized via the [autoChild](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) pattern. See [ScalarViewer.valueItem](#attr-scalarviewervalueitem).

---
## Attr: ScalarViewer.fieldName

### Description
[name](FormItem.md#attr-formitemname) for the [ScalarViewer.valueItem](#attr-scalarviewervalueitem)

**Flags**: IRW

---
## Attr: ScalarViewer.initialSort

### Description
An array of [SortSpecifier](../reference_2.md#object-sortspecifier) objects used to set up the initial sort configuration for this form.

### Groups

- sorting

**Flags**: IR

---
## Attr: ScalarViewer.valueItem

### Description
Single item for displaying a value from a data object.

This item will have [name](FormItem.md#attr-formitemname) set to [this.fieldName](../reference.md#type-fieldname) and title set to [this.title](#attr-scalarviewertitle).

Other properties are derived from [ScalarViewer.valueItemDefaults](#attr-scalarviewervalueitemdefaults) and [ScalarViewer.valueItemProperties](#attr-scalarviewervalueitemproperties) using the auto-child pattern.

**Flags**: IR

---
## Attr: ScalarViewer.title

### Description
[title](FormItem.md#attr-formitemtitle) for the [ScalarViewer.valueItem](#attr-scalarviewervalueitem)

**Flags**: IRW

---
## Attr: ScalarViewer.valueItemProperties

### Description
Optional [autoChild properties](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) to customize the generated [ScalarViewer.valueItem](#attr-scalarviewervalueitem).

**Flags**: IR

---
## Attr: ScalarViewer.valueItemDefaults

### Description
Defaults for the generated [ScalarViewer.valueItem](#attr-scalarviewervalueitem).

By default the valueItem will be a StaticTextItem with [titleOrientation:"top"](FormItem.md#attr-formitemtitleorientation).

**Flags**: IR

---
## Method: ScalarViewer.setFieldName

### Description
Set the [FieldName](../reference.md#type-fieldname) at runtime. This will rebuild the [ScalarViewer.valueItem](#attr-scalarviewervalueitem).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | new fieldName to use |

---
## Method: ScalarViewer.setTitle

### Description
Set the [ScalarViewer.title](#attr-scalarviewertitle) at runtime of the [ScalarViewer.valueItem](#attr-scalarviewervalueitem).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| title | [String](#type-string) | false | — | new title to use |

---
