# CanvasItem Documentation

[← Back to API Index](../reference.md)

---

## Class: CanvasItem

*Inherits from:* [FormItem](FormItem.md#class-formitem)

### Description
FormItem which renders a Canvas inline in a DynamicForm instance.

CanvasItem is [shouldSaveValue](#attr-canvasitemshouldsavevalue):false by default, meaning that no value from the CanvasItem will be present in [DynamicForm.getValues](DynamicForm.md#method-dynamicformgetvalues) and no value will be saved when [DynamicForm.saveData](DynamicForm.md#method-dynamicformsavedata) is called. This is appropriate if the Canvas does not participate in editing a value of the form and is embedded in the form for layout or UI purposes only (e.g. [ButtonItem](ButtonItem.md#class-buttonitem), [SectionItem](SectionItem.md#class-sectionitem)). Note that some built-in CanvasItem types override the shouldSaveValue default to true (e.g. [MultiComboBoxItem](MultiComboBoxItem.md#class-multicomboboxitem), [RichTextItem](RichTextItem.md#class-richtextitem)).

If you set [shouldSaveValue](FormItem.md#attr-formitemshouldsavevalue):true, a [showValue](#method-canvasitemshowvalue) event will be raised to provide a value that your item should display. Handle this event by calling methods on the Canvas you've created to cause the value to be displayed.

The [showValue](#method-canvasitemshowvalue) event will be triggered in various situations where the form receives data, including a call to [DynamicForm.setValues](DynamicForm.md#method-dynamicformsetvalues), [DynamicForm.editRecord](DynamicForm.md#method-dynamicformeditrecord), or if [DynamicForm.fetchData](DynamicForm.md#method-dynamicformfetchdata) is called and a Record is returned. Bear in mind that the `showValue` event can be called when the form and your item have not yet been drawn; in this case, store the value for later display.

To provide a value to the form, call [CanvasItem.storeValue](#method-canvasitemstorevalue) whenever the user changes the value in your Canvas. Generally, if storeValue() is called then [shouldSaveValue](#attr-canvasitemshouldsavevalue) should be overridden to true. Note that the form **will not** call getValue() in order to discover your item's value, so there is no purpose in overriding this method; instead, call storeValue() to proactively inform the form about changes to the value. This approach is necessary in order to enable change events.

If you cannot easily detect changes to values in your Canvas, a workaround is to call `storeValue` right before the form saves.

---
## Attr: CanvasItem.canvas

### Description
The canvas that will be displayed inside this item. You can pass an instance you've already created, or its global ID as a String. You can also implement [CanvasItem.createCanvas](#method-canvasitemcreatecanvas) to dynamically create the canvas when the FormItem is initialized.

If `canvas` and `createCanvas()` are unspecified, the canvas for this item will be auto-created using the overrideable defaults: [CanvasItem.canvasProperties](#attr-canvasitemcanvasproperties) and [CanvasItem.canvasConstructor](#attr-canvasitemcanvasconstructor)

Note that subclasses of `CanvasItem` may use a different AutoChild name than just "canvas". For example, [SliderItem](SliderItem.md#class-slideritem) uses "slider", and in that case, you need to use the specific APIs provided by the subclass.

Note that [Canvas.canvasItem](Canvas.md#attr-canvascanvasitem) will be set on the canvas to point back to this item.

### See Also

- [autoChildUsage](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren)

**Flags**: IRW

---
## Attr: CanvasItem.prompt

### Description
This text is shown as a tooltip prompt when the cursor hovers over this item.

When item is [read-only](FormItem.md#method-formitemsetcanedit) a different hover can be shown with [FormItem.readOnlyHover](FormItem.md#attr-formitemreadonlyhover). Or, when item is [disabled](FormItem.md#attr-formitemdisabled) or read-only with [readOnlyDisplay:disabled](FormItem.md#attr-formitemreadonlydisplay) a different hover can be shown with [FormItem.disabledHover](FormItem.md#attr-formitemdisabledhover).

Note that when the form is [disabled](Canvas.md#attr-canvasdisabled) this prompt will not be shown.

### Groups

- basics

**Flags**: IRW

---
## Attr: CanvasItem.editCriteriaInInnerForm

### Description
Flag to disable the criteria editing overrides described in [CanvasItem.getCriterion](#method-canvasitemgetcriterion) whereby if this item contains a DynamicForm as its canvas, it will be used to edit nested AdvancedCriteria automatically.

This flag is required for cases where a canvasItem contains a DynamicForm, but the form is not set up to show inner field values of nested objects, and therefore should not attempt to apply nested advanced criteria directly to the form.

**Flags**: IRA

---
## Attr: CanvasItem.minHeight

### Description
Minimum valid height for this CanvasItem in pixels. Used in calculating the row heights of the containing [DynamicForm](DynamicForm.md#class-dynamicform) if the item has a flexible [CanvasItem.height](#attr-canvasitemheight).

**Flags**: IRW

---
## Attr: CanvasItem.maxHeight

### Description
Maximum valid height for this CanvasItem in pixels. Used in calculating the row heights of the containing [DynamicForm](DynamicForm.md#class-dynamicform) if the item has a flexible [CanvasItem.height](#attr-canvasitemheight).

**Flags**: IRW

---
## Attr: CanvasItem.canvasConstructor

### Description
If [this.canvas](#attr-canvasitemcanvas) is not specified as a canvas instance at init time, a canvas will be created instead. This property denotes the class of that widget (Should be set to the name of a subclass of Canvas).

**Flags**: IRW

---
## Attr: CanvasItem.canvasDefaults

### Description
Default properties for the canvas if this.canvas is not already a canvas instance.

**Flags**: IRW

---
## Attr: CanvasItem.multiple

### Description
Whether this CanvasItem is intended to hold multiple values.

**Flags**: IR

---
## Attr: CanvasItem.overflow

### Description
CanvasItems support specifying overflow for the Canvas directly on the item.

**Flags**: IR

---
## Attr: CanvasItem.applyPromptToCanvas

### Description
If [FormItem.prompt](FormItem.md#attr-formitemprompt) is specified for this item, should the prompt be applied to the [CanvasItem.canvas](#attr-canvasitemcanvas) for this item?

**Flags**: IRW

---
## Attr: CanvasItem.height

### Description
Height of the Canvas. Can be either a number indicating a fixed height in pixels, a percentage indicating a percentage of the overall form's height, or "\*" indicating take whatever remaining space is available. See the [formLayout](../kb_topics/formLayout.md#kb-topic-form-layout) overview for details.

Height may also be explicitly specified on the [CanvasItem.canvas](#attr-canvasitemcanvas). In this any `canvasItem.height` will be ignored in favor of the value applied to the canvas directly. In either case, percentage values will be resolved using standard formItem sizing rules as described in [formLayout](../kb_topics/formLayout.md#kb-topic-form-layout)

**Flags**: IRW

---
## Attr: CanvasItem.autoDestroy

### Description
Should this item's [canvas](#attr-canvasitemcanvas) be automatically destroyed when the item is destroyed? Form items are destroyed automatically when a call to [DynamicForm.setItems](DynamicForm.md#method-dynamicformsetitems) removes them from their parent form, or if their parent form is destroyed. This property governs whether, when this occurs, the item's canvas should also be [destroyed](Canvas.md#method-canvasdestroy).

This property has no effect for canvases automatically created via the "autoChild" pattern, using [CanvasItem.canvasProperties](#attr-canvasitemcanvasproperties), [CanvasItem.canvasDefaults](#attr-canvasitemcanvasdefaults) etc. CanvasItems which create their canvas in this way will always destroy the canvas when the item is destroyed or on an explicit [CanvasItem.setCanvas](#method-canvasitemsetcanvas) call, regardless of this property's value.

Setting this property to true is typically appropriate for cases where a custom CanvasItem automatically creates its canvas as part of its initialization flow, and the canvas will not be re-used outside the item.  
Note that once a canvas has been destroyed it can not be re-used elsewhere within an application.

**Flags**: IRWA

---
## Attr: CanvasItem.shouldSaveValue

### Description
Should this item's value be saved in the form's values and hence returned from [DynamicForm.getValues](DynamicForm.md#method-dynamicformgetvalues)?

Note that by default, `shouldSaveValue` is false for CanvasItems, meaning that no value from the CanvasItem will be present in [DynamicForm.getValues](DynamicForm.md#method-dynamicformgetvalues) and no value for the CanvasItem will be saved when [DynamicForm.saveData](DynamicForm.md#method-dynamicformsavedata) is called. See the [CanvasItem](#class-canvasitem) class overview for a discussion of values handling in CanvasItems.

**Flags**: IR

---
## Attr: CanvasItem.canvasProperties

### Description
Properties to apply to this canvas on creation if this.canvas is not already a canvas instance.

**Flags**: IRW

---
## Method: CanvasItem.setPrompt

### Description
Set the [FormItem.prompt](FormItem.md#attr-formitemprompt) for this item. Default implementation will also apply the prompt to [CanvasItem.canvas](#attr-canvasitemcanvas) if [CanvasItem.applyPromptToCanvas](#attr-canvasitemapplyprompttocanvas) is true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| prompt | [HTMLString](../reference.md#type-htmlstring) | false | — | new prompt for the item. |

---
## Method: CanvasItem.setCanvas

### Description
Setter to update the [CanvasItem.canvas](#attr-canvasitemcanvas) at runtime

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canvas | [Canvas](#type-canvas) | false | — | New canvas to display. |

---
## Method: CanvasItem.getCriterion

### Description
The standard formItem criteria editing APIs have been overridden in the canvasItem class to simplify the editing of complex [AdvancedCriteria](../reference.md#object-advancedcriteria) objects using nested DynamicForms.

The following pattern is supported without need for further modification:  
A complex Advanced criteria object may have nested sub criteria using the `"and"` or `"or"` operators. For example:

```
 { _constructor:"AdvancedCriteria",
   operator:"and",
   criteria:[
      {fieldName:"field1", value:"value1", operator:"iContains"},
      {operator:"or", criteria:[
          {fieldName:"innerField1", value:"value1", operator:"equals"},
          {fieldName:"innerField2", value:"value2", operator:"iContains"}
       ]
      }
   ]
 }
 
```
To create a form capable of editing the above criteria without providing custom overrides to [FormItem.getCriterion](FormItem.md#method-formitemgetcriterion) et al, you would create a form with 2 items. The 'field1' criterion could be edited by a simple form item such as a TextItem. The nested criteria ('innerField1' and 'innerField2') could be edited by a canvasItem whose canvas property was set to a DynamicForm showing items capable of editing the 2 inner criteria, and whose operator was specified as "or".  
For example:
```
  isc.DynamicForm.create({
      items:[
          {name:"field1", type:"TextItem"},
          {name:"nestedItem", shouldSaveValue:true, type:"CanvasItem",
              canvas:isc.DynamicForm.create({
                  operator:"or",
                  items:[
                      {name:"innerField1", type:"TextItem", operator:"equals"},
                      {name:"innerField2", type:"TextItem"}
                  ]
              })
          }
      ]
  });
 
```
This form would be able to edit the above advanced criteria object via [DynamicForm.setValuesAsCriteria](DynamicForm.md#method-dynamicformsetvaluesascriteria). Edited values would be retrieved via [DynamicForm.getValuesAsCriteria](DynamicForm.md#method-dynamicformgetvaluesascriteria).

Note that the canvas item has `shouldSaveValue` set to true - this is required to ensure the nested form is actually passed the values to edit.

The default implementation of this method checks for this.canvas being specified as a dynamicForm, and in that case simply returns the result of [DynamicForm.getValuesAsAdvancedCriteria](DynamicForm.md#method-dynamicformgetvaluesasadvancedcriteria) on the inner form.

Note that this functionality may be entirely bypassed by setting [CanvasItem.editCriteriaInInnerForm](#attr-canvasitemeditcriteriaininnerform) to false. This flag is useful when defining a dynamicForm based canvasItem which is not intended for editing nested data -- for example if a standard atomic field value is being displayed in some custom way using a DynamicForm embedded in the item.

### Returns

`[Criterion](#type-criterion)` — criterion to merge with advanced criteria returned by [DynamicForm.getValuesAsCriteria](DynamicForm.md#method-dynamicformgetvaluesascriteria)

### Groups

- criteriaEditing

---
## Method: CanvasItem.canEditChanged

### Description
Notification method called when the [canEdit](FormItem.md#attr-formitemcanedit) setting is modified. Developers may make use of this to toggle between an editable and a read-only appearance of the [canvas](#attr-canvasitemcanvas).

The default behavior is:

*   If `canvas` is a [DynamicForm](DynamicForm.md#class-dynamicform), the form's [DynamicForm.canEdit](DynamicForm.md#attr-dynamicformcanedit) setting is set to `canEdit`.
*   [CanvasItem.shouldDisableCanvas](#method-canvasitemshoulddisablecanvas) is called to determine if the `canvas` should be disabled.

Standard `CanvasItem`\-based form items may customize the default behavior. For example, a [MultiComboBoxItem](MultiComboBoxItem.md#class-multicomboboxitem) will hide its [comboForm](MultiComboBoxItem.md#attr-multicomboboxitemcomboform) if the [readOnlyDisplay](FormItem.md#attr-formitemreadonlydisplay) is "readOnly" or "static" and also disable the buttons when made read-only.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canEdit | [boolean](../reference.md#type-boolean) | false | — | New `canEdit` value |

### Returns

`[boolean](../reference.md#type-boolean)` — `false` to cancel the default behavior.

### See Also

- [CanvasItem.readOnlyDisplayChanged](#method-canvasitemreadonlydisplaychanged)

---
## Method: CanvasItem.createCanvas

### Description
This method allows dynamic creation of a CanvasItem's canvas, rather than setting [CanvasItem.canvas](#attr-canvasitemcanvas) statically. If specified this [StringMethod](../reference.md#kb-topic-string-methods-overview) will be called when the form item is initialized and should return the Canvas to display for this item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | the dynamicForm in which this item is contained |
| item | [CanvasItem](#type-canvasitem) | false | — | the live form item instance |

### Returns

`[Canvas](#type-canvas)` — the canvas to be rendered inside this CanvasItem

---
## Method: CanvasItem.setCriterion

### Description
Display a [Criterion](../reference.md#object-criterion) object in this item for editing. Overridden from [FormItem.setCriterion](FormItem.md#method-formitemsetcriterion) in order to support editing nested criteria using nested dynamicForms as described in [CanvasItem.getCriterion](#method-canvasitemgetcriterion).

Implementation checks for this.canvas being specified as a DynamicForm, and applies criterion directly to the embedded form via setValuesAsCriteria()

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criterion | [Criterion](#type-criterion) | false | — | criteria to edit |

### Groups

- criteriaEditing

---
## Method: CanvasItem.updateCanvasTabPosition

### Description
This method will place an entry for the [CanvasItem.canvas](#attr-canvasitemcanvas) under this item in the [TabIndexManager](TabIndexManager.md#class-tabindexmanager). This ensures the user can tab into the canvas (and its descendants) in the expected position within this item's DynamicForm.

See also [Canvas.updateChildTabPositions](Canvas.md#method-canvasupdatechildtabpositions).

---
## Method: CanvasItem.canEditCriterion

### Description
AdvancedCriteria objects may be edited via nested dynamicForms as described in [CanvasItem.getCriterion](#method-canvasitemgetcriterion)

This method has been overridden to return true if this item's canvas is a DynamicForm, where the [DynamicForm.operator](DynamicForm.md#attr-dynamicformoperator) matches the operator of the criterion passed in and dynamicForm contains items where [FormItem.canEditCriterion](FormItem.md#method-formitemcaneditcriterion) returns true for each sub-criterion in the object passed in.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criterion | [Criterion](#type-criterion) | false | — | criteria to test |

### Returns

`[boolean](../reference.md#type-boolean)` — returns true if the specified criterion may be edited by this item

### Groups

- criteriaEditing

---
## Method: CanvasItem.hasAdvancedCriteria

### Description
Overridden to return true if [CanvasItem.canvas](#attr-canvasitemcanvas) is a dynamicForm. See [CanvasItem.getCriterion](#method-canvasitemgetcriterion) for details of editing advanced criteria using nested dynamicForms.

### Returns

`[Boolean](#type-boolean)` — true if this item's canvas is a DynamicForm

### Groups

- criteriaEditing

---
## Method: CanvasItem.isFocused

### Description
Does this CanvasItem have keyboard focus.

This method will return true if this item's canvas, or any of its descendents, has keyboard focus

### Returns

`[Boolean](#type-boolean)` — returns true if this item contains focus.

---
## Method: CanvasItem.shouldDisableCanvas

### Description
Method called to determine whether the [canvas](#attr-canvasitemcanvas) should be [disabled](Canvas.md#method-canvassetdisabled) when this `CanvasItem` is disabled or its [editability changes](#method-canvasitemcaneditchanged). By default, if the `canvas` is a [DynamicForm](DynamicForm.md#class-dynamicform), then it is disabled if and only if this `CanvasItem` is disabled; otherwise, the `canvas` is disabled if and only if this `CanvasItem` is disabled or [read-only](FormItem.md#method-formitemgetcanedit).

This method may be overridden to customize the default return value.

### Returns

`[boolean](../reference.md#type-boolean)` — `true` if the `canvas` should be disabled; `false` otherwise.

---
## Method: CanvasItem.readOnlyDisplayChanged

### Description
Notification method called when the [readOnlyDisplay](FormItem.md#attr-formitemreadonlydisplay) setting is modified. Developers may make use of this to toggle between an editable and a read-only appearance of the [canvas](#attr-canvasitemcanvas).

The default behavior is: when the `canvas` is a [DynamicForm](DynamicForm.md#class-dynamicform), the form's [DynamicForm.readOnlyDisplay](DynamicForm.md#attr-dynamicformreadonlydisplay) setting is set to `appearance`.

Standard `CanvasItem`\-based form items may customize the default behavior.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| appearance | [ReadOnlyDisplayAppearance](../reference.md#type-readonlydisplayappearance) | false | — | new `readOnlyDisplay` value |

### Returns

`[boolean](../reference.md#type-boolean)` — `false` to cancel the default behavior.

### See Also

- [CanvasItem.canEditChanged](#method-canvasitemcaneditchanged)

---
## Method: CanvasItem.storeValue

### Description
Store (and optionally show) a value for this form item.

This method will fire standard [FormItem.change](FormItem.md#method-formitemchange) and [DynamicForm.itemChanged](DynamicForm.md#method-dynamicformitemchanged) handlers, and store the value passed in such that subsequent calls to [FormItem.getValue](FormItem.md#method-formitemgetvalue) or [DynamicForm.getValue](DynamicForm.md#method-dynamicformgetvalue) will return the new value for this item.

This method is intended to provide a way for custom formItems - most commonly [canvasItems](#class-canvasitem) - to provide a new interface to the user, allowing them to manipulate the item's value, for example in an embedded [CanvasItem.canvas](#attr-canvasitemcanvas), or a pop-up dialog launched from an [icon](../reference_2.md#object-formitemicon), etc. Developers should call this method when the user interacts with this custom interface in order to store the changed value.

[shouldSaveValue](#attr-canvasitemshouldsavevalue) for CanvasItems is false by default. Custom CanvasItems will need to override shouldSaveValue to true if the values stored via this API should be included in the form's [getValues()](DynamicForm.md#method-dynamicformgetvalues) and saved with the form when [saveData()](DynamicForm.md#method-dynamicformsavedata) is called.

If you cannot easily detect interactions that should change the value as the user performs them, a workaround is to call `storeValue` right before the form saves.

Note that this method is not designed for customizing a value which is already being saved by a standard user interaction. For example you should not call this method from a [change handler](FormItem.md#method-formitemchange). Other APIs such as [FormItem.transformInput](FormItem.md#method-formitemtransforminput) exist for this.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | value to save for this item |
| showValue | [Boolean](#type-boolean) | true | — | Should the formItem be updated to display the new value? |

---
## Method: CanvasItem.showValue

### Description
This method will be called whenever this FormItem's value is being set via a programmatic call to e.g: [DynamicForm.setValues](DynamicForm.md#method-dynamicformsetvalues) or [FormItem.setValue](FormItem.md#method-formitemsetvalue) and may be overridden by CanvasItems intended to support displaying data values to update the embedded Canvas to reflect the value passed in. Note that the first parameter will be a formatted value - while the second parameter will contain the underlying data value for the item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| displayValue | [Any](#type-any) | false | — | new display value for the item. This is the value after applying any custom formatter or valueMap |
| dataValue | [Any](#type-any) | false | — | underlying data value for the item |
| form | [DynamicForm](#type-dynamicform) | false | — | the dynamicForm in which this item is contained |
| item | [CanvasItem](#type-canvasitem) | false | — | the live form item instance |

---
