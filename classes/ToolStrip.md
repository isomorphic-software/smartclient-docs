# ToolStrip Documentation

[← Back to API Index](../reference.md)

---

## Class: ToolStrip

*Inherits from:* [Layout](Layout.md#class-layout)

### Description
Base class for creating toolstrips like those found in browsers and office applications: a mixed set of controls including [icon buttons](ImgButton.md#class-imgbutton), [radio button groups](Button.md#attr-buttonradiogroup), [menus](MenuButton.md#class-menubutton), [comboBoxes](ComboBoxItem.md#class-comboboxitem), [spacers](../reference.md#class-layoutspacer), [status displays](Label.md#class-label) and [drop-down selects](SelectItem.md#class-selectitem).

All of the above components are placed in the [members array](#attr-toolstripmembers) to form a ToolStrip. Note that the [FormItems](FormItem.md#class-formitem) mentioned above (ComboBox and drop-down selects) need to be placed within a [DynamicForm](DynamicForm.md#class-dynamicform) as usual.

The following strings can be used to add special behaviors:

*   the String "separator" will cause a separator to be created (instance of [ToolStrip.separatorClass](#attr-toolstripseparatorclass))
*   the String "resizer" will cause a resizer to be created (instance of [ToolStrip.resizeBarClass](#attr-toolstripresizebarclass)). This is equivalent to setting [showResizeBar:true](Canvas.md#attr-canvasshowresizebar) on the preceding member.
*   the String "starSpacer" will cause a spacer to be created (instance of [LayoutSpacer](../reference.md#class-layoutspacer)).

---
## Attr: ToolStrip.verticalStyleName

### Description
Default stylename to use if [this.vertical](#attr-toolstripvertical) is true. If unset, the standard [ToolStrip.styleName](#attr-toolstripstylename) will be used for both vertical and horizontal toolstrips.

Note that this property only applies to the widget at init time. To modify the styleName after this widget has been initialized, you should simply call [setStyleName()](Canvas.md#method-canvassetstylename) rather than updating this property.

### Groups

- appearance

**Flags**: IR

---
## Attr: ToolStrip.separatorBreadth

### Description
Separator height, when vertical is true, or width otherwise.

**Flags**: IR

---
## Attr: ToolStrip.vertical

### Description
Indicates whether the components are drawn horizontally from left to right (false), or vertically from top to bottom (true).

### Groups

- appearance

**Flags**: IR

---
## Attr: ToolStrip.resizeBarSize

### Description
Thickness of the resizeBars in pixels.

**Flags**: IRA

---
## Attr: ToolStrip.formWrapperDefaults

### Description
Default properties to apply to [ToolStrip.formWrapper](#attr-toolstripformwrapper) components.

The default configuration will has the following settings:

*   [DynamicForm.numCols](DynamicForm.md#attr-dynamicformnumcols) set to `2`
*   [DynamicForm.overflow](Canvas.md#attr-canvasoverflow) set to `"visible"`
*   [DynamicForm.width](Canvas.md#attr-canvaswidth) and [DynamicForm.height](Canvas.md#attr-canvasheight) set to `1`

To customize the wrapper form for an individual item, use the `formProperties` argument of [ToolStrip.addFormItem](#method-toolstripaddformitem).

**Flags**: IR

---
## Attr: ToolStrip.separatorClass

### Description
Class to create when the string "separator" appears in [ToolStrip.members](#attr-toolstripmembers).

**Flags**: IR

---
## Attr: ToolStrip.members

### Description
Array of components that will be contained within this Toolstrip, like [Layout.members](Layout.md#attr-layoutmembers). Built-in special behaviors can be indicated as describe [here](#class-toolstrip).

**Flags**: IR

---
## Attr: ToolStrip.formWrapperProperties

### Description
Properties to apply to [ToolStrip.formWrapper](#attr-toolstripformwrapper) components.

**Flags**: IR

---
## Attr: ToolStrip.resizeBarClass

### Description
Customized resizeBar with typical appearance for a ToolStrip.

**Flags**: IR

---
## Attr: ToolStrip.separatorSize

### Description
Separator thickness in pixels

**Flags**: IR

---
## Attr: ToolStrip.height

### Description
ToolStrips set a default [height](Canvas.md#attr-canvasheight) to avoid being stretched by containing layouts.

### Groups

- sizing

**Flags**: IRW

---
## Attr: ToolStrip.formWrapperConstructor

### Description
SmartClient class for generated [ToolStrip.formWrapper](#attr-toolstripformwrapper) components.

**Flags**: IRA

---
## Attr: ToolStrip.styleName

### Description
CSS class applied to this toolstrip.

Note that if [ToolStrip.vertical](#attr-toolstripvertical) is true for this toolStrip, [ToolStrip.verticalStyleName](#attr-toolstripverticalstylename) will be used instead of this value if it is non-null.

### Groups

- appearance

**Flags**: IRW

---
## Attr: ToolStrip.formWrapper

### Description
DynamicForm instance created by [ToolStrip.addFormItem](#method-toolstripaddformitem) to contain form items for display in this toolStrip. Each time addFormItem() is run, a new formWrapper autoChild will be created, picking up properties according to the standard [AutoChild](../reference.md#type-autochild) pattern.

**Flags**: IR

---
## Method: ToolStrip.addFormItem

### Description
Add a form item to this toolStrip. This method will create a DynamicForm autoChild with the item passed in as a single item, based on the [formWrapper config](#attr-toolstripformwrapper), and add it to the toolstrip as a member.

Returns a pointer to the generated formWrapper component.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| formItem | [FormItem Properties](#type-formitem-properties) | false | — | properties for the form item to add to this toolStrip. |
| formProperties | [DynamicForm Properties](#type-dynamicform-properties) | true | — | properties to apply to the generated formWrapper component. If passed, specified properties will be overlaid onto the properties derived from [ToolStrip.formWrapperDefaults](#attr-toolstripformwrapperdefaults) and [ToolStrip.formWrapperProperties](#attr-toolstripformwrapperproperties). |
| position | [Integer](../reference_2.md#type-integer) | true | — | desired position for the form item in the tools |

### Returns

`[DynamicForm](#type-dynamicform)` — generated wrapper containing the form item.

---
