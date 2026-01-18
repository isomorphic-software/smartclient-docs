# FormItem Documentation

[← Back to API Index](../reference.md)

---

## Class: FormItem

### Description
A UI component that can participate in a DynamicForm, allowing editing or display of one of the [values tracked by the form](DynamicForm.md#attr-dynamicformvalues).

FormItems are never created via the [create()](Class.md#classmethod-classcreate) method, instead, an Array of plain [JavaScript objects](../reference.md#type-object) are passed as [DynamicForm.items](DynamicForm.md#attr-dynamicformitems) when the form is created.

See the [DynamicForm](DynamicForm.md#class-dynamicform) documentation for details and sample code.

---
## ClassAttr: FormItem.defaultPickerIconHeight

### Description
Default [height](FormItemIcon.md#attr-formitemiconheight) value for pickers created by [FormItem.getPickerIcon](#classmethod-formitemgetpickericon).

**Flags**: IR

---
## ClassAttr: FormItem.defaultPickerIconSpace

### Description
Default [hspace](FormItemIcon.md#attr-formitemiconhspace) value for pickers created by [FormItem.getPickerIcon](#classmethod-formitemgetpickericon).

**Flags**: IR

---
## Attr: FormItem.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: FormItem.exportFormat

### Description
[FormatString](../reference.md#type-formatstring) used during exports for numeric or date formatting. See [DataSourceField.exportFormat](DataSourceField.md#attr-datasourcefieldexportformat).

### Groups

- exportFormatting

**Flags**: IR

---
## Attr: FormItem.foreignDisplayField

### Description
For items with an [FormItem.optionDataSource](#attr-formitemoptiondatasource), this property specifies an explicit display field for records within the option dataSource. Typically this property will be set in conjunction with [FormItem.displayField](#attr-formitemdisplayfield) in the case where the name of the displayField within the record being edited differs from the displayField in the optionDataSource.

See [DataSourceField.foreignDisplayField](DataSourceField.md#attr-datasourcefieldforeigndisplayfield) for additional details.

### See Also

- [FormItem.getDisplayFieldName](#method-formitemgetdisplayfieldname)

**Flags**: IR

---
## Attr: FormItem.hoverPersist

### Description
Allows interaction with hovers when the cursor is positioned over them.

Overrides the [same attribute](Canvas.md#attr-canvashoverpersist) on the parent form.

### Groups

- hovers

### See Also

- [FormItem.hoverFocusKey](#attr-formitemhoverfocuskey)

**Flags**: IRW

---
## Attr: FormItem.showValueIconOnly

### Description
If [FormItem.valueIcons](#attr-formitemvalueicons) is set, this property may be set to show the valueIcon only and prevent the standard form item element or text from displaying

### Groups

- valueIcons

**Flags**: IRW

---
## Attr: FormItem.optionTextMatchStyle

### Description
If this item has a specified `optionDataSource`, this property determines the textMatchStyle to use when interpretating any [FormItem.optionCriteria](#attr-formitemoptioncriteria) during the fetch to map valueField values to displayField values.

### Groups

- databinding
- searchCriteria

**Flags**: IRA

---
## Attr: FormItem.linearEndRow

### Description
Specifies [FormItem.endRow](#attr-formitemendrow) for an item in [linearMode](DynamicForm.md#attr-dynamicformlinearmode), overriding the default of `true` in that mode.

### Groups

- formLayout

**Flags**: IRW

---
## Attr: FormItem.validateOnChange

### Description
If true, form items will be validated when each item's "change" handler is fired as well as when the entire form is submitted or validated.

Note that this property can also be set at the form level or on each validator; If true at the form or field level, validators not explicitly set with `validateOnChange:false` will be fired on change - displaying errors and rejecting the change on validation failure.

### Groups

- changeHandling

### See Also

- [DynamicForm.validateOnChange](DynamicForm.md#attr-dynamicformvalidateonchange)

**Flags**: IRW

---
## Attr: FormItem.hint

### Description
Specifies "hint" string to show next to the form item to indicate something to the user. This string generally appears to the right of the form item.

### Groups

- appearance

### See Also

- [FormItem.hintStyle](#attr-formitemhintstyle)

**Flags**: IRW

---
## Attr: FormItem.inputFormat

### Description
For fields of type `"date"`, if this is an editable field such as a [TextItem](TextItem.md#class-textitem), this property allows you to specify the [inputFormat](DateItem.md#attr-dateiteminputformat) applied to the item.

### See Also

- [FormItem.dateFormatter](#attr-formitemdateformatter)

**Flags**: IRWA

---
## Attr: FormItem.top

### Description
Top coordinate of this item in pixels. Applies only when the containing DynamicForm sets `itemLayout:"absolute"`.

**Flags**: IRWA

---
## Attr: FormItem.valueIconWidth

### Description
If [FormItem.valueIcons](#attr-formitemvalueicons) is specified, use this property to specify a width for the value icon written out.

### Groups

- valueIcons

### See Also

- [FormItem.valueIconHeight](#attr-formitemvalueiconheight)
- [FormItem.valueIconSize](#attr-formitemvalueiconsize)

**Flags**: IRW

---
## Attr: FormItem.linearColSpan

### Description
Specifies a column span for an item in [linearMode](DynamicForm.md#attr-dynamicformlinearmode), overriding the default value of "\*" in that mode.

### Groups

- formLayout

### See Also

- [FormItem.colSpan](#attr-formitemcolspan)

**Flags**: IRW

---
## Attr: FormItem.printTextBoxStyle

### Description
Base CSS class name for a form item's text box element when getting printable HTML for the form. If unset [FormItem.textBoxStyle](#attr-formitemtextboxstyle) will be used instead. Note that focused styling will never be displayed while printing, though error and disabled styling will.

By default this style will be used for printHTML for the item even if the item is [canEdit:false](#attr-formitemcanedit) with [readOnlyDisplay:static](#attr-formitemreadonlydisplay).  
To override this behavior, developers may also specify a custom print style for this state via the [FormItem.printReadOnlyTextBoxStyle](#attr-formitemprintreadonlytextboxstyle).

### Groups

- printing
- formItemStyling

**Flags**: IRW

---
## Attr: FormItem.picker

### Description
The component that will be displayed when [FormItem.showPicker](#method-formitemshowpicker) is called due to a click on the [picker icon](#attr-formitemshowpickericon).

Can be specified directly as a Canvas, or created automatically via the [AutoChild](../reference.md#type-autochild) pattern. The default autoChild configuration for the picker is a Canvas with backgroundColor set and no other modifications.

Note that the picker is not automatically destroyed with the FormItem that uses it, in order to allow recycling of picker components. To destroy a single-use picker, override [Canvas.destroy](Canvas.md#method-canvasdestroy).

**Flags**: IRW

---
## Attr: FormItem.hintClassName

### Description
CSS class for the "hint" string.

### Groups

- appearance

### See Also

- [FormItem.hint](#attr-formitemhint)

**Deprecated**

**Flags**: IR

---
## Attr: FormItem.type

### Description
The DynamicForm picks a field renderer based on the type of the field (and sometimes other attributes of the field).

In addition to the standard [FormItemType](../reference.md#type-formitemtype) values, this property also accepts the name of any [FormItem](#class-formitem) subclass (e.g., "ButtonItem", "CheckboxItem") or a shorthand lowercase version (e.g., "button", "checkbox"). When a class name or shorthand is provided, it acts as a shortcut for setting [FormItem.editorType](#attr-formitemeditortype).

### Groups

- appearance

### See Also

- [FormItemType](../reference.md#type-formitemtype)
- [FieldType](../reference_2.md#type-fieldtype)

**Flags**: IR

---
## Attr: FormItem.value

### Description
Value for this form item. This value may be set directly on the form item initialization block but is not updated on live items and should not be directly accessed. Once a form item has been created by the dynamicForm use [FormItem.setValue](#method-formitemsetvalue) and [FormItem.getValue](#method-formitemgetvalue) directly.

### Groups

- basics

**Flags**: IR

---
## Attr: FormItem.changeOnKeypress

### Description
Should this form item fire its [change](#method-formitemchange) handler (and store its value in the form) on every keypress? Set to `false` to suppress the 'change' handler firing (and the value stored) on every keypress.

Note: If `false`, the value returned by [getValue](#method-formitemgetvalue) will not reflect the value displayed in the form item element as long as focus is in the form item element.

### Groups

- eventHandling
- values

**Flags**: IRW

---
## Attr: FormItem.left

### Description
Left coordinate of this item in pixels. Applies only when the containing DynamicForm sets `itemLayout:"absolute"`.

**Flags**: IRWA

---
## Attr: FormItem.pickerIconPrompt

### Description
Prompt to show when the user hovers the mouse over the picker icon.

### Groups

- pickerIcon
- i18nMessages

**Flags**: IR

---
## Attr: FormItem.autoComplete

### Description
Should this item allow browser auto-completion of its value? Applies only to items based on native HTML form elements ([TextItem](TextItem.md#class-textitem), [PasswordItem](../reference.md#class-passworditem), etc), and will only have a user-visible impact for browsers where native autoComplete behavior is actually supported and enabled via user settings.

Alternatively, [FormItem.autoCompleteKeywords](#attr-formitemautocompletekeywords) can be specified, in which case this setting is ignored. If `autoCompleteKeywords` are not provided, and `autoComplete` is not set on this FormItem, the value of [DynamicForm.autoComplete](DynamicForm.md#attr-dynamicformautocomplete) is used.

Note that even with this value set to `"none"`, native browser auto-completion may occur for log in forms (forms containing username and [password](../reference.md#class-passworditem) fields). This behavior varies by browser, and is a result of an [intentional change by some browser developers](https://www.google.com/search?q=password+ignores+autocomplete+off) to disregard the HTML setting _autocomplete=off_ for password items or log-in forms.

In some browsers any form redraw (including a redraw from a call to [DynamicForm.setValues](DynamicForm.md#method-dynamicformsetvalues)) will re-populate the form with the natively remembered login credentials. This can make it very difficult to control the values displayed to the user, as a call to 'setValues()' may appear to be ignored. While behavior varies by browser we have specifically observed this behavior in Safari. Moreover in this browser, if the user asks the browser to remember login credentials for a URL, any form with a password item and a text item may be auto-filled with the remembered login credentials, even if the form's configuration and field names differ from those on the login form.

If an application has both an initial log in form, and a separate form within the application which makes contains a Password item (a use case might be an interface for a user with manager privileges for modifying other users' passwords), this will cause the second form to autofill with unexpected values.

Should this arise, developers can avoid this by making the initial log in interface into a separate log in page from the main application page. This is often good practice in any case for reasons outlined in the "Authentication" section of the Quick Start guide.

### Groups

- autoComplete

### See Also

- [DynamicForm.autoComplete](DynamicForm.md#attr-dynamicformautocomplete)

**Flags**: IRW

---
## Attr: FormItem.defaultOperator

### Description
The default search-operator for this item when it or its form allow [filter-expressions](#attr-formitemallowexpressions).

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: FormItem.titleErrorClassName

### Description
CSS class for a form item's title when a validation error is showing.

### Groups

- title

**Deprecated**

**Flags**: IR

---
## Attr: FormItem.colSpan

### Description
Number of columns that this item spans.

The `colSpan` setting does not include the title shown for items with [FormItem.showTitle](#attr-formitemshowtitle):true, so the effective `colSpan` is one higher than this setting for items that are showing a title and whose [TitleOrientation](../reference_2.md#type-titleorientation) is either "left" or "right".

### Groups

- formLayout

### See Also

- [FormItem.linearColSpan](#attr-formitemlinearcolspan)

**Flags**: IRW

---
## Attr: FormItem.browserSpellCheck

### Description
If this browser supports spell-checking of text editing elements, do we want this enabled for this item? If unset the property will be inherited from the containing form.

Notes:  
\- this property only applies to text based items such as TextItem and TextAreaItem.  
\- this property is not supported on all browsers.

### See Also

- [DynamicForm.browserSpellCheck](DynamicForm.md#attr-dynamicformbrowserspellcheck)

**Flags**: IRWA

---
## Attr: FormItem.dataPath

### Description
dataPath for this item. Allows the user to edit details nested data structures in a flat set of form fields

**NOTE: the dataPath feature is intended to help certain legacy architectures, such as systems that work in terms of exchanging large messages with several different entity types in one message, and are incapable of providing separate access to each entity type.  
See the [DataPath overview](../reference_2.md#type-datapath) for more information.**

Note that an item must have a valid dataPath or [name](#attr-formitemname) in order for its value to be validated and/or saved.

**Flags**: IR

---
## Attr: FormItem.imageURLPrefix

### Description
Prefix to apply to the beginning of any [FormItem.valueIcons](#attr-formitemvalueicons) when determining the URL for the image. Will not be applied if the `valueIcon` URL is absolute.

### Groups

- valueIcons

**Flags**: IRWA

---
## Attr: FormItem.hoverAlign

### Description
Text alignment for text displayed in this item's hover canvas, if shown.

### Groups

- Hovers

### See Also

- [DynamicForm.itemHoverAlign](DynamicForm.md#attr-dynamicformitemhoveralign)

**Flags**: IRW

---
## Attr: FormItem.textFormula

### Description
Formula to be used to calculate the text value of this FormItem. For a numeric field [FormItem.formula](#attr-formitemformula) is used instead.

Available fields for use in the formula are the current [rule context](Canvas.md#attr-canvasrulescope). The formula is re-evaluated every time the rule context changes.

See [FormItem.formula](#attr-formitemformula) for details on available fields for the formula and when the formula is calculated.

Note: A FormItem using a textFormula must have a [FormItem.name](#attr-formitemname) defined. [FormItem.shouldSaveValue](#attr-formitemshouldsavevalue) can be set to `false` to prevent the formula field from storing the calculated value into the form's values.

### Groups

- formulaFields

**Flags**: IR

---
## Attr: FormItem.decimalPad

### Description
Applies only to fields of type "float" and enforces a minimum number of digits shown after the decimal point.

For example, a field value of 343.1, 343.104 and 343.09872677 would all be shown as 343.10 if decimalPad is 2.

The original unpadded value is always shown when the value is edited.

### Groups

- appearance

**Flags**: IRW

---
## Attr: FormItem.cellHeight

### Description
If specified, this property will govern the height of the cell in which this form item is rendered. Will not apply when the containing DynamicForm sets `itemLayout:"absolute"`.

### Groups

- formItemStyling

**Flags**: IRW

---
## Attr: FormItem.showFocusedErrorState

### Description
If set to true, when an item has errors and is focused, an "ErrorFocused" suffix will appear on the stylename.

### Groups

- appearance

### See Also

- [FormItem.cellStyle](#attr-formitemcellstyle)

**Flags**: IRWA

---
## Attr: FormItem.hoverOpacity

### Description
Opacity for any hover shown for this item

### Groups

- Hovers

### See Also

- [DynamicForm.itemHoverOpacity](DynamicForm.md#attr-dynamicformitemhoveropacity)

**Flags**: IRW

---
## Attr: FormItem.vAlign

### Description
Vertical alignment of this item within its cell. This property governs the position of the item's text box within the cell (not the content within the text box). If [FormItem.shouldApplyHeightToTextBox](#method-formitemshouldapplyheighttotextbox) is true, for this to have a visible effect, the cell height must exceed the specified height of the item, either due to an explicit [FormItem.cellHeight](#attr-formitemcellheight) specification, or due to the row being expanded by another taller item.

Has no effect if [DynamicForm.itemLayout](DynamicForm.md#attr-dynamicformitemlayout) is set to `"absolute"` for the form.

### Groups

- title

**Flags**: IRW

---
## Attr: FormItem.wrapStaticValue

### Description
If this item is [read-only](#method-formitemgetcanedit) and is using [readOnlyDisplay](#attr-formitemreadonlydisplay) "static", should the item value wrap?

**Flags**: IRW

---
## Attr: FormItem.textBoxStyle

### Description
Base CSS class name for a form item's text box element.

See [formItemStyling](../kb_topics/formItemStyling.md#kb-topic-formitem-styling) for an overview of formItem styling, and the [CompoundFormItem_skinning](../reference.md#kb-topic-compoundformitem_skinning) discussion for special skinning considerations.

If the `textBoxStyle` is changed at runtime, [updateState()](#method-formitemupdatestate) must be called to update the visual state of this item.

### Groups

- formItemStyling

### See Also

- [FormItem.cellStyle](#attr-formitemcellstyle)

**Flags**: IRW

---
## Attr: FormItem.showFocusedIcons

### Description
If we're showing icons, should we change their image source to the appropriate _focused_ source when this item has focus? Can be overridden on a per icon basis by the formItemIcon `showFocused` property.

### Groups

- formIcons

**Flags**: IRWA

---
## Attr: FormItem.browserInputType

### Description
Form item input type - governs which keyboard should be displayed for mobile devices (supported on iPhone / iPad)

**Flags**: IRA

---
## Attr: FormItem.iconBaseStyle

### Description
Fallback base CSS class to apply to this item's [FormItem.icons](#attr-formitemicons) if they don't specify a [baseStyle](FormItemIcon.md#attr-formitemiconbasestyle) or provide a sprite-based [src string](FormItemIcon.md#attr-formitemiconsrc) that specifies a `cssClass`.

### Groups

- formItemStyling

**Flags**: IRW

---
## Attr: FormItem.emptyDisplayValue

### Description
Text to display when this form item has a null or undefined value.

If the formItem has a databound pickList, and its [FormItem.displayField](#attr-formitemdisplayfield) or [FormItem.valueField](#attr-formitemvaluefield) (if the former isn't set) has an undefined [emptyCellValue](ListGridField.md#attr-listgridfieldemptycellvalue) setting, that field's `emptyCellValue` will automatically be set to the `emptyDisplayValue`.

### Groups

- display_values

**Flags**: IRW

---
## Attr: FormItem.errorMessageWidth

### Description
When [DynamicForm.showInlineErrors](DynamicForm.md#attr-dynamicformshowinlineerrors) and [FormItem.showErrorText](#attr-formitemshowerrortext) are both true and [FormItem.errorOrientation](#attr-formitemerrororientation) is "left" or "right", errorMessageWidth is the amount to reduce the width of the editor to accommodate the error message and icon.

### Groups

- validation

**Flags**: IRW

---
## Attr: FormItem.iconHSpace

### Description
Horizontal space (in px) to leave between form item icons. The space appears either on the left or right of each icon. May be overridden at the icon level via [FormItemIcon.hspace](FormItemIcon.md#attr-formitemiconhspace). Must be non-negative.

### Groups

- formIcons

**Flags**: IR

---
## Attr: FormItem.titleVAlign

### Description
Vertical alignment of this item's title in its cell. Only applies when [FormItem.titleOrientation](#attr-formitemtitleorientation) is `"left"` or `"right"`.

### Groups

- title

**Flags**: IRW

---
## Attr: FormItem.requiredMessage

### Description
The required message for required field errors.

### Groups

- validation

**Flags**: IRW

---
## Attr: FormItem.showOldValueInHover

### Description
Causes the original value to be shown to the end user when the user hovers over the FormItem as such (when the [FormItem.itemHover](#method-formitemitemhover) event would fire).

When [FormItem.showOldValueInHover](#attr-formitemshowoldvalueinhover) and the form's [DynamicForm.showOldValueInHover](DynamicForm.md#attr-dynamicformshowoldvalueinhover) are both unset, defaults to the value of [FormItem.showPending](#attr-formitemshowpending).

The message shown is controlled by [FormItem.originalValueMessage](#attr-formitemoriginalvaluemessage), unless the item is [disabled](#attr-formitemdisabled) and [disabledHover](#attr-formitemdisabledhover) is set - in this case, the hover shows the `disabledHover` HTML.

If the item [suppresses hovers](#attr-formitemcanhover), nothing will be shown.

**Flags**: IRWA

---
## Attr: FormItem.showClippedValueOnHover

### Description
If true and the value is clipped, then a hover containing the full value of this item is enabled.

The [FormItem.valueHover](#method-formitemvaluehover) method is called before the hover is displayed, allowing the hover to be canceled if desired. The HTML shown in the hover can be customized by overriding [FormItem.valueHoverHTML](#method-formitemvaluehoverhtml).

**Interaction with valueHoverHTML vs itemHoverHTML:** This attribute controls which hover method handles textbox/value area hovers:

*   `true` (default): textbox hovers are handled via [FormItem.itemHoverHTML](#method-formitemitemhoverhtml), which shows the item's prompt or clipped value
*   `false`: no hover is shown for the textbox area
*   `null`: textbox hovers are handled via [FormItem.valueHoverHTML](#method-formitemvaluehoverhtml), allowing custom value-specific hover content

If the item [suppresses hovers](#attr-formitemcanhover), nothing will be shown.

### Groups

- Hovers

### See Also

- [FormItem.valueHoverHTML](#method-formitemvaluehoverhtml)
- [FormItem.itemHoverHTML](#method-formitemitemhoverhtml)

**Flags**: IRW

---
## Attr: FormItem.updatePickerIconOnOver

### Description
If [FormItem.showOver](#attr-formitemshowover) is true, setting this property to false will explicitly disable showing the "Over" state for the PickerIcon of this item (if present)

### Groups

- formItemStyling

### See Also

- [FormItem.showOver](#attr-formitemshowover)

**Flags**: IRWA

---
## Attr: FormItem.wrapTitle

### Description
If specified determines whether this items title should wrap. Overrides [wrapItemTitles](DynamicForm.md#attr-dynamicformwrapitemtitles) at the DynamicForm level.

### Groups

- title

**Flags**: IRW

---
## Attr: FormItem.valueDeselectedCSSText

### Description
Custom CSS text to be applied to values that have been deleted, when [showDeletions](#attr-formitemshowdeletions) is enabled.

**Flags**: IRA

---
## Attr: FormItem.name

### Description
Name for this form field. Must be unique within the form as well as a valid JavaScript identifier - see [FieldName](../reference.md#type-fieldname) for details and how to check for validity.

The FormItem's name determines the name of the property it edits within the form.

Note that an item must have a valid name or [dataPath](#attr-formitemdatapath) in order for its value to be validated and/or saved.

### Groups

- basics

**Flags**: IR

---
## Attr: FormItem.readOnlyControlStyle

### Description
Modified [control style](#attr-formitemcontrolstyle) to apply when this item is [read-only](#method-formitemgetcanedit) and is using [readOnlyDisplay](#attr-formitemreadonlydisplay) "static".

**Flags**: IRW

---
## Attr: FormItem.titleClassName

### Description
CSS class for the form item's title.

### Groups

- title

**Deprecated**

**Flags**: IR

---
## Attr: FormItem.align

### Description
Alignment of this item in its cell. Note that the alignment of text / content within this item is controlled separately via [FormItem.textAlign](#attr-formitemtextalign) (typically `textAlign` applies to items showing a "textBox", such as a [TextItem](TextItem.md#class-textitem) or [SelectItem](SelectItem.md#class-selectitem), as well as text-only form item types such as [StaticTextItem](StaticTextItem.md#class-statictextitem) and [HeaderItem](HeaderItem.md#class-headeritem)). If [applyAlignToText](#attr-formitemapplyaligntotext) is true, then the `textAlign` setting, if unset, will default to the `align` setting if set.

### Groups

- appearance

### See Also

- [FormItem.applyAlignToText](#attr-formitemapplyaligntotext)

**Flags**: IRW

---
## Attr: FormItem.errorOrientation

### Description
If [DynamicForm.showInlineErrors](DynamicForm.md#attr-dynamicformshowinlineerrors) is true, where should the error icon and text appear relative to the form item itself. Valid options are `"top"`, `"bottom"`, `"left"` or `"right"`.  
If unset the orientation will be derived from [DynamicForm.errorOrientation](DynamicForm.md#attr-dynamicformerrororientation).

### Groups

- validation
- appearance

**Flags**: IRW

---
## Attr: FormItem.formula

### Description
Formula to be used to calculate the numeric value of this FormItem. For a field of type "text" (or subtypes) [FormItem.textFormula](#attr-formitemtextformula) is used instead.

Available fields for use in the formula are the current [rule context](Canvas.md#attr-canvasrulescope). The formula is re-evaluated every time the rule context changes.

Values calculated by the formula will always replace the current value of a non-editable field. For an editable field, the current value will be replaced if the end user has not changed the value since the last time it was computed by the formula, or if the value of the field is invalid according to declared [validators](#attr-formitemvalidators).

Note: A FormItem using a formula must have a [FormItem.name](#attr-formitemname) defined. [FormItem.shouldSaveValue](#attr-formitemshouldsavevalue) can be set to `false` to prevent the formula field from storing the calculated value into the form's values.

### Groups

- formulaFields

**Flags**: IR

---
## Attr: FormItem.defaultIconSrc

### Description
Default icon image source. Specify as the partial URL to an image, relative to the imgDir of this component. To specify image source for a specific icon use the `icon.src` property.  
If this item is drawn in the disabled state, the url will be modified by adding "\_Disabled" to get a disabled state image for the icon. If `icon.showOver` is true, this url will be modified by adding "\_Over" to get an over state image for the icon.

[Spriting](../kb_topics/skinning.md#kb-topic-skinning--theming) can be used for this image, by setting this property to a [SCSpriteConfig](../reference.md#type-scspriteconfig) formatted string.

### Groups

- formIcons

**Flags**: IRWA

---
## Attr: FormItem.saveOnEnter

### Description
Set this to true to allow the parent form to save it's data when 'Enter' is pressed on this formItem and [saveOnEnter](DynamicForm.md#attr-dynamicformsaveonenter) is true on the parent form.

**Flags**: IRW

---
## Attr: FormItem.emptyValueIcon

### Description
This property allows the developer to specify an icon to display when this item has no value. It is configured in the same way as any other valueIcon (see [FormItem.valueIcons](#attr-formitemvalueicons))

### Groups

- valueIcons

**Flags**: IRW

---
## Attr: FormItem.visible

### Description
Whether this item is currently visible.

`visible` can only be set on creation. After creation, use [FormItem.show](#method-formitemshow) and [FormItem.hide](#method-formitemhide) to manipulate visibility.

### Groups

- appearance

**Flags**: IRW

---
## Attr: FormItem.staticHeight

### Description
Height of the FormItem when `canEdit` is false and `readOnlyDisplay` is "static". The normal [FormItem.height](#attr-formitemheight) is used if this property is not set.

### Groups

- formLayout

### See Also

- [FormItem.height](#attr-formitemheight)

**Flags**: IR

---
## Attr: FormItem.prompt

### Description
This text is shown as a tooltip prompt when the cursor hovers over this item.

When the item is [read-only](#method-formitemsetcanedit) a different hover can be shown with [FormItem.readOnlyHover](#attr-formitemreadonlyhover). Or, when the item is [disabled](#attr-formitemdisabled) or read-only with [readOnlyDisplay:disabled](#attr-formitemreadonlydisplay) a different hover can be shown with [FormItem.disabledHover](#attr-formitemdisabledhover).

Note that when the form is [disabled](Canvas.md#attr-canvasdisabled), or when this item [suppresses hovers](#attr-formitemcanhover), this prompt will not be shown.

### Groups

- basics

**Flags**: IRW

---
## Attr: FormItem.showErrorIcon

### Description
[showErrorIcons](DynamicForm.md#attr-dynamicformshowerroricons), [showErrorText](DynamicForm.md#attr-dynamicformshowerrortext), [errorOrientation](DynamicForm.md#attr-dynamicformerrororientation), and [showErrorStyle](DynamicForm.md#attr-dynamicformshowerrorstyle) control how validation errors are displayed when they are displayed inline in the form (next to the form item where there is a validation error). To instead display all errors at the top of the form, set [showInlineErrors](DynamicForm.md#attr-dynamicformshowinlineerrors):false.

`showErrorIcons`, `showErrorText`, `errorOrientation` and `showErrorStyle` are all boolean properties, and can be set on a DynamicForm to control the behavior form-wide, or set on individual FormItems.

The HTML displayed next to a form item with errors is generated by [FormItem.getErrorHTML](#method-formitemgeterrorhtml). The default implementation of that method respects `showErrorIcons` and `showErrorText` as follows:

`showErrorIcons`, or `showErrorIcon` at the FormItem level controls whether an error icon should appear next to fields which have validation errors. The icon's appearance is governed by [FormItem.errorIconSrc](#attr-formitemerroriconsrc), [FormItem.errorIconWidth](#attr-formitemerroriconwidth) and [FormItem.errorIconHeight](#attr-formitemerroriconheight)

`showErrorText` determines whether the text of the validation error should be displayed next to fields which have validation errors. The attribute [DynamicForm.showTitlesWithErrorMessages](DynamicForm.md#attr-dynamicformshowtitleswitherrormessages) may be set to prefix error messages with the form item's title + `":"` (may be desired if the item has [FormItem.showTitle](#attr-formitemshowtitle) set to false).  
If `showErrorText` is unset, the error text will be shown if [DynamicForm.linearMode](DynamicForm.md#attr-dynamicformlinearmode) is true (or [DynamicForm.linearOnMobile](DynamicForm.md#attr-dynamicformlinearonmobile) is true for mobile devices), otherwise it will not be shown.

In addition to this:

[DynamicForm.errorOrientation](DynamicForm.md#attr-dynamicformerrororientation) controls where the error HTML should appear relative to form items. Therefore the combination of [FormItem.showErrorText](#attr-formitemshowerrortext)`:false` and [FormItem.errorOrientation](#attr-formitemerrororientation)`:"left"` creates a compact validation error display consisting of just an icon, to the left of the item with the error message available via a hover (similar appearance to ListGrid validation error display).  
If `errorOrientation` is unset, the error orientation will default to "top" if [DynamicForm.linearMode](DynamicForm.md#attr-dynamicformlinearmode) is enabled (or [DynamicForm.linearOnMobile](DynamicForm.md#attr-dynamicformlinearonmobile) is true for mobile devices) and error text is not showing, "left" otherwise.

`showErrorStyle` determines whether fields with validation errors should have special styling applied to them. Error styling is achieved by applying suffixes to existing styling applied to various parts of the form item. See [FormItemBaseStyle](../reference_2.md#type-formitembasestyle) for more on this.

### Groups

- errorIcon
- validation
- appearance

**Flags**: IRW

---
## Attr: FormItem.optionFilterContext

### Description
If this item has a specified `optionDataSource`, and this property is not null, the context is passed to the dataSource as [RPCRequest](../reference.md#object-rpcrequest) properties when performing fetch operations on the dataSource to obtain a data-value to display-value mapping, and when fetching for grid-based pickers.

This attribute is a direct shortcut for setting fetch-request properties via `item.pickerProperties.dataProperties.requestProperties`.

**Flags**: IRA

---
## Attr: FormItem.showRTL

### Description
When this item is in RTL mode, should its style name include an "RTL" suffix?

### Groups

- RTL
- appearance

### See Also

- [FormItem.cellStyle](#attr-formitemcellstyle)

**Flags**: IRA

---
## Attr: FormItem.readOnlyTextBoxStyle

### Description
Base text box style to apply when this item is [read-only](#method-formitemgetcanedit) and is using [readOnlyDisplay](#attr-formitemreadonlydisplay) "static". If set, overrides the form-level [DynamicForm.readOnlyTextBoxStyle](DynamicForm.md#attr-dynamicformreadonlytextboxstyle) default.

### See Also

- [DynamicForm.readOnlyTextBoxStyle](DynamicForm.md#attr-dynamicformreadonlytextboxstyle)

**Flags**: IRW

---
## Attr: FormItem.hoverHeight

### Description
Option to specify a height for any hover shown for this item.

### Groups

- Hovers

### See Also

- [DynamicForm.itemHoverHeight](DynamicForm.md#attr-dynamicformitemhoverheight)

**Flags**: IRW

---
## Attr: FormItem.stopOnError

### Description
Indicates that if validation fails, the user should not be allowed to exit the field - focus will be forced back into the field until the error is corrected.

This property defaults to [DynamicForm.stopOnError](DynamicForm.md#attr-dynamicformstoponerror) if unset.

Enabling this property also implies [FormItem.validateOnExit](#attr-formitemvalidateonexit) is automatically enabled. If there are server-based validators on this item, setting this property also implies that [FormItem.synchronousValidation](#attr-formitemsynchronousvalidation) is forced on.

**Flags**: IR

---
## Attr: FormItem.requiredRightTitlePrefix

### Description
The string prepended to this item's title if it is required and the [TitleOrientation](../reference_2.md#type-titleorientation) property is set to "right". The [DynamicForm.requiredRightTitlePrefix](DynamicForm.md#attr-dynamicformrequiredrighttitleprefix) is used by default.

### Groups

- title

### See Also

- [FormItem.requiredRightTitleSuffix](#attr-formitemrequiredrighttitlesuffix)

**Flags**: IRW

---
## Attr: FormItem.alwaysFetchMissingValues

### Description
If this form item has a specified [FormItem.optionDataSource](#attr-formitemoptiondatasource) and [FormItem.fetchMissingValues](#attr-formitemfetchmissingvalues) is true, when the item value changes, a fetch will be performed against the optionDataSource to retrieve the related record if [FormItem.displayField](#attr-formitemdisplayfield) is specified and the new item value is not present in any valueMap explicitly specified on the item.

Setting this property to true means that a fetch will occur against the optionDataSource to retrieve the related record even if [FormItem.displayField](#attr-formitemdisplayfield) is unset, or the item has a valueMap which explicitly contains this field's value.

An example of a use case where this might be set would be if [FormItem.formatValue](#method-formitemformatvalue) or [FormItem.formatEditorValue](#method-formitemformateditorvalue) were written to display properties from the [selected record](#method-formitemgetselectedrecord).

Note - for efficiency we cache the associated record once a fetch has been performed, meaning if the value changes, then reverts to a previously seen value, we do not kick off an additional fetch even if this property is true. If necessary this cache may be explicitly invalidated via a call to [FormItem.invalidateDisplayValueCache](#method-formiteminvalidatedisplayvaluecache)

### Groups

- display_values

**Flags**: IRWA

---
## Attr: FormItem.errorIconHeight

### Description
Height of the error icon, if we're showing icons when validation errors occur.

### Groups

- errorIcon

### See Also

- [FormItem.showErrorIcon](#attr-formitemshowerroricon)

**Flags**: IRW

---
## Attr: FormItem.validateOnExit

### Description
If true, form items will be validated when each item's "editorExit" handler is fired as well as when the entire form is submitted or validated.

Note that this property can also be set at the form level. If true at either level the validator will be fired on editorExit.

### See Also

- [DynamicForm.validateOnExit](DynamicForm.md#attr-dynamicformvalidateonexit)

**Flags**: IRW

---
## Attr: FormItem.synchronousValidation

### Description
If enabled, whenever validation is triggered and a request to the server is required, user interactivity will be blocked until the request returns. Can be set for the entire form or individual FormItems.

If false, the form will try to avoid blocking user interaction until it is strictly required. That is until the user attempts to use a FormItem whose state could be affected by a server request that has not yet returned.

**Flags**: IR

---
## Attr: FormItem.showPickerIcon

### Description
Should we show a special 'picker' [icon](../reference.md#object-formitemicon) for this form item? Picker icons are customizable via [pickerIconProperties](#attr-formitempickericonproperties). By default they will be rendered inside the form item's ["control box"](#attr-formitemcontrolstyle) area. By default clicking the pickerIcon will call [FormItem.showPicker](#method-formitemshowpicker).

### Groups

- pickerIcon

**Flags**: IRW

---
## Attr: FormItem.showErrorIconInline

### Description
When set to true, this attribute renders the [error-icon](#attr-formitemerroriconsrc) [inline](FormItemIcon.md#attr-formitemiconinline) in the FormItem, next to other icons, instead of in a separate error-element outside of the item's main editor. When rendering the error-icon inline, the [error-text](#attr-formitemshowerrortext) is not displayed but is available in the icon's hover.

[Icon-properties](../reference.md#object-formitemicon) can be applied to the error-icon via [errorIconProperties](#attr-formitemerroriconproperties).

**Flags**: IRA

---
## Attr: FormItem.wrapHintText

### Description
If this item is showing a [FormItem.hint](#attr-formitemhint), should the hint text be allowed to wrap? Setting this property to `false` will render the hint on a single line without wrapping, expanding the width required to render the item if necessary.

If unset this property will be picked up from the [DynamicForm.wrapHintText](DynamicForm.md#attr-dynamicformwraphinttext) setting.

This setting does not apply to hints that are [shown in field](TextItem.md#attr-textitemshowhintinfield).

### See Also

- [FormItem.minHintWidth](#attr-formitemminhintwidth)

**Flags**: IR

---
## Attr: FormItem.valueIconLeftPadding

### Description
If we're showing a value icon, this attribute governs the amount of space between the icon and the start edge of the form item cell.

**NOTE:** In RTL mode, the valueIconLeftPadding is applied to the _right_ of the value icon.

### Groups

- valueIcons

### See Also

- [FormItem.valueIcons](#attr-formitemvalueicons)

**Flags**: IRW

---
## Attr: FormItem.iconPrompt

### Description
Default prompt (and tooltip-text) for icons.

If [canHover](#attr-formitemcanhover) is set to false, this prompt will not be shown.

### Groups

- formIcons

**Flags**: IRWA

---
## Attr: FormItem.ariaState

### Description
ARIA state mappings for this formItem. Usually this does not need to be manually set - see [accessibility](../kb_topics/accessibility.md#kb-topic-accessibility--section-508-compliance).

This attribute should be set to a mapping of aria state-names to values - for example to have the "aria-multiline" property be present with a value "true", you'd specify:

```
  { multiline : true }
 
```

### Groups

- accessibility

**Flags**: IRWA

---
## Attr: FormItem.implicitSaveOnBlur

### Description
If set to true, this item's value will be saved immediately when its "editorExit" handler is fired. This attribute works separately from [implicitSave](#attr-formitemimplicitsave), which causes saves during editing, after a [short delay](DynamicForm.md#attr-dynamicformimplicitsavedelay), and when the entire form is submitted.

**Flags**: IRW

---
## Attr: FormItem.pickerIconSrc

### Description
If [showPickerIcon](#attr-formitemshowpickericon) is true for this item, this property governs the [src](FormItemIcon.md#attr-formitemiconsrc) of the picker icon image to be displayed.

[Spriting](../kb_topics/skinning.md#kb-topic-skinning--theming) can be used for this image, by setting this property to a [SCSpriteConfig](../reference.md#type-scspriteconfig) formatted string.

### Groups

- pickerIcon

**Flags**: IRWA

---
## Attr: FormItem.errorIconSrc

### Description
URL of the image to show as an error icon, if we're showing icons when validation errors occur.

### Groups

- errorIcon

### See Also

- [FormItem.showErrorIcon](#attr-formitemshowerroricon)

**Flags**: IRW

---
## Attr: FormItem.controlStyle

### Description
Base CSS class name for a form item's "control box". This is an HTML element which contains the text box and picker icon for the item.

See [FormItem.alwaysShowControlBox](#attr-formitemalwaysshowcontrolbox) for details on when the control box is written out.

See [formItemStyling](../kb_topics/formItemStyling.md#kb-topic-formitem-styling) for an overview of formItem styling, and the [CompoundFormItem_skinning](../reference.md#kb-topic-compoundformitem_skinning) discussion for special skinning considerations.

### Groups

- formItemStyling
- pickerIcon

### See Also

- [FormItem.cellStyle](#attr-formitemcellstyle)

**Flags**: IRW

---
## Attr: FormItem.ID

### Description
Global identifier for referring to the formItem in JavaScript. The ID property is optional if you do not need to refer to the widget from JavaScript, or can refer to it indirectly (for example, via `form.getItem("_itemName_")`).

An internal, unique ID will automatically be created upon instantiation for any formItem where one is not provided.

### Groups

- basics

**Flags**: IRW

---
## Attr: FormItem.allowExpressions

### Description
For a form that produces filter criteria (see [form.getValuesAsCriteria()](DynamicForm.md#method-dynamicformgetvaluesascriteria)), allows the user to type in simple expressions to cause filtering with that operator. For example, entering ">5" means values greater than 5, and ">0 and <5" means values between 0 and 5.

The following table lists character sequences that can be entered as a prefix to a value, and the corresponding [operator](../reference.md#type-operatorid) that will be used.

| Prefix | Operator |
|---|---|
| < | lessThan |
| > | greaterThan |
| <= | lessThanOrEqual |
| >= | greaterThanOrEqual |
| someValue...someValue | betweenInclusive |
| ! | notEqual |
| ^ | startsWith |
| \| | endsWith |
| !^ | notStartsWith plus logical not |
| !@ | notEndsWith plus logical not |
| ~ | contains |
| !~ | notContains |
| $ | isBlank |
| !$ | notBlank |
| # | isNull |
| !# | isNotNull |
| == | exact match (for fields where 'contains' is the default) |

Two further special notations are allowed:

*   /_regex_/ means the value is taken as a regular expression and applied via the "regexp" operator
*   \=._fieldName_ means the value should match the value of another field. Either the user-visible title of the field (field.title) or the field's name (field.name) may be used.

In all cases, if an operator is disallowed for the field (via [field.validOperators](DataSourceField.md#attr-datasourcefieldvalidoperators) at either the dataSource or field level), the operator character is ignored (treated as part of a literal value).

By default, the case-insensitive version of the operator is used (eg, startsWith will actually use "iStartsWith"). To avoid this, explicitly set item.operator (the default operator) to any case sensitive operator (eg "equals" or "contains") and case sensitive operators will be used for user-entered expressions.

Compound expressions (including "and" and "or") are allowed only for numeric or date/time types.

Note that if the user does not type a prefix or use other special notation as described above, the operator specified via [FormItem.operator](#attr-formitemoperator) is used, or if `formItem.operator` is unspecified, a default operator chosen as described under [FormItem.operator](#attr-formitemoperator).

Also note that whatever you enter will be used literally, including any whitespace characters. For example if you input '== China ' then ' China ' will be the value.

The `allowExpression` behavior can be enabled for every field in a form via [DynamicForm.allowExpressions](DynamicForm.md#attr-dynamicformallowexpressions).

Finally, note that, like [FormItem.operator](#attr-formitemoperator), enabling `allowExpressions:true` causes [form.getValuesAsCriteria()](DynamicForm.md#method-dynamicformgetvaluesascriteria)) to return [AdvancedCriteria](../reference.md#object-advancedcriteria).

### Groups

- advancedFilter

**Flags**: IRW

---
## Attr: FormItem.readOnlyDisplay

### Description
If this item is [read-only](#method-formitemgetcanedit), how should this item be displayed to the user? If set, overrides the form-level [DynamicForm.readOnlyDisplay](DynamicForm.md#attr-dynamicformreadonlydisplay) default.

### Groups

- appearance
- readOnly

### See Also

- [DynamicForm.readOnlyDisplay](DynamicForm.md#attr-dynamicformreadonlydisplay)

**Flags**: IRW

---
## Attr: FormItem.height

### Description
Height of the FormItem. Can be either a number indicating a fixed height in pixels, a percentage indicating a percentage of the overall form's height, or "\*" indicating take whatever remaining space is available. See the [formLayout](../kb_topics/formLayout.md#kb-topic-form-layout) overview for details.

For form items having a [picker icon](#attr-formitemshowpickericon) (e.g. [SelectItem](SelectItem.md#class-selectitem), [ComboBoxItem](ComboBoxItem.md#class-comboboxitem)) and [SpinnerItem](SpinnerItem.md#class-spinneritem)s, if there is no explicit [FormItem.pickerIconHeight](#attr-formitempickericonheight), the pickerIcon will be sized to match the available space based on the specified item height.  
Note that if spriting is being used, and the image to be displayed in these icons is specified using css properties such as `background-image`, `background-size`, changing this value may result in an unexpected appearance as the image will not scale.  
Scaleable spriting can be achieved using the [SCSpriteConfig](../reference.md#type-scspriteconfig) format. See the section on spriting in the [skinning overview](../kb_topics/skinning.md#kb-topic-skinning--theming) for further information.  
Alternatively, the [pickerIconStyle](#attr-formitempickericonstyle) could be changed to a custom CSS style name, and in the case of [SpinnerItem](SpinnerItem.md#class-spinneritem)s, the [baseStyle](FormItemIcon.md#attr-formitemiconbasestyle) and [src](FormItemIcon.md#attr-formitemiconsrc) of the [SpinnerItem.increaseIcon](SpinnerItem.md#attr-spinneritemincreaseicon) and [SpinnerItem.decreaseIcon](SpinnerItem.md#attr-spinneritemdecreaseicon) AutoChildren could be customized.

Note that when FormItem is rendered as read-only with `readOnlyDisplay` as "static" the property [FormItem.staticHeight](#attr-formitemstaticheight) is used instead.

### Groups

- formLayout

### See Also

- [formLayout](../kb_topics/formLayout.md#kb-topic-form-layout)
- [FormItem.width](#attr-formitemwidth)
- [DynamicForm.itemLayout](DynamicForm.md#attr-dynamicformitemlayout)

**Flags**: IRW

---
## Attr: FormItem.hoverDelay

### Description
If specified, this is the number of milliseconds to wait between the user rolling over this form item, and triggering any hover action for it.  
If not specified `this.form.itemHoverDelay` will be used instead.

### Groups

- Hovers

**Flags**: IRWA

---
## Attr: FormItem.hoverFocusKey

### Description
This attribute gives users a way to pin this item's hover in place so they can interact with it (scroll it, click embedded links, etc).

Overrides the [same attribute](Canvas.md#attr-canvashoverfocuskey) on the parent form.

### Groups

- hovers

### See Also

- [FormItem.hoverPersist](#attr-formitemhoverpersist)

**Flags**: IRW

---
## Attr: FormItem.showDisabledIconsOnFocus

### Description
If [FormItem.showIconsOnFocus](#attr-formitemshowiconsonfocus) is true, should icons marked as disabled be shown on focus?

Default setting is `false` - it is not commonly desirable to present a user with a disabled icon on focus.

Can be overridden at the icon level by [FormItemIcon.showDisabledOnFocus](FormItemIcon.md#attr-formitemiconshowdisabledonfocus)

### Groups

- formIcons

**Flags**: IRWA

---
## Attr: FormItem.pickerIconProperties

### Description
If [showPickerIcon](#attr-formitemshowpickericon) is true for this item, this block of properties will be applied to the pickerIcon. Allows for advanced customization of this icon.

### Groups

- pickerIcon

**Flags**: IRWA

---
## Attr: FormItem.applyAlignToText

### Description
If the [textAlign](#attr-formitemtextalign) is unset, should the [align](#attr-formitemalign) setting, if set, be used for this item's `textAlign`?

`applyAlignToText` defaults to false for most form item types. It defaults to true for [StaticTextItem](StaticTextItem.md#class-statictextitem) and [HeaderItem](HeaderItem.md#class-headeritem), which are text-based form item types that do not have a natural distinction between the item and its cell.

### Groups

- appearance

**Flags**: IRA

---
## Attr: FormItem.showDeletions

### Description
For items that support [multiple values](SelectItem.md#attr-selectitemmultiple), this causes distinct CSS styling to be applied to values that the user has unselected.

Only allowed when [showPending](#attr-formitemshowpending) is `true`. Defaults to the form-level [DynamicForm.showDeletions](DynamicForm.md#attr-dynamicformshowdeletions) setting if set; otherwise, to the value of `showPending`.

Only supported for [MultiComboBoxItem](MultiComboBoxItem.md#class-multicomboboxitem) and for [SelectItem](SelectItem.md#class-selectitem) when [multiple:true](SelectItem.md#attr-selectitemmultiple) is set. The specific default behaviors are:

*   For `MultiComboBoxItem`, buttons corresponding to deleted values (also called "deselected buttons") will be disabled and have their [Button.baseStyle](Button.md#attr-buttonbasestyle) set to [MultiComboBoxItem.deselectedButtonStyle](MultiComboBoxItem.md#attr-multicomboboxitemdeselectedbuttonstyle).
*   For a multiple `SelectItem`, [FormItem.valueDeselectedCSSText](#attr-formitemvaluedeselectedcsstext) is applied to any deleted value in the text box. In addition, "Deselected" is appended to the cells' [ListGrid.baseStyle](ListGrid_1.md#attr-listgridbasestyle) for cells in the pickList menu corresponding to deleted values.

**NOTE:** When a value is shown as deleted, this is not reflected to screen readers, and screen readers are instructed to ignore the deleted value. Therefore, it is not advisable to design a UI where it is necessary for the user to know whether a value is shown as deleted in order to work with the form.

### See Also

- [DynamicForm.showDeletions](DynamicForm.md#attr-dynamicformshowdeletions)

**Flags**: IRA

---
## Attr: FormItem.validOperators

### Description
Array of valid filtering operators (eg "greaterThan") that are legal for this FormItem.

Applies only to form/formItem when [FormItem.allowExpressions](#attr-formitemallowexpressions) is true, allowing the user to input expressions.

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: FormItem.valueIconRightPadding

### Description
If we're showing a value icon, this attribute governs the amount of space between the icon and the value text.

**NOTE:** In RTL mode, the valueIconRightPadding is applied to the _left_ of the value icon.

### Groups

- valueIcons

### See Also

- [FormItem.valueIcons](#attr-formitemvalueicons)

**Flags**: IRW

---
## Attr: FormItem.visibleWhen

### Description
Criteria to be evaluated to determine whether this FormItem should be visible.

Criteria are evaluated against the ${isc.DocUtils.linkForRef('method:DynamicForm.getValues','form\\'s current values')} as well as the current [rule context](Canvas.md#attr-canvasrulescope). Criteria are re-evaluated every time form values or the rule context changes, whether by end user action or by programmatic calls.

If both [FormItem.showIf](#method-formitemshowif) and `visibleWhen` are specified, `visibleWhen` is ignored.

A basic criteria uses textMatchStyle:"exact". When specified in [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml) this property allows [shorthand formats](../kb_topics/xmlCriteriaShorthand.md#kb-topic-xmlcriteriashorthand) for defining criteria.

Note: A FormItem using visibleWhen must have a [FormItem.name](#attr-formitemname) defined. [FormItem.shouldSaveValue](#attr-formitemshouldsavevalue) can be set to `false` to prevent the field from storing its value into the form's values.

### Groups

- ruleCriteria
- appearance

**Flags**: IR

---
## Attr: FormItem.autoCompleteKeywords

### Description
Set of autocompletion keywords to be used with the native "autocomplete" attribute, in accordance with the [HTML5 Autofill specification](https://html.spec.whatwg.org/multipage/form-control-infrastructure.html#autofill).

When autoCompleteKeywords are provided, the [FormItem.autoComplete](#attr-formitemautocomplete) setting is ignored.

### Groups

- autoComplete

**Flags**: IR

---
## Attr: FormItem.implicitSave

### Description
When true, indicates that changes to this item will cause an automatic save on a [delay](DynamicForm.md#attr-dynamicformimplicitsavedelay), as well as when the entire form is submitted. If implicitSaveOnBlur is set to true on either this [formItem](#attr-formitemimplicitsaveonblur) or it's [form](DynamicForm.md#attr-dynamicformimplicitsaveonblur), changes will also be automatically saved immediately on editorExit.

**Flags**: IRW

---
## Attr: FormItem.showErrorText

### Description
[showErrorIcons](DynamicForm.md#attr-dynamicformshowerroricons), [showErrorText](DynamicForm.md#attr-dynamicformshowerrortext), [errorOrientation](DynamicForm.md#attr-dynamicformerrororientation), and [showErrorStyle](DynamicForm.md#attr-dynamicformshowerrorstyle) control how validation errors are displayed when they are displayed inline in the form (next to the form item where there is a validation error). To instead display all errors at the top of the form, set [showInlineErrors](DynamicForm.md#attr-dynamicformshowinlineerrors):false.

`showErrorIcons`, `showErrorText`, `errorOrientation` and `showErrorStyle` are all boolean properties, and can be set on a DynamicForm to control the behavior form-wide, or set on individual FormItems.

The HTML displayed next to a form item with errors is generated by [FormItem.getErrorHTML](#method-formitemgeterrorhtml). The default implementation of that method respects `showErrorIcons` and `showErrorText` as follows:

`showErrorIcons`, or `showErrorIcon` at the FormItem level controls whether an error icon should appear next to fields which have validation errors. The icon's appearance is governed by [FormItem.errorIconSrc](#attr-formitemerroriconsrc), [FormItem.errorIconWidth](#attr-formitemerroriconwidth) and [FormItem.errorIconHeight](#attr-formitemerroriconheight)

`showErrorText` determines whether the text of the validation error should be displayed next to fields which have validation errors. The attribute [DynamicForm.showTitlesWithErrorMessages](DynamicForm.md#attr-dynamicformshowtitleswitherrormessages) may be set to prefix error messages with the form item's title + `":"` (may be desired if the item has [FormItem.showTitle](#attr-formitemshowtitle) set to false).  
If `showErrorText` is unset, the error text will be shown if [DynamicForm.linearMode](DynamicForm.md#attr-dynamicformlinearmode) is true (or [DynamicForm.linearOnMobile](DynamicForm.md#attr-dynamicformlinearonmobile) is true for mobile devices), otherwise it will not be shown.

In addition to this:

[DynamicForm.errorOrientation](DynamicForm.md#attr-dynamicformerrororientation) controls where the error HTML should appear relative to form items. Therefore the combination of [FormItem.showErrorText](#attr-formitemshowerrortext)`:false` and [FormItem.errorOrientation](#attr-formitemerrororientation)`:"left"` creates a compact validation error display consisting of just an icon, to the left of the item with the error message available via a hover (similar appearance to ListGrid validation error display).  
If `errorOrientation` is unset, the error orientation will default to "top" if [DynamicForm.linearMode](DynamicForm.md#attr-dynamicformlinearmode) is enabled (or [DynamicForm.linearOnMobile](DynamicForm.md#attr-dynamicformlinearonmobile) is true for mobile devices) and error text is not showing, "left" otherwise.

`showErrorStyle` determines whether fields with validation errors should have special styling applied to them. Error styling is achieved by applying suffixes to existing styling applied to various parts of the form item. See [FormItemBaseStyle](../reference_2.md#type-formitembasestyle) for more on this.

### Groups

- validation
- appearance

**Flags**: IRW

---
## Attr: FormItem.showImageAsURL

### Description
For fields of [type:"image"](../reference.md#type-formitemtype), if the field is non editable, and being displayed with [readOnlyDisplay:"static"](#attr-formitemreadonlydisplay), should the value (URL) be displayed as text, or should an image be rendered?

If unset, [DynamicForm.showImageAsURL](DynamicForm.md#attr-dynamicformshowimageasurl) will be consulted instead.

**Flags**: IRW

---
## Attr: FormItem.globalTabIndex

### Description
TabIndex for the form item within the page. Takes precedence over any local tab index specified as [item.tabIndex](#attr-formitemtabindex).

Use of this API is **extremely** advanced and essentially implies taking over management of tab index assignment for all components on the page.

### Groups

- focus

**Flags**: IRWA

---
## Attr: FormItem.readOnlyCanSelectText

### Description
For items showing a text value with [FormItem.canEdit](#attr-formitemcanedit) set to false, should the user be able to select the text in the item?

Default behavior allows selection if [FormItem.readOnlyDisplay](#attr-formitemreadonlydisplay) is `"static"` or `"readOnly"` \[but not `"disabled"`\]. Developers may add or remove ReadOnlyDisplayAppearance values to change this behavior.

Note that this does not apply to [disabled items](#attr-formitemdisabled), where text selection is never enabled

**Flags**: IRW

---
## Attr: FormItem.updateTextBoxOnOver

### Description
If [FormItem.showOver](#attr-formitemshowover) is true, setting this property to false will explicitly disable showing the "Over" state for the TextBox element of this item.

### Groups

- formItemStyling

### See Also

- [FormItem.showOver](#attr-formitemshowover)

**Flags**: IRWA

---
## Attr: FormItem.showIconsOnFocus

### Description
Show the [FormItem.icons](#attr-formitemicons) when the item gets focus, and hide them when it loses focus. Can be overridden at the icon level by [FormItemIcon.showOnFocus](FormItemIcon.md#attr-formitemiconshowonfocus).

Note that icons marked as disabled will not be shown on focus even if this flag is true by default. This may be overridden by [FormItem.showDisabledIconsOnFocus](#attr-formitemshowdisablediconsonfocus).

### Groups

- formIcons

**Flags**: IRWA

---
## Attr: FormItem.linearStartRow

### Description
Specifies [FormItem.startRow](#attr-formitemstartrow) for an item in [linearMode](DynamicForm.md#attr-dynamicformlinearmode), overriding the default of `false` in that mode.

### Groups

- formLayout

**Flags**: IRW

---
## Attr: FormItem.validators

### Description
Validators for this form item.

**Note:** these validators will only be run on the client; to do real client-server validation, validators must be specified via [DataSourceField.validators](DataSourceField.md#attr-datasourcefieldvalidators).

**Flags**: IR

---
## Attr: FormItem.alwaysShowControlBox

### Description
A formItem showing a [pickerIcon](#attr-formitemshowpickericon) will always write out a "control box" around the text box and picker icon. This is an HTML element styled using the specified [FormItem.controlStyle](#attr-formitemcontrolstyle).

This attribute controls whether the control box should be written out even if the picker icon is not being shown. If unset, default behavior will write out a control table if [FormItem.showPickerIcon](#attr-formitemshowpickericon) is true and the icon is not suppressed via [FormItemIcon.showIf](FormItemIcon.md#method-formitemiconshowif). This means the control table can be written out with no visible picker if [FormItem.showPickerIconOnFocus](#attr-formitemshowpickericononfocus) is true and the item does not have focus.

This attribute is useful for developers who wish to rely on styling specified via the [FormItem.controlStyle](#attr-formitemcontrolstyle) even while the picker icon is not visible.

See the [form item styling overview](../kb_topics/formItemStyling.md#kb-topic-formitem-styling) for details of the control table and other styling options.

**Flags**: IRA

---
## Attr: FormItem.rowSpan

### Description
Number of rows that this item spans

### Groups

- formLayout

**Flags**: IRW

---
## Attr: FormItem.criteriaField

### Description
When using [FormItem.operator](#attr-formitemoperator), the name of the DataSource field for the [Criterion](../reference_2.md#object-criterion) this FormItem generates. If not specified, defaults to [FormItem.name](#attr-formitemname).

Generally, because `criteriaField` defaults to `item.name`, you don't need to specify it. However, if more than one FormItem specifies criteria for the same DataSource field, they will need unique values for [FormItem.name](#attr-formitemname) but should set [FormItem.criteriaField](#attr-formitemcriteriafield) to the name of DataSource field they both target.

For example, if two DateItems are used to provide a min and max date for a single field called "joinDate", set [FormItem.criteriaField](#attr-formitemcriteriafield) to "joinDate" on both fields but give the fields distinct names (eg "minDate" and "maxDate") and use those names for any programmatic access, such as [DynamicForm.setValue](DynamicForm.md#method-dynamicformsetvalue).

**Flags**: IR

---
## Attr: FormItem.accessKey

### Description
If specified this governs the HTML accessKey for the item.

This should be set to a character - when a user hits the html accessKey modifier for the browser, plus this character, focus will be given to the item. The accessKey modifier can vary by browser and platform.

The following list of default behavior is for reference only, developers should also consult browser documentation for additional information.

*   **Internet Explorer (all platforms)**: `Alt` + _accessKey_
*   **Mozilla Firefox (Windows, Unix)**: `Alt+Shift` + _accessKey_
*   **Mozilla Firefox (Mac)**: `Ctrl+Opt` + _accessKey_
*   **Chrome and Safari (Windows, Unix)**: `Alt` + _accessKey_
*   **Chrome and Safari (Mac)**: `Ctrl+Opt` + _accessKey_

### Groups

- focus

**Flags**: IRW

---
## Attr: FormItem.requiredTitlePrefix

### Description
The string prepended to this item's title if it is required. The [DynamicForm.requiredTitlePrefix](DynamicForm.md#attr-dynamicformrequiredtitleprefix) is used by default.

### Groups

- title

### See Also

- [FormItem.requiredTitleSuffix](#attr-formitemrequiredtitlesuffix)

**Flags**: IRW

---
## Attr: FormItem.cellStyle

### Description
CSS style applied to the form item as a whole, including the text element, any icons, and any hint text for the item. Applied to the cell containing the form item.

See [formItemStyling](../kb_topics/formItemStyling.md#kb-topic-formitem-styling) for an overview of formItem styling, and the [CompoundFormItem_skinning](../reference.md#kb-topic-compoundformitem_skinning) discussion for special skinning considerations.

### Groups

- formItemStyling

**Flags**: IRW

---
## Attr: FormItem.applyHeightToTextBox

### Description
If [FormItem.height](#attr-formitemheight) is specified, should it be applied to the item's text box element?

If unset, behavior is determined as described in [FormItem.shouldApplyHeightToTextBox](#method-formitemshouldapplyheighttotextbox)

**Flags**: IRA

---
## Attr: FormItem.useLocalDisplayFieldValue

### Description
If [FormItem.displayField](#attr-formitemdisplayfield) is specified for a field, should the display value for the field be picked up from the [record currently being edited](DynamicForm.md#method-dynamicformgetvalues)?

This behavior is typically valuable for dataBound components where the displayField is specified at the DataSourceField level. See [DataSourceField.displayField](DataSourceField.md#attr-datasourcefielddisplayfield) for more on this.

Note that for DataSources backed by the [SmartClient server](../kb_topics/serverDataIntegration.md#kb-topic-server-datasource-integration), fields with a specified [DataSourceField.foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) and [DataSourceField.displayField](DataSourceField.md#attr-datasourcefielddisplayfield) will automatically have this property set to true if not explicitly set to false in the dataSource configuration.

Otherwise, if not explicitly set, local display value will be used unless:

*   This item has an explicitly specified optionDataSource, rather than deriving its optionDataSource from a specified [DataSourceField.foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) specification
*   The [FormItem.name](#attr-formitemname) differs from the [valueField](#method-formitemgetvaluefieldname) for the item

**Flags**: IR

---
## Attr: FormItem.rightTitlePrefix

### Description
The string prepended to this item's title when its titleOrientation is set to "right". The [DynamicForm.rightTitlePrefix](DynamicForm.md#attr-dynamicformrighttitleprefix) is used by default.

### Groups

- title

### See Also

- [FormItem.rightTitleSuffix](#attr-formitemrighttitlesuffix)

**Flags**: IRW

---
## Attr: FormItem.suppressValueIcon

### Description
If [FormItem.valueIcons](#attr-formitemvalueicons) is set, this property may be set to prevent the value icons from showing up next to the form items value

### Groups

- valueIcons

**Flags**: IRWA

---
## Attr: FormItem.containerWidget

### Description
A Read-Only pointer to the SmartClient canvas that holds this form item. In most cases this will be the [DynamicForm](#attr-formitemform) containing the item but in some cases editable components handle writing out form items directly. An example of this is [Grid Editing](../kb_topics/editing.md#kb-topic-grid-editing) - when a listGrid shows per-field editors, the `containerWidget` for each item will be the listGrid body.

Note that even if the `containerWidget` is not a DynamicForm, a DynamicForm will still exist for the item (available as [FormItem.form](#attr-formitemform)), allowing access to standard APIs such as [DynamicForm.getValues](DynamicForm.md#method-dynamicformgetvalues)

**Flags**: RA

---
## Attr: FormItem.showHint

### Description
If a hint is defined for this form item, should it be shown?

### Groups

- appearance

**Flags**: IRWA

---
## Attr: FormItem.canSelectText

### Description
For items showing a text value, should the user be able to select the text in this item?

For [canEdit:false](#attr-formitemcanedit) items, see [FormItem.readOnlyCanSelectText](#attr-formitemreadonlycanselecttext)

**Flags**: IRW

---
## Attr: FormItem.storeDisplayValues

### Description
If specified, this overrides the [DynamicForm.storeDisplayValues](DynamicForm.md#attr-dynamicformstoredisplayvalues) property for this field.

**Flags**: IRA

---
## Attr: FormItem.errorIconWidth

### Description
Height of the error icon, if we're showing icons when validation errors occur.

### Groups

- errorIcon

### See Also

- [FormItem.showErrorIcon](#attr-formitemshowerroricon)

**Flags**: IRW

---
## Attr: FormItem.valueIconHeight

### Description
If [FormItem.valueIcons](#attr-formitemvalueicons) is specified, use this property to specify a height for the value icon written out.

### Groups

- valueIcons

### See Also

- [FormItem.valueIconWidth](#attr-formitemvalueiconwidth)
- [FormItem.valueIconSize](#attr-formitemvalueiconsize)

**Flags**: IRW

---
## Attr: FormItem.tabIndex

### Description
TabIndex for the form item within the form, which controls the order in which controls are visited when the user hits the tab or shift-tab keys to navigate between items.

tabIndex is automatically assigned as the order that items appear in the [DynamicForm.items](DynamicForm.md#attr-dynamicformitems) list.

To specify the tabindex of an item within the page as a whole (not just this form), use [FormItem.globalTabIndex](#attr-formitemglobaltabindex) instead.

### Groups

- focus

**Flags**: IRW

---
## Attr: FormItem.selectOnClick

### Description
Allows the [selectOnClick](DynamicForm.md#attr-dynamicformselectonclick) behavior to be configured on a per-FormItem basis. Normally all items in a form default to the value of [DynamicForm.selectOnClick](DynamicForm.md#attr-dynamicformselectonclick).

### Groups

- focus

**Flags**: IRW

---
## Attr: FormItem.valueIconSize

### Description
If [FormItem.valueIcons](#attr-formitemvalueicons) is specified, this property may be used to specify both the width and height of the icon written out. Note that [FormItem.valueIconWidth](#attr-formitemvalueiconwidth) and [FormItem.valueIconHeight](#attr-formitemvalueiconheight) take precedence over this value, if specified.

### Groups

- valueIcons

### See Also

- [FormItem.valueIconWidth](#attr-formitemvalueiconwidth)
- [FormItem.valueIconHeight](#attr-formitemvalueiconheight)

**Flags**: IRW

---
## Attr: FormItem.rightTitleSuffix

### Description
The string appended to this item's title when its titleOrientation is set to "right". The [DynamicForm.rightTitleSuffix](DynamicForm.md#attr-dynamicformrighttitlesuffix) is used by default.

### Groups

- title

### See Also

- [FormItem.rightTitlePrefix](#attr-formitemrighttitleprefix)

**Flags**: IRW

---
## Attr: FormItem.nullOriginalValueText

### Description
Text shown as the value in the [FormItem.originalValueMessage](#attr-formitemoriginalvaluemessage) when [showOldValueInHover](#attr-formitemshowoldvalueinhover) is enabled, and when the value has been modified but was originally unset.

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: FormItem.hoverVAlign

### Description
Vertical text alignment for text displayed in this item's hover canvas, if shown.

### Groups

- Hovers

### See Also

- [DynamicForm.itemHoverVAlign](DynamicForm.md#attr-dynamicformitemhovervalign)

**Flags**: IRW

---
## Attr: FormItem.hidden

### Description
Should this form item be hidden? Setting this property to `true` on an item configuration will have the same effect as having a [FormItem.showIf](#method-formitemshowif) implementation which returns `false`.

Note this differs slightly from [DataSourceField.hidden](DataSourceField.md#attr-datasourcefieldhidden). That property will cause the field in question to be omitted entirely from databound components by default. A dataSourceField with `hidden` set to `true` can still be displayed in a DynamicForm either by being explicitly included in the specified [items array](DynamicForm.md#attr-dynamicformitems), or by having [DataBoundComponent.showHiddenFields](DataBoundComponent.md#attr-databoundcomponentshowhiddenfields) set to true. In this case, this property will not be inherited onto the FormItem instance, meaning the item will be visible in the form even though the `hidden` property was set to true on the dataSourceField configuration object.

**Flags**: IR

---
## Attr: FormItem.showFocusedPickerIcon

### Description
If [FormItem.showPickerIcon](#attr-formitemshowpickericon) is true for this item, should the picker icon show a focused image when the form item has focus?

### Groups

- pickerIcon

**Flags**: IRW

---
## Attr: FormItem.requiredTitleSuffix

### Description
The string appended to this item's title if it is required. The [DynamicForm.requiredTitleSuffix](DynamicForm.md#attr-dynamicformrequiredtitlesuffix) is used by default.

### Groups

- title

### See Also

- [FormItem.requiredTitlePrefix](#attr-formitemrequiredtitleprefix)

**Flags**: IRW

---
## Attr: FormItem.hoverStyle

### Description
Explicit CSS Style for any hover shown for this item.

### Groups

- Hovers

### See Also

- [DynamicForm.itemHoverStyle](DynamicForm.md#attr-dynamicformitemhoverstyle)

**Flags**: IRW

---
## Attr: FormItem.showIcons

### Description
Set to false to suppress writing out any [FormItem.icons](#attr-formitemicons) for this item.

### Groups

- formIcons

**Flags**: IRWA

---
## Attr: FormItem.titleAlign

### Description
Alignment of this item's title in its cell.

If null, dynamically set according to text direction.

### Groups

- title

**Flags**: IRW

---
## Attr: FormItem.loadingDisplayValue

### Description
Value shown in field when [fetchMissingValues](#attr-formitemfetchmissingvalues) is active and a fetch is pending. The field is read-only while a fetch is pending.

Set to `null` to show actual value until display value is loaded.

### Groups

- display_values
- i18nMessages

**Flags**: IRW

---
## Attr: FormItem.useDisabledHintStyleForReadOnly

### Description
By default, [read-only](#attr-formitemcanedit) fields use the same style name as editable fields for in-field hints, unless they are [disabled](#method-formitemisdisabled) or configured to use a disabled [ReadOnlyDisplayAppearance](../reference_2.md#type-readonlydisplayappearance). This is described under [TextItem.showHintInField](TextItem.md#attr-textitemshowhintinfield)

If `useDisabledHintStyleForReadOnly` is set, the "HintDisabled" style will be used for read-only fields regardless of their `ReadOnlyDisplayAppearance`. This allows you to use a different in-field hint style for read-only fields without having to use a general disabled appearance for those fields

### Groups

- appearance

**Flags**: IRW

---
## Attr: FormItem.linearWidth

### Description
Specifies a width for an item in [linearMode](DynamicForm.md#attr-dynamicformlinearmode), overriding the default width of "\*" in that mode.

### Groups

- formLayout

### See Also

- [FormItem.width](#attr-formitemwidth)

**Flags**: IRW

---
## Attr: FormItem.minHintWidth

### Description
If this item is showing a [FormItem.hint](#attr-formitemhint), this setting specifies how much horizontal space is made available for rendering the hint text by default. Typically this reflects how much space the hint text takes up before it wraps.

Note that the presence of a hint may cause a form item to expand horizontally past its specified [FormItem.width](#attr-formitemwidth). This property value acts as a minimum - if the hint text can not wrap within this width (either due to [FormItem.wrapHintText](#attr-formitemwraphinttext) being set to `false`, or due to it containing long, un-wrappable content), it will further expand to take up the space it needs.

If unset this property will be picked up from the [DynamicForm.minHintWidth](DynamicForm.md#attr-dynamicformminhintwidth) setting.

This setting does not apply to hints that are [shown in field](TextItem.md#attr-textitemshowhintinfield).

### See Also

- [FormItem.wrapHintText](#attr-formitemwraphinttext)

**Flags**: IR

---
## Attr: FormItem.useAdvancedCriteria

### Description
Should this form item always produce an [AdvancedCriteria](../reference.md#object-advancedcriteria) sub criterion object? When set to true, causes [hasAdvancedCriteria](#method-formitemhasadvancedcriteria) to return true. Can also be set at the [ListGrid](ListGrid_1.md#attr-listgriduseadvancedcriteria) level.

### Groups

- criteriaEditing

**Flags**: IRW

---
## Attr: FormItem.showDisabled

### Description
When this item is disabled, should it be re-styled to indicate its disabled state?

See [formItemStyling](../kb_topics/formItemStyling.md#kb-topic-formitem-styling) for more details on formItem styling.

### Groups

- formItemStyling

### See Also

- [FormItem.cellStyle](#attr-formitemcellstyle)

**Flags**: IRWA

---
## Attr: FormItem.requiredRightTitleSuffix

### Description
The string appended to this item's title if it is required and the [TitleOrientation](../reference_2.md#type-titleorientation) property is set to "right". The +link(DynamicForm.requiredRightTitleSuffix) is used by default.

### Groups

- title

### See Also

- [FormItem.requiredRightTitlePrefix](#attr-formitemrequiredrighttitleprefix)

**Flags**: IRW

---
## Attr: FormItem.titlePrefix

### Description
The string prepended to this item's title. The [DynamicForm.titlePrefix](DynamicForm.md#attr-dynamicformtitleprefix) is used by default.

### Groups

- title

### See Also

- [FormItem.titleSuffix](#attr-formitemtitlesuffix)

**Flags**: IRW

---
## Attr: FormItem.required

### Description
Whether a non-empty value is required for this field to pass validation.

If the user does not fill in the required field, the error message to be shown will be taken from these properties in the following order: [FormItem.requiredMessage](#attr-formitemrequiredmessage), [DynamicForm.requiredMessage](DynamicForm.md#attr-dynamicformrequiredmessage), [DataSource.requiredMessage](DataSource.md#attr-datasourcerequiredmessage), [Validator.requiredField](Validator.md#classattr-validatorrequiredfield).

**Note:** if specified on a FormItem, `required` is only enforced on the client. `required` should generally be specified on a [DataSourceField](../reference_2.md#object-datasourcefield).

### Groups

- validation

**Flags**: IR

---
## Attr: FormItem.pickerIconStyle

### Description
Base CSS class name for a form item's picker icon cell. If unset, inherits from this item's [controlStyle](#attr-formitemcontrolstyle).

### Groups

- pickerIcon
- formItemStyling

### See Also

- [FormItem.cellStyle](#attr-formitemcellstyle)

**Flags**: IRW

---
## Attr: FormItem.canHover

### Description
Indicates whether hovers can be shown for this item. When set to false, suppresses all hovers, including those for the [item in general](#method-formitemitemhoverhtml), or for its [value](#method-formitemvaluehoverhtml) or [title](#method-formitemtitlehoverhtml).

For finer control over suppressing hovers, see [itemHover](#method-formitemitemhover), [titleHover](#method-formitemtitlehover) and [valueHover](#method-formitemvaluehover).

### Groups

- Hovers

### See Also

- [FormItem.prompt](#attr-formitemprompt)
- [FormItem.itemHover](#method-formitemitemhover)
- [FormItem.titleHover](#method-formitemtitlehover)
- [FormItem.valueHover](#method-formitemvaluehover)

**Flags**: IRW

---
## Attr: FormItem.title

### Description
User visible title for this form item.

### Groups

- basics

**Flags**: IRW

---
## Attr: FormItem.disableIconsOnReadOnly

### Description
If [FormItem.canEdit](#attr-formitemcanedit) is set to false, should [icons](#attr-formitemicons) be disabled by default?

This may also be specified at the icon level. See [FormItemIcon.disableOnReadOnly](FormItemIcon.md#attr-formitemicondisableonreadonly).

### Groups

- formIcons

**Flags**: IRW

---
## Attr: FormItem.printTitleStyle

### Description
Base CSS stylename for a form item's title when generating print HTML for the item. If unset [FormItem.titleStyle](#attr-formitemtitlestyle) will be used instead.

### Groups

- printing

**Flags**: IRW

---
## Attr: FormItem.destroyed

### Description
The destroyed attribute will be set to true if this item has been destroyed() Note that FormItem lifecycle is managed by the DynamicForm itself. FormItem instances are created and destroyed automatically when new fields are added to the form.

**Flags**: RA

---
## Attr: FormItem.multiple

### Description
If true, multiple values may be selected.

Only certain FormItems that support both singular and multiple values actually use this setting, such as [SelectItem](SelectItem.md#class-selectitem). Other FormItems such as [MultiComboBoxItem](MultiComboBoxItem.md#class-multicomboboxitem) are always effectively multiple:true, even if multiple:true is not set.

### Groups

- appearance

**Flags**: IRW

---
## Attr: FormItem.cellClassName

### Description
CSS class for a form item's cell in the form layout

### Groups

- appearance

**Deprecated**

**Flags**: IR

---
## Attr: FormItem.showFocused

### Description
When this item receives focus, should it be re-styled to indicate it has focus?

See [formItemStyling](../kb_topics/formItemStyling.md#kb-topic-formitem-styling) for more details on formItem styling.

### Groups

- formItemStyling

### See Also

- [FormItem.cellStyle](#attr-formitemcellstyle)

**Flags**: IRWA

---
## Attr: FormItem.dateFormatter

### Description
Display format to use for date type values within this formItem.

Note that Fields of type `"date"`, `"datetime"` or `"time"` will be edited using a [DateItem](DateItem.md#class-dateitem) or [TimeItem](TimeItem.md#class-timeitem) by default, but this can be overridden - for `canEdit:false` fields, a [StaticTextItem](StaticTextItem.md#class-statictextitem) is used by default, and the developer can always specify a custom [FormItem.editorType](#attr-formitemeditortype) as well as [data type](#attr-formitemtype).

The [FormItem.timeFormatter](#attr-formitemtimeformatter) may also be used to format underlying Date values as times (ommitting the date part entirely). If both `dateFormatter` and `timeFormatter` are specified on an item, for fields specified as [type "time"](#attr-formitemtype) the `timeFormatter` will be used, otherwise the `dateFormatter`

If `item.dateFormatter` and `item.timeFormatter` is unspecified, date display format may be defined at the component level via [DynamicForm.dateFormatter](DynamicForm.md#attr-dynamicformdateformatter), or for fields of type `"datetime"` [DynamicForm.datetimeFormatter](DynamicForm.md#attr-dynamicformdatetimeformatter). Otherwise the default is to use the system-wide default short date format, configured via [DateUtil.setShortDisplayFormat](DateUtil.md#classmethod-dateutilsetshortdisplayformat). Specify any valid [DateDisplayFormat](../reference.md#type-datedisplayformat) to change the format used by this item.

Note that if this is a freeform editable field, such a [TextItem](TextItem.md#class-textitem), with type specified as `"date"` or `"datetime"` the system will automatically attempt to parse user entered values back to a Date value, assuming the entered string matches the date format for the field. Developers may further customize this via an explicit [FormItem.inputFormat](#attr-formiteminputformat) or via entirely custom [FormItem.formatEditorValue](#method-formitemformateditorvalue) and [FormItem.parseEditorValue](#method-formitemparseeditorvalue) methods.

### Groups

- appearance

### See Also

- [FormItem.timeFormatter](#attr-formitemtimeformatter)
- [FormItem.format](#attr-formitemformat)

**Flags**: IRWA

---
## Attr: FormItem.width

### Description
Width of the FormItem. Can be either a number indicating a fixed width in pixels, or "\*" indicating the FormItem fills the space allocated to it's column (or columns, for a [column spanning](#attr-formitemcolspan) item). You may also use "100%" as a synonym for "\*", but other percentages are not supported.

Note that for "absolute" item layout rather than the default "table" layout, the rules for specifying the width are slightly different. All percent sizes are allowed, but not "\*". See [DynamicForm.itemLayout](DynamicForm.md#attr-dynamicformitemlayout) for further details.

See the [formLayout](../kb_topics/formLayout.md#kb-topic-form-layout) overview for details.

### Groups

- formLayout

### See Also

- [FormItem.linearWidth](#attr-formitemlinearwidth)
- [formLayout](../kb_topics/formLayout.md#kb-topic-form-layout)
- [FormItem.height](#attr-formitemheight)
- [DynamicForm.itemLayout](DynamicForm.md#attr-dynamicformitemlayout)

**Flags**: IRW

---
## Attr: FormItem.imageURLSuffix

### Description
Suffix to apply to the end of any [FormItem.valueIcons](#attr-formitemvalueicons) when determining the URL for the image. A common usage would be to specify a suffix of `".gif"` in which case the `valueIcons` property would map values to the names of images without the `".gif"` extension.

### Groups

- valueIcons

**Flags**: IRWA

---
## Attr: FormItem.extraTextBoxCSS

### Description
Additional CSS-text that overrides the item's [FormItem.textBoxStyle](#attr-formitemtextboxstyle), applying arbitrary custom styling to the textBox.

This is an advanced attribute - while it can be used to modify many properties, such as colors, font-style and border-radius, it should not be used to modify any property that may affect element-size, such as height, padding/margin or overflow.

**Flags**: IRA

---
## Attr: FormItem.icons

### Description
An array of descriptor objects for icons to display in a line after this form item. These icons are clickable images, often used to display some kind of helper for populating a form item.

### Groups

- formIcons

### See Also

- [FormItemIcon](../reference.md#object-formitemicon)

**Flags**: IRW

---
## Attr: FormItem.readOnlyHover

### Description
This text is shown as a tooltip prompt when the cursor hovers over this item and the item is [read-only](#method-formitemsetcanedit).

Note that when the form is [disabled](Canvas.md#attr-canvasdisabled), or when this item [suppresses hovers](#attr-formitemcanhover), nothing will be shown.

**Flags**: IRW

---
## Attr: FormItem.titleColSpan

### Description
Number of columns that this item's title spans.

This setting only applies for items that are showing a title and whose [TitleOrientation](../reference_2.md#type-titleorientation) is either "left" or "right".

### Groups

- formLayout

**Flags**: IRW

---
## Attr: FormItem.showDisabledPickerIconOnFocus

### Description
If [FormItem.showPickerIconOnFocus](#attr-formitemshowpickericononfocus) is true, should the picker icon be shown on focus if it is disabled (as in a read-only item, for example?)

Default setting is `false` - it is not commonly desirable to present a user with a disabled icon on focus.

Can be overridden at the icon level by [FormItemIcon.showDisabledOnFocus](FormItemIcon.md#attr-formitemiconshowdisabledonfocus)

### Groups

- formIcons

**Flags**: IRWA

---
## Attr: FormItem.hintStyle

### Description
CSS class for the "hint" string. For items that support [TextItem.showHintInField](TextItem.md#attr-textitemshowhintinfield), this only applies when showHintInField is false.

### Groups

- formItemStyling

### See Also

- [FormItem.hint](#attr-formitemhint)

**Flags**: IRW

---
## Attr: FormItem.showErrorStyle

### Description
[showErrorIcons](DynamicForm.md#attr-dynamicformshowerroricons), [showErrorText](DynamicForm.md#attr-dynamicformshowerrortext), [errorOrientation](DynamicForm.md#attr-dynamicformerrororientation), and [showErrorStyle](DynamicForm.md#attr-dynamicformshowerrorstyle) control how validation errors are displayed when they are displayed inline in the form (next to the form item where there is a validation error). To instead display all errors at the top of the form, set [showInlineErrors](DynamicForm.md#attr-dynamicformshowinlineerrors):false.

`showErrorIcons`, `showErrorText`, `errorOrientation` and `showErrorStyle` are all boolean properties, and can be set on a DynamicForm to control the behavior form-wide, or set on individual FormItems.

The HTML displayed next to a form item with errors is generated by [FormItem.getErrorHTML](#method-formitemgeterrorhtml). The default implementation of that method respects `showErrorIcons` and `showErrorText` as follows:

`showErrorIcons`, or `showErrorIcon` at the FormItem level controls whether an error icon should appear next to fields which have validation errors. The icon's appearance is governed by [FormItem.errorIconSrc](#attr-formitemerroriconsrc), [FormItem.errorIconWidth](#attr-formitemerroriconwidth) and [FormItem.errorIconHeight](#attr-formitemerroriconheight)

`showErrorText` determines whether the text of the validation error should be displayed next to fields which have validation errors. The attribute [DynamicForm.showTitlesWithErrorMessages](DynamicForm.md#attr-dynamicformshowtitleswitherrormessages) may be set to prefix error messages with the form item's title + `":"` (may be desired if the item has [FormItem.showTitle](#attr-formitemshowtitle) set to false).  
If `showErrorText` is unset, the error text will be shown if [DynamicForm.linearMode](DynamicForm.md#attr-dynamicformlinearmode) is true (or [DynamicForm.linearOnMobile](DynamicForm.md#attr-dynamicformlinearonmobile) is true for mobile devices), otherwise it will not be shown.

In addition to this:

[DynamicForm.errorOrientation](DynamicForm.md#attr-dynamicformerrororientation) controls where the error HTML should appear relative to form items. Therefore the combination of [FormItem.showErrorText](#attr-formitemshowerrortext)`:false` and [FormItem.errorOrientation](#attr-formitemerrororientation)`:"left"` creates a compact validation error display consisting of just an icon, to the left of the item with the error message available via a hover (similar appearance to ListGrid validation error display).  
If `errorOrientation` is unset, the error orientation will default to "top" if [DynamicForm.linearMode](DynamicForm.md#attr-dynamicformlinearmode) is enabled (or [DynamicForm.linearOnMobile](DynamicForm.md#attr-dynamicformlinearonmobile) is true for mobile devices) and error text is not showing, "left" otherwise.

`showErrorStyle` determines whether fields with validation errors should have special styling applied to them. Error styling is achieved by applying suffixes to existing styling applied to various parts of the form item. See [FormItemBaseStyle](../reference_2.md#type-formitembasestyle) for more on this.

### Groups

- validation
- appearance

### See Also

- [FormItem.cellStyle](#attr-formitemcellstyle)

**Flags**: IRW

---
## Attr: FormItem.pickerIconName

### Description
If [showPickerIcon](#attr-formitemshowpickericon) is true, this attribute specifies the [FormItemIcon.name](FormItemIcon.md#attr-formitemiconname) applied to the picker icon

### Groups

- pickerIcon

**Flags**: IRA

---
## Attr: FormItem.shouldSaveValue

### Description
Should this item's value be saved in the form's values and hence returned from [form.getValues()](DynamicForm.md#method-dynamicformgetvalues)?

`shouldSaveValue:false` is used to mark formItems which do not correspond to the underlying data model and should not save a value into the form's [values](DynamicForm.md#attr-dynamicformvalues). Example includes visual separators, password re-type fields, or checkboxes used to show/hide other form items.

A `shouldSaveValue:false` item should be given a value either via [FormItem.defaultValue](#attr-formitemdefaultvalue) or by calling [form.setValue(item, value)](DynamicForm.md#method-dynamicformsetvalue) or [formItem.setValue(value)](#method-formitemsetvalue). Providing a value via [form.values](DynamicForm.md#attr-dynamicformvalues) or [form.setValues()](DynamicForm.md#method-dynamicformsetvalues) will automatically switch the item to `shouldSaveValue:true`.

Note that

*   if an item is shouldSaveValue true, but has no name, a warning is logged, and shouldSaveValue will be set to false.

### Groups

- formValues

**Flags**: IR

---
## Attr: FormItem.pickerConstructor

### Description
Class name of the picker to be created.

**Flags**: IRW

---
## Attr: FormItem.format

### Description
[FormatString](../reference.md#type-formatstring) for numeric or date formatting. See [DataSourceField.format](DataSourceField.md#attr-datasourcefieldformat).

### Groups

- appearance

**Flags**: IR

---
## Attr: FormItem.showTitle

### Description
Should we show a title cell for this formItem?

Note: the default value of this attribute is overridden by some subclasses.

### Groups

- title

**Flags**: IRW

---
## Attr: FormItem.updateControlOnOver

### Description
If [FormItem.showOver](#attr-formitemshowover) is true, setting this property to false will explicitly disable showing the "Over" state for the control table element of this item (if present).

### Groups

- formItemStyling

### See Also

- [FormItem.showOver](#attr-formitemshowover)

**Flags**: IRWA

---
## Attr: FormItem.errorCellClassName

### Description
CSS class for a form item's cell when a validation error is showing.

### Groups

- appearance

**Deprecated**

**Flags**: IR

---
## Attr: FormItem.showClippedTitleOnHover

### Description
If true and the title is clipped, then a hover containing the full title of this item is enabled.

The [FormItem.titleHover](#method-formitemtitlehover) method is called before the hover is displayed, allowing the hover to be canceled if desired. The HTML shown in the hover can be customized by overriding [FormItem.titleHoverHTML](#method-formitemtitlehoverhtml).

If the item [suppresses hovers](#attr-formitemcanhover), nothing will be shown.

### Groups

- Hovers

**Flags**: IRW

---
## Attr: FormItem.showPending

### Description
When set to `true`, this property adds the optional "Pending" suffix to the CSS styles applied to the widget if the current value of the item differs from the value that would be restored by invoking [DynamicForm.resetValues](DynamicForm.md#method-dynamicformresetvalues). See [FormItemBaseStyle](../reference_2.md#type-formitembasestyle) for details.

[shouldSaveValue](#attr-formitemshouldsavevalue) must be `true` for this setting to have an effect.

Styling of the value is updated only after the [FormItem.change](#method-formitemchange) event is processed, so depending on the value of [changeOnKeypress](#attr-formitemchangeonkeypress), styling may be updated immediately on keystroke or only when the user leaves the field.

Default styling is provided for the Enterprise, EnterpriseBlue, and Graphite skins only. `showPending` should not be enabled for an item when using a skin without default styling unless the default [FormItem.pendingStatusChanged](#method-formitempendingstatuschanged) behavior is canceled and a custom pending visual state is implemented by the item.

On the other hand, when set to `true` and if [FormItem.canHover](#attr-formitemcanhover) is also true, a hover will appear, displaying the old value and controlled by [FormItem.showOldValueInHover](#attr-formitemshowoldvalueinhover), [FormItem.originalValueMessage](#attr-formitemoriginalvaluemessage) and [FormItem.nullOriginalValueText](#attr-formitemnulloriginalvaluetext). Additionally, if the new value is [clipped](#attr-formitemshowclippedvalueonhover), it will be shown in the hover as well.

**NOTE:** Whether an item is shown as pending is not reflected to screen readers. Therefore, it is not advisable to design a UI where it is necessary for the user to know whether an item is shown as pending in order to work with the form.

### See Also

- [FormItem.pendingStatusChanged](#method-formitempendingstatuschanged)

**Flags**: IRA

---
## Attr: FormItem.startRow

### Description
Whether this item should always start a new row in the form layout.

### Groups

- formLayout

### See Also

- [FormItem.linearStartRow](#attr-formitemlinearstartrow)

**Flags**: IRW

---
## Attr: FormItem.extraControlTableCSS

### Description
Additional CSS-text that overrides the item's [FormItem.controlStyle](#attr-formitemcontrolstyle), applying arbitrary custom styling to the outer control-table that contains both textBox and icons.

This is an advanced attribute - while it can be used to modify many properties, such as colors, font-style and border-radius, it should not be used to modify any property that may affect element-size, such as height, padding/margin or overflow.

**Flags**: IRA

---
## Attr: FormItem.rejectInvalidValueOnChange

### Description
If validateOnChange is true, and validation fails for this item on change, with no suggested value, should we revert to the previous value, or continue to display the bad value entered by the user. May be set at the item or form level.

**Flags**: IRWA

---
## Attr: FormItem.iconVAlign

### Description
How should icons be aligned vertically for this form item.

### Groups

- formIcons

**Flags**: IRWA

---
## Attr: FormItem.editorType

### Description
Name of the FormItem to use for editing, eg "TextItem" or "SelectItem".

The type of FormItem to use for editing is normally derived automatically from [field.type](#attr-formitemtype), which is the data type of the field, by the rules explained [here](../reference.md#type-formitemtype).

### Groups

- appearance

### See Also

- [FormItemType](../reference.md#type-formitemtype)
- [FieldType](../reference_2.md#type-fieldtype)

**Flags**: IR

---
## Attr: FormItem.optionCriteria

### Description
If this item has a specified `optionDataSource`, this property may be used to specify criteria to pass to the datasource when performing the fetch operation on the dataSource to obtain a data-value to display-value mapping.

The criteria generated for this fetch will consist of the specified optionCriteria, combined with criteria required to identify the current item value.  
For example, if a developer's use case was a DataSource of user records, with [FormItem.valueField](#attr-formitemvaluefield) set to _"userID"_" and [FormItem.displayField](#attr-formitemdisplayfield) set to _"userName"_, the generated criteria to retrieve the display value for the item would look for an exact match between the current item value and the userID field in the dataSource. The _optionCriteria_ would allow additional restrictions on this fetch (searching for records matching some other _"region"_ field, say).  
The sub-criterion containing the current valueField value will always look for an exact match (rather than any kind of substring match), so if [FormItem.optionTextMatchStyle](#attr-formitemoptiontextmatchstyle) is set to something other than "exact", developers may expect to see AdvancedCriteria passed to the server

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope). Criteria are re-evaluated when the [rule context](Canvas.md#method-canvasgetrulecontext) changes.

### Groups

- databinding
- searchCriteria

**Flags**: IR

---
## Attr: FormItem.filterLocally

### Description
If this form item is mapping data values to a display value by fetching records from a dataSource (see [FormItem.optionDataSource](#attr-formitemoptiondatasource), [FormItem.displayField](#attr-formitemdisplayfield) and [FormItem.fetchMissingValues](#attr-formitemfetchmissingvalues)), setting this property to true ensures that when the form item value is set, entire data-set from the dataSource is loaded at once and used as a valueMap, rather than just loading the display value for the current value. This avoids the need to perform fetches each time setValue() is called with a new value.

See also [PickList.filterLocally](PickList.md#attr-picklistfilterlocally) for behavior on form items such as SelectItems that show pick-lists.

### Groups

- display_values

**Flags**: IRA

---
## Attr: FormItem.valueField

### Description
If this form item maps data values to display values by retrieving the [FormItem.displayField](#attr-formitemdisplayfield) values from an [optionDataSource](#attr-formitemoptiondatasource), this property denotes the the field to use as the underlying data value in records from the optionDataSource.  
If not explicitly supplied, the valueField name will be derived as described in [FormItem.getValueFieldName](#method-formitemgetvaluefieldname).

### Groups

- databinding

**Flags**: IR

---
## Attr: FormItem.titleOrientation

### Description
On which side of this item should the title be placed. [TitleOrientation](../reference_2.md#type-titleorientation) lists valid options.

Note that titles on the left or right take up a cell in tabular [form layouts](../kb_topics/formLayout.md#kb-topic-form-layout), but titles on top do not.

### Groups

- title

### See Also

- [DynamicForm.titleOrientation](DynamicForm.md#attr-dynamicformtitleorientation)

**Flags**: IRW

---
## Attr: FormItem.iconWidth

### Description
Default width for form item icons. May be overridden at the icon level by [FormItemIcon.width](FormItemIcon.md#attr-formitemiconwidth).

### Groups

- formIcons

**Flags**: IRA

---
## Attr: FormItem.pickerProperties

### Description
Default properties for the picker.

**Flags**: IRW

---
## Attr: FormItem.operator

### Description
[OperatorId](../reference.md#type-operatorid) to be used when [DynamicForm.getValuesAsCriteria](DynamicForm.md#method-dynamicformgetvaluesascriteria) is called.

`item.operator` can be used to create a form that offers search functions such as numeric range filtering, without the more advanced user interface of the [FilterBuilder](FilterBuilder.md#class-filterbuilder). For example, two SpinnerItems could be created with `formItem.operator` set to "greaterThan" and "lessThan" respectively to enable filtering by a numeric range.

When `item.operator` is set for any FormItem in a form, `form.getValuesAsCriteria()` will return an [AdvancedCriteria](../reference.md#object-advancedcriteria) object instead of a normal [Criteria](../reference_2.md#type-criteria) object. Each FormItem will produce one [Criterion](../reference_2.md#object-criterion) affecting the DataSource field specified by [FormItem.criteriaField](#attr-formitemcriteriafield). The criteria produced by the FormItems will be grouped under the logical operator provided by [DynamicForm.operator](DynamicForm.md#attr-dynamicformoperator).

If `operator` is set for some fields but not others, the default operator is "equals" for fields with a valueMap or an optionDataSource, and for fields of type "enum" (or of a type that inherits from "enum"). The default operator for all other fields is controlled by [DynamicForm.defaultSearchOperator](DynamicForm.md#attr-dynamicformdefaultsearchoperator).

**Note:** `formItem.operator` is only supported for a form that has a [dataSource](DataBoundComponent.md#attr-databoundcomponentdatasource). In a form with no DataSource, setting `formItem.operator` will have no effect.

### Groups

- criteriaEditing

**Flags**: IR

---
## Attr: FormItem.valueMap

### Description
In a form, valueMaps are used for FormItem types that allow the user to pick from a limited set of values, such as a SelectItem. The valueMap can be either an Array of legal values or an Object where each property maps a stored value to a user-displayable value.

To set the initial selection for a form item with a valueMap, use [FormItem.defaultValue](#attr-formitemdefaultvalue).

See also [DataSourceField.valueMap](DataSourceField.md#attr-datasourcefieldvaluemap).

### Groups

- valueMap

**Flags**: IRW

---
## Attr: FormItem.readOnlyWhen

### Description
Criteria to be evaluated to determine whether this FormItem should be made [read-only](#method-formitemsetcanedit). Appearance when read-only is determined by [FormItem.readOnlyDisplay](#attr-formitemreadonlydisplay).

Criteria are evaluated against the ${isc.DocUtils.linkForRef('method:DynamicForm.getValues','form\\'s current values')} as well as the current [rule context](Canvas.md#attr-canvasrulescope). Criteria are re-evaluated every time form values or the rule context changes, whether by end user action or by programmatic calls.

A basic criteria uses textMatchStyle:"exact". When specified in [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml) this property allows [shorthand formats](../kb_topics/xmlCriteriaShorthand.md#kb-topic-xmlcriteriashorthand) for defining criteria.

Note: A FormItem using readOnlyWhen must have a [FormItem.name](#attr-formitemname) defined. [FormItem.shouldSaveValue](#attr-formitemshouldsavevalue) can be set to `false` to prevent the field from storing its value into the form's values.

### Groups

- ruleCriteria
- readOnly

**Flags**: IR

---
## Attr: FormItem.textAlign

### Description
Alignment of the text / content within this form item. Note that [FormItem.align](#attr-formitemalign) may be used to control alignment of the entire form item within its cell. `textAlign` does not apply to all form item types; typically it applies only to items showing a "textBox", such as a [TextItem](TextItem.md#class-textitem) or [SelectItem](SelectItem.md#class-selectitem), as well as text-only form item types such as [StaticTextItem](StaticTextItem.md#class-statictextitem) and [HeaderItem](HeaderItem.md#class-headeritem).

If [applyAlignToText](#attr-formitemapplyaligntotext) is true, then `textAlign` will default to the `align` setting if set. Otherwise, if this item has [icons](#attr-formitemicons), then `textAlign` will default to "left" ("right" in [RTL mode](Page.md#classmethod-pageisrtl)).

### Groups

- appearance

### See Also

- [FormItem.applyAlignToText](#attr-formitemapplyaligntotext)

**Flags**: IRW

---
## Attr: FormItem.defaultValue

### Description
Value used when no value is provided for this item. Note that whenever this item's value is cleared programmatically (for example via `item.clearValue()` or `item.setValue(null)`), it will be reverted to the `defaultValue`.

Developers should use the [DynamicForm.values](DynamicForm.md#attr-dynamicformvalues) object if their intention is to provide an initial value for a field in a form rather than a value to use in place of `null`.

Developers looking to provide a 'hint' or placeholder value for an empty item may wish to use [FormItem.hint](#attr-formitemhint) (possibly in conjunction with [TextItem.showHintInField](TextItem.md#attr-textitemshowhintinfield)), or [FormItem.prompt](#attr-formitemprompt).

Note: Some items provide a user interface allowing the user to explicitly clear them - for example a standard TextItem. If such an item has a defaultValue specified, and the user explicitly clears that value, the value of the item will be (correctly) reported as null, and will remain null over form item redraw()s. However any programmatic call to set the value to null (including, but not limited to `item.clearValue()`, `item.setValue(null)`, `dynamicForm.setValues(...)` with a null value for this field, etc) will reset the item value to its default.

### Groups

- basics

### See Also

- [FormItem.defaultDynamicValue](#method-formitemdefaultdynamicvalue)

**Flags**: IRW

---
## Attr: FormItem.titleStyle

### Description
Base CSS class name for a regular form-item's title. Note that this is a [FormItemBaseStyle](../reference_2.md#type-formitembasestyle) so will pick up stateful suffixes on focus, disabled state change etc. by default.

When the [title](#attr-formitemtitle) is shown [above](#attr-formitemtitleorientation) the item, the title element is given the [verticalTitleStyle](#attr-formitemverticaltitlestyle) if it's set, as it is in some skins - otherwise, it will fall back to `titleStyle`.

Note the appearance of the title is also affected by [DynamicForm.titlePrefix](DynamicForm.md#attr-dynamicformtitleprefix)/[titleSuffix](DynamicForm.md#attr-dynamicformtitlesuffix) and [DynamicForm.requiredTitlePrefix](DynamicForm.md#attr-dynamicformrequiredtitleprefix)/[requiredTitleSuffix](DynamicForm.md#attr-dynamicformrequiredtitlesuffix).

### Groups

- formItemStyling

### See Also

- [FormItem.cellStyle](#attr-formitemcellstyle)

**Flags**: IRW

---
## Attr: FormItem.fetchMissingValues

### Description
If this form item has a specified [FormItem.optionDataSource](#attr-formitemoptiondatasource), should the item ever perform a fetch against this dataSource to retrieve the related record.

The fetch occurs if the item value is non null on initial draw of the form or whenever setValue() is called. Once the fetch completes, the returned record is available via the [FormItem.getSelectedRecord](#method-formitemgetselectedrecord) api.

By default, a fetch will only occur if [FormItem.displayField](#attr-formitemdisplayfield) is specified, and the item does not have an explicit [FormItem.valueMap](#attr-formitemvaluemap) containing the data value as a key.  
However you can also set [FormItem.alwaysFetchMissingValues](#attr-formitemalwaysfetchmissingvalues) to have a fetch occur even if no `displayField` is specified. This ensures [FormItem.getSelectedRecord](#method-formitemgetselectedrecord) will return a record if possible - useful for custom formatter functions, etc.

Note - for efficiency we cache the associated record once a fetch has been performed, meaning if the value changes, then reverts to a previously seen value, we do not kick off an additional fetch to pick up the display value for the previously seen data value. If necessary this cache may be explicitly invalidated via a call to [FormItem.invalidateDisplayValueCache](#method-formiteminvalidatedisplayvaluecache)

### Groups

- display_values

### See Also

- [FormItem.optionDataSource](#attr-formitemoptiondatasource)
- [FormItem.getSelectedRecord](#method-formitemgetselectedrecord)
- [FormItem.filterLocally](#attr-formitemfilterlocally)

**Flags**: IRWA

---
## Attr: FormItem.canEditOpaqueValues

### Description
If true, indicates that this FormItem is capable of editing "opaque" values, ie, objects that are more complex than simple primitive types like numbers, strings and dates. Ordinarily, you use the [SimpleType system](SimpleType.md#class-simpletype) to convert these opaque values into "atomic" values that can be edited by the built-in editors like [TextItem](TextItem.md#class-textitem). However, sometimes you to create a custom editor that knows how to edit a particular opaque type in a domain-specific way - for example, a composite custom FormItem that allows the user to edit both a number and a currency code, both of which are needed to make a proper monetary amount (for that particular application). When this value is set, the FormItem will manage the opaque value directly, rather than it being filtered through calls to [getAtomicValue()](SimpleType.md#method-simpletypegetatomicvalue) and [updateAtomicValue()](SimpleType.md#method-simpletypeupdateatomicvalue). Note, if you set this flag on a FormItem that does not have the ability to edit an opaque value (which is something that must be custom-coded) then you will get garbage in your editor, if not an outright crash.

**Flags**: IRA

---
## Attr: FormItem.pickerIconWidth

### Description
If [showPickerIcon](#attr-formitemshowpickericon) is true for this item, this property governs the size of the picker icon. If unset, the picker icon will be sized as a square to fit in the available height for the icon.

Note that if spriting is being used, and the image to be displayed is specified using css properties such as `background-image`, `background-size`, changing this value may result in an unexpected appearance as the image will not scale.  
Scaleable spriting can be achieved using the [SCSpriteConfig](../reference.md#type-scspriteconfig) format. See the section on spriting in the [skinning overview](../kb_topics/skinning.md#kb-topic-skinning--theming) for further information.

### Groups

- pickerIcon

**Flags**: IRWA

---
## Attr: FormItem.showOverIcons

### Description
If we're showing icons, should we change their image source to the appropriate _over_ source when the user rolls over (or puts focus onto) them? Can be overridden on a per icon basis by the formItemIcon `showOver` property.

### Groups

- formIcons

**Flags**: IRWA

---
## Attr: FormItem.pickerIconHeight

### Description
If [showPickerIcon](#attr-formitemshowpickericon) is true for this item, this property governs the size of the picker icon. If unset, the picker icon will be sized as a square to fit in the available height for the icon.

Note that if spriting is being used, and the image to be displayed is specified using css properties such as `background-image`, `background-size`, changing this value may result in an unexpected appearance as the image will not scale.  
Scaleable spriting can be achieved using the [SCSpriteConfig](../reference.md#type-scspriteconfig) format. See the section on spriting in the [skinning overview](../kb_topics/skinning.md#kb-topic-skinning--theming) for further information.

### Groups

- pickerIcon

**Flags**: IRWA

---
## Attr: FormItem.requiredWhen

### Description
Criteria to be evaluated to determine whether this FormItem should be [required](#attr-formitemrequired).

Criteria are evaluated against the ${isc.DocUtils.linkForRef('method:DynamicForm.getValues','form\\'s current values')} as well as the current [rule context](Canvas.md#attr-canvasrulescope). Criteria are re-evaluated every time form values or the rule context changes, whether by end user action or by programmatic calls.

A basic criteria uses textMatchStyle:"exact". When specified in [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml) this property allows [shorthand formats](../kb_topics/xmlCriteriaShorthand.md#kb-topic-xmlcriteriashorthand) for defining criteria.

Note: A FormItem using requiredWhen must have a [FormItem.name](#attr-formitemname) defined.

### Groups

- ruleCriteria
- validation

**Flags**: IR

---
## Attr: FormItem.multipleValueSeparator

### Description
If this item is displaying multiple values, this property will be the string that separates those values for display purposes.

### Groups

- display_values

**Flags**: IR

---
## Attr: FormItem.hoverWidth

### Description
Option to specify a width for any hover shown for this item.

### Groups

- Hovers

### See Also

- [DynamicForm.itemHoverWidth](DynamicForm.md#attr-dynamicformitemhoverwidth)

**Flags**: IRW

---
## Attr: FormItem.supportsCutPasteEvents

### Description
Does the current formItem support native cut and paste events?

This attribute only applies to freeform text entry fields such as [TextItem](TextItem.md#class-textitem) and [TextAreaItem](TextAreaItem.md#class-textareaitem), and only if [FormItem.changeOnKeypress](#attr-formitemchangeonkeypress) is true. If true, developers can detect the user editing the value via cut or paste interactions (triggered from keyboard shortcuts or the native browser menu options) using the [FormItem.isCutEvent](#method-formitemiscutevent) and [FormItem.isPasteEvent](#method-formitemispasteevent) methods. This allows custom cut/paste handling to be added to the various change notification flow methods including [FormItem.change](#method-formitemchange), and [FormItem.transformInput](#method-formitemtransforminput).

**Flags**: IR

---
## Attr: FormItem.ariaRole

### Description
ARIA role of this formItem. Usually does not need to be manually set - see [accessibility](../kb_topics/accessibility.md#kb-topic-accessibility--section-508-compliance).

### Groups

- accessibility

**Flags**: IRWA

---
## Attr: FormItem.clipTitle

### Description
If the title for this form item is showing, and is too large for the available space should the title be clipped?

Null by default - if set to true or false, overrides [DynamicForm.clipItemTitles](DynamicForm.md#attr-dynamicformclipitemtitles).

### Groups

- title

**Flags**: IRW

---
## Attr: FormItem.optionDataSource

### Description
If set, this FormItem will map stored values to display values as though a [ValueMap](../reference_2.md#type-valuemap) were specified, by fetching records from the specified `optionDataSource` and extracting the [valueField](#attr-formitemvaluefield) and [displayField](#attr-formitemdisplayfield) in loaded records, to derive one valueMap entry per record loaded from the optionDataSource.

With the default setting of [fetchMissingValues](#attr-formitemfetchmissingvalues), fetches will be initiated against the optionDataSource any time the FormItem has a non-null value and no corresponding display value is available. This includes when the form is first initialized, as well as any subsequent calls to [FormItem.setValue](#method-formitemsetvalue), such as may happen when [DynamicForm.editRecord](DynamicForm.md#method-dynamicformeditrecord) is called. Retrieved values are automatically cached by the FormItem.

Note that if a normal, static [valueMap](#attr-formitemvaluemap) is **also** specified for the field (either directly in the form item or as part of the field definition in the dataSource), it will be preferred to the data derived from the optionDataSource for whatever mappings are present.

In a databound form, if [FormItem.displayField](#attr-formitemdisplayfield) is specified for a FormItem and `optionDataSource` is unset, `optionDataSource` will default to the form's current DataSource

### Groups

- display_values

### See Also

- [FormItem.invalidateDisplayValueCache](#method-formiteminvalidatedisplayvaluecache)

**Flags**: IRW

---
## Attr: FormItem.valueIcons

### Description
A mapping of logical form item values to [SCImgURL](../reference.md#type-scimgurl)s or the special value "blank", which means that no image will be displayed. If specified, when the form item is set to the value in question, an icon will be displayed with the appropriate source URL.

### Groups

- valueIcons

### See Also

- [FormItem.getValueIcon](#method-formitemgetvalueicon)

**Flags**: IRW

---
## Attr: FormItem.iconHeight

### Description
Default height for form item icons. May be overridden at the icon level by [FormItemIcon.height](FormItemIcon.md#attr-formitemiconheight).

### Groups

- formIcons

**Flags**: IRA

---
## Attr: FormItem.disabledHover

### Description
This text is shown as a tooltip prompt when the cursor hovers over this item and the item is [disabled](#attr-formitemdisabled) or [read-only](#method-formitemsetcanedit) with [readOnlyDisplay:disabled](#attr-formitemreadonlydisplay).

You can also override [itemHoverHTML](#method-formitemitemhoverhtml) on the item to show a custom hover, whether or not the item is disabled.

Note that when the form is [disabled](Canvas.md#attr-canvasdisabled), or when this item [suppresses hovers](#attr-formitemcanhover), nothing will be shown.

**Flags**: IRW

---
## Attr: FormItem.canTabToIcons

### Description
Should this item's [icons](#attr-formitemicons) and [picker icon](#attr-formitemshowpickericon) be included in the page's tab order by default? If not explicitly set, this property will be derived from [DynamicForm.canTabToIcons](DynamicForm.md#attr-dynamicformcantabtoicons).

Developers may also suppress tabbing to individual icons by setting [FormItemIcon.tabIndex](FormItemIcon.md#attr-formitemicontabindex) to `-1`.

Note that if this form item has tabIndex -1, neither the form item nor the icons will be included in the page's tab order.

### Groups

- formIcons

**Flags**: IRWA

---
## Attr: FormItem.originalValueMessage

### Description
Message shown when [showOldValueInHover](#attr-formitemshowoldvalueinhover) is enabled and the value has been modified.

If unset, defaults to the form's [DynamicForm.originalValueMessage](DynamicForm.md#attr-dynamicformoriginalvaluemessage). Otherwise, overrides the form-default `originalValueMessage` for this item.

**Flags**: IRWA

---
## Attr: FormItem.locateItemBy

### Description
When [AutoTest.getElement](AutoTest.md#classmethod-autotestgetelement) is used to parse locator strings generated by [AutoTest.getLocator](AutoTest.md#classmethod-autotestgetlocator) for this form item, should the item be identified? If the locator has a specified [FormItem.name](#attr-formitemname), it is considered to definitely locate the item and no fallback approach will be used.

Otherwise, the following options are available:

*   `"title"` use the title as an identifier within this form
*   `"value"` use the value of the item to identify it (often used for items with a static defaultValue such as HeaderItems
*   `"index"` use the index within the form's items array.

If unset, and the locator has no specified name, default behavior is to identify by title (if available), then value (if available), otherwise by index.

### Groups

- autoTest

### See Also

- [LocatorStrategy](../reference_2.md#type-locatorstrategy)

**Flags**: IRWA

---
## Attr: FormItem.showPickerIconOnFocus

### Description
Show the picker icon when the item gets focus, and hide it when it loses focus. Can be overridden at the icon level by [FormItemIcon.showOnFocus](FormItemIcon.md#attr-formitemiconshowonfocus).

Note that a pickerIcon marked as disabled will not be shown on focus even if this flag is true by default. This may be overridden by [FormItem.showDisabledIconsOnFocus](#attr-formitemshowdisablediconsonfocus).

### Groups

- formIcons

**Flags**: IRWA

---
## Attr: FormItem.displayField

### Description
If set, this item will display a value from another field to the user instead of showing the underlying data value for the [field name](#attr-formitemname).

This property is used in two ways:

The item will display the displayField value from the [record currently being edited](DynamicForm.md#method-dynamicformgetvalues) if [FormItem.useLocalDisplayFieldValue](#attr-formitemuselocaldisplayfieldvalue) is true, (or if unset and the conditions outlined in the documentation for that property are met).

If this field has an [FormItem.optionDataSource](#attr-formitemoptiondatasource), this property is used by default to identify which value to use as a display value in records from this related dataSource. In this usage the specified displayField must be explicitly defined in the optionDataSource to be used - see [FormItem.getDisplayFieldName](#method-formitemgetdisplayfieldname) for more on this behavior.  
If not using [local display values](#attr-formitemuselocaldisplayfieldvalue), the display value for this item will be derived by performing a fetch against the [option dataSource](#method-formitemgetoptiondatasource) to find a record where the [value field](#method-formitemgetvaluefieldname) matches this item's value, and use the `displayField` value from that record.  
In addition to this, PickList-based form items that provide a list of possible options such as the [SelectItem](SelectItem.md#class-selectitem) or [ComboBoxItem](ComboBoxItem.md#class-comboboxitem) will show the `displayField` values to the user by default, allowing them to choose a new data value (see [FormItem.valueField](#attr-formitemvaluefield)) from a list of user-friendly display values.

This essentially allows the specified `optionDataSource` to be used as a server based [valueMap](../reference.md#kb-topic-valuemap).

If [local display values](#attr-formitemuselocaldisplayfieldvalue) are being used and [FormItem.storeDisplayValues](#attr-formitemstoredisplayvalues) is true, selecting a new value will update both the value for this field and the associated display-field value on the record being edited.

Note: Developers may specify the [FormItem.foreignDisplayField](#attr-formitemforeigndisplayfield) property in addition to `displayField`. This is useful for cases where the display field name in the local dataSource differs from the display field name in the optionDataSource. See the documentation for [DataSourceField.foreignDisplayField](DataSourceField.md#attr-datasourcefieldforeigndisplayfield) for more on this.  
If a foreignDisplayField is specified, as with just displayField, if [local display values](#attr-formitemuselocaldisplayfieldvalue) are being used and [FormItem.storeDisplayValues](#attr-formitemstoredisplayvalues) is true, when the user chooses a value the associated display-field value on the record being edited will be updated. In this case it would be set to the foreignDisplayField value from the related record. This means foreignDisplayField is always expected to be set to the equivalent field in the related dataSources.  
Developers looking to display some _other_ arbitrary field(s) from the related dataSource during editing should consider using custom [PickList.pickListFields](PickList.md#attr-picklistpicklistfields) instead of setting a foreignDisplayField.

Note that if `optionDataSource` is set and no valid display field is specified, [FormItem.getDisplayFieldName](#method-formitemgetdisplayfieldname) will return the dataSource title field by default.

If a displayField is specified for a freeform text based item (such as a [ComboBoxItem](ComboBoxItem.md#class-comboboxitem)), any user-entered value will be treated as a display value. In this scenario, items will derive the data value for the item from the first record where the displayField value matches the user-entered value. To avoid ambiguity, developers may wish to avoid this usage if display values are not unique.

### Groups

- databinding

### See Also

- [FormItem.getDisplayFieldName](#method-formitemgetdisplayfieldname)
- [FormItem.invalidateDisplayValueCache](#method-formiteminvalidatedisplayvaluecache)

**Flags**: IR

---
## Attr: FormItem.timeFormatter

### Description
Time-format to apply to date type values within this formItem. If specified, any dates displayed in this item will be formatted as times using the appropriate format. This is most commonly only applied to fields specified as type `"time"` though if no explicit [FormItem.dateFormatter](#attr-formitemdateformatter) is specified it will be respected for other fields as well.

If unspecified, a timeFormatter may be defined [at the component level](DynamicForm.md#attr-dynamicformtimeformatter) and will be respected by fields of type `"time"`.

### Groups

- appearance

### See Also

- [FormItem.format](#attr-formitemformat)

**Flags**: IRWA

---
## Attr: FormItem.endRow

### Description
Whether this item should end the row it's in in the form layout

### Groups

- formLayout

### See Also

- [FormItem.linearEndRow](#attr-formitemlinearendrow)

**Flags**: IRW

---
## Attr: FormItem.titleSuffix

### Description
The string appended to this item's title. The [DynamicForm.titleSuffix](DynamicForm.md#attr-dynamicformtitlesuffix) is used by default.

### Groups

- title

### See Also

- [FormItem.requiredTitleSuffix](#attr-formitemrequiredtitlesuffix)

**Flags**: IRW

---
## Attr: FormItem.optionOperationId

### Description
If this item has a specified `optionDataSource`, this attribute may be set to specify an explicit [DSRequest.operationId](DSRequest.md#attr-dsrequestoperationid) when performing a fetch against the option dataSource to pick up display value mapping.

### Groups

- databinding

**Flags**: IRA

---
## Attr: FormItem.decimalPrecision

### Description
Applies only to fields of type "float" and affects how many significant digits are shown.

For example, with decimalPrecision 3, if the field value is 343.672677, 343.673 is shown.

If the value is 125.2, 125.2 is shown - decimalPrecision will not cause extra zeros to be added. Use [DataSourceField.decimalPad](DataSourceField.md#attr-datasourcefielddecimalpad) for this.

A number is always shown with its original precision when edited.

### Groups

- appearance

**Flags**: IRW

---
## Attr: FormItem.printReadOnlyTextBoxStyle

### Description
CSS class name to apply to the print view of an item's text box if the item is [canEdit:false](#attr-formitemcanedit), with [readOnlyDisplay:static](#attr-formitemreadonlydisplay).

If specified this will take precedence over [FormItem.printTextBoxStyle](#attr-formitemprinttextboxstyle) for static readonly items.

### Groups

- printing
- formItemStyling

**Flags**: IRW

---
## Attr: FormItem.form

### Description
A Read-Only pointer to this formItem's DynamicForm widget.

**Flags**: R

---
## Attr: FormItem.disabled

### Description
Whether this item is disabled. Can be updated at runtime via the `setDisabled()` method. Note that if the widget containing this formItem is disabled, the formItem will behave in a disabled manner regardless of the setting of the item.disabled property.

Note that not all items can be disabled, and not all browsers show an obvious disabled style for native form elements.

### Groups

- appearance

### See Also

- [FormItem.setDisabled](#method-formitemsetdisabled)

**Flags**: IRW

---
## Attr: FormItem.clipStaticValue

### Description
If this item is [read-only](#method-formitemgetcanedit) and is using [readOnlyDisplay](#attr-formitemreadonlydisplay) "static", should the item value be clipped if it overflows the specified size of the item? If set, overrides the form-level [DynamicForm.clipStaticValue](DynamicForm.md#attr-dynamicformclipstaticvalue) default.

### See Also

- [DynamicForm.clipStaticValue](DynamicForm.md#attr-dynamicformclipstaticvalue)

**Flags**: IR

---
## Attr: FormItem.redrawOnChange

### Description
If true, this item will cause the entire form to be redrawn when the item's "elementChanged" event is done firing

### Groups

- changeHandling

**Flags**: IRW

---
## Attr: FormItem.selectOnFocus

### Description
Allows the [selectOnFocus](DynamicForm.md#attr-dynamicformselectonfocus) behavior to be configured on a per-FormItem basis. Normally all items in a form default to the value of [DynamicForm.selectOnFocus](DynamicForm.md#attr-dynamicformselectonfocus).

### Groups

- focus

**Flags**: IRW

---
## Attr: FormItem.pickerIconDefaults

### Description
Block of default properties to apply to the pickerIcon for this widget. Intended for class-level customization: To modify this value we recommend using [Class.changeDefaults](Class.md#classmethod-classchangedefaults) rather than directly assigning a value to the property.

### Groups

- pickerIcon

**Flags**: IRWA

---
## Attr: FormItem.errorIconProperties

### Description
[Icon-properties](../reference.md#object-formitemicon) to apply to the [error-icon](#attr-formitemshowerroricon) when [FormItem.showErrorIconInline](#attr-formitemshowerroriconinline) is true.

**Flags**: IRA

---
## Attr: FormItem.showOver

### Description
When the user rolls over this item, should it be re-styled to indicate it has focus?

When enabled, the "Over" styling is applied to the text box, control table (if present), and pickerIcon (if present), and any icons where [FormItemIcon.showOver](FormItemIcon.md#attr-formitemiconshowover) is true and [FormItemIcon.showOverWhen](FormItemIcon.md#attr-formitemiconshowoverwhen) is set to "textBox".  
These behaviors can be disabled piecemeal via [FormItem.updateTextBoxOnOver](#attr-formitemupdatetextboxonover), [FormItem.updateControlOnOver](#attr-formitemupdatecontrolonover) and [FormItem.updatePickerIconOnOver](#attr-formitemupdatepickericononover) properties.

Developers may also show rollover styling for other icons (see [FormItem.showOverIcons](#attr-formitemshowovericons) and [FormItemIcon.showOverWhen](FormItemIcon.md#attr-formitemiconshowoverwhen)).

See [formItemStyling](../kb_topics/formItemStyling.md#kb-topic-formitem-styling) for more details on formItem styling.

### Groups

- formItemStyling

**Flags**: IRWA

---
## Attr: FormItem.editPendingCSSText

### Description
Custom CSS text to be applied to cells with pending edits that have not yet been submitted.

### Groups

- appearance

**Flags**: IRWA

---
## Attr: FormItem.canFocus

### Description
Is this form item focusable? Setting this property to true on an otherwise non-focusable element such as a [StaticTextItem](StaticTextItem.md#class-statictextitem) will cause the item to be included in the page's tab order and respond to keyboard events.

### Groups

- focus

**Flags**: IRA

---
## Attr: FormItem.canEdit

### Description
Is this form item editable (canEdit:true) or read-only (canEdit:false)? Setting the form item to non-editable causes it to render as read-only. Can be updated at runtime via the [setCanEdit()](#method-formitemsetcanedit) method.

Read-only appearance may be specified via [FormItem.readOnlyDisplay](#attr-formitemreadonlydisplay). The default setting for this value (`"readOnly"`) differs from the disabled state in that the form item is not rendered with disabled styling and most form items will allow copying of the contents while read-only but do not while disabled.

Note that for forms bound to a [DataSource](DataSource.md#class-datasource), if this property is not explicitly set at the item level, its default value will match the [DynamicForm.canEditFieldAttribute](DynamicForm.md#attr-dynamicformcaneditfieldattribute) on the associated dataSource field.

Developers should also be aware that the [FormItem.readOnlyDisplay](#attr-formitemreadonlydisplay) attribute is unrelated to the [DataSourceField.readOnlyEditorType](DataSourceField.md#attr-datasourcefieldreadonlyeditortype) attribute. When a DynamicForm is first bound to a dataSource, for [canEdit:false](DataSourceField.md#attr-datasourcefieldcanedit) DataSourceFields, [DataSourceField.readOnlyEditorType](DataSourceField.md#attr-datasourcefieldreadonlyeditortype) will determine what [FormItemType](../reference.md#type-formitemtype) should be created for the field. Once created, a FormItem's type can not be changed. Setting [FormItem.canEdit](#attr-formitemcanedit) at runtime will simply change the appearance of the item to allow or disallow editing of the item.

### Groups

- readOnly

### See Also

- [FormItem.setCanEdit](#method-formitemsetcanedit)
- [DynamicForm.setCanEdit](DynamicForm.md#method-dynamicformsetcanedit)

**Flags**: IRW

---
## ClassMethod: FormItem.create

### Description
FormItem.create() should never be called directly, instead, create a [DynamicForm](DynamicForm.md#class-dynamicform) and specify form items via [form.items](DynamicForm.md#attr-dynamicformitems).

---
## ClassMethod: FormItem.getPickerIcon

### Description
Returns a [FormItemIcon](../reference.md#object-formitemicon) for a standard picker with skin-specific settings.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pickerName | [PickerIconName](../reference.md#type-pickericonname) | false | — | Name of picker icon |
| properties | [FormItemIcon Properties](#type-formitemicon-properties) | true | — | Properties to apply to new picker icon |

### Returns

`[FormItemIcon Properties](#type-formitemicon-properties)` — the icon for picker

---
## Method: FormItem.show

### Description
Show this form item.

This will cause the form to redraw. If this item had an item.showIf expression, it will be destroyed.

---
## Method: FormItem.getPageTop

### Description
Returns the drawn page-top coordinate of this form item in pixels.

### Returns

`[int](../reference.md#type-int)` — page-top coordinate in px

### Groups

- positioning

---
## Method: FormItem.mapDisplayToValue

### Description
Given a display value for this FormItem, return the underlying data value. This is done by reverse value-mapping, and/or parsing.

This method is called by the framework to derive an underlying data value for a given display value (ie, the value the user sees and interacts with) in a FormItem. Your own code can call this method if you need to programmatically obtain the underlying data value for a given display value. However, it is **not** intended as an override point, and you should not treat it as one. If you have a field that requires the stored value to be different from the displayed value, and the requirement cannot be satisfied with a [valueMap](#attr-formitemvaluemap) for some reason, you can add custom parsing logic by implementing [parseEditorValue()](#method-formitemparseeditorvalue)

This method is also **not** intended as a place where you can validate, sanitize, transform or canonicalize user input

*   To ensure you get well-formed input values, use [input masks](TextItem.md#attr-textitemmask) or the [change() event](#method-formitemchange)
*   To transform or canonicalize input values, use a [mask validator](../reference.md#type-validatortype) with "transformTo". See the link to "mask validator" for more details and an example of this
*   To transform or canonicalize input character-by-character as the user types, use [transformInput()](#method-formitemtransforminput)

#### Deriving the data value
The process of deriving an underlying data display value from a display value involves the following steps:

*   If the formItem declares a [FormItem.parseEditorValue](#method-formitemparseeditorvalue) method, it is called
*   Otherwise, if the formItem is of a [SimpleType](SimpleType.md#class-simpletype) that declares a [parseInput()](SimpleType.md#method-simpletypeparseinput) method, it is called
*   If the formItem is of a `SimpleType` that [inheritsFrom](SimpleType.md#attr-simpletypeinheritsfrom) "date", "time" or "datetime", it will be parsed as a date, time or datetime. Note, this parsing step is applied on top of custom SimpleType- and FormItem-level parsing
*   If the formItem declares a [valueMap](#attr-formitemvaluemap), a value is derived by looking up the display value (including the effects of any parsing we may have done so far) in the valueMap

**Note:** Unlike the corollary method [mapValueToDisplay()](#method-formitemmapvaluetodisplay), there is no special built-in handling of `[DataSourceField.multiple](DataSourceField.md#attr-datasourcefieldmultiple):true` fields. If you want an array to be parsed out of some user input, you must write the parser method to do so.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [String](#type-string) | false | — | display value |

### Returns

`[Any](#type-any)` — value re-mapped for storing

### See Also

- [FormItem.mapValueToDisplay](#method-formitemmapvaluetodisplay)

---
## Method: FormItem.titleHoverHTML

### Description
If defined, this method should return the HTML to display in a hover canvas when the user holds the mousepointer over this item's title. Return null to suppress the hover canvas altogether.

If not defined, [DynamicForm.titleHoverHTML](DynamicForm.md#method-dynamicformtitlehoverhtml) will be evaluated to determine hover content instead.

If [FormItem.canHover](#attr-formitemcanhover) is set to false, this method is not called.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | Pointer to this item |
| form | [DynamicForm](#type-dynamicform) | false | — | This items form |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML to be displayed in the hover

### Groups

- Hovers

### See Also

- [FormItem.canHover](#attr-formitemcanhover)
- [FormItem.prompt](#attr-formitemprompt)
- [FormItem.titleHover](#method-formitemtitlehover)
- [FormItem.itemHoverHTML](#method-formitemitemhoverhtml)
- [FormItem.showClippedTitleOnHover](#attr-formitemshowclippedtitleonhover)

**Flags**: A

---
## Method: FormItem.setIconShowOnFocus

### Description
Sets [FormItemIcon.showOnFocus](FormItemIcon.md#attr-formitemiconshowonfocus) for the supplied icon, and causes that icon's visibility to be updated and the item redrawn as appropriate.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [Identifier](../reference.md#type-identifier) | false | — | [name](FormItemIcon.md#attr-formitemiconname) of the icon to update |
| showOnFocus | [Boolean](#type-boolean) | false | — | new value of [FormItemIcon.showOnFocus](FormItemIcon.md#attr-formitemiconshowonfocus) |

### Groups

- formIcons

---
## Method: FormItem.getVisibleWidth

### Description
Output the drawn width for this item in pixels. This method is only reliable after the item has been drawn into the page.

### Returns

`[Integer](../reference_2.md#type-integer)` — width of the form item

### Groups

- sizing

**Flags**: A

---
## Method: FormItem.parseEditorValue

### Description
Allows customization of how a used-entered text value is converted to the FormItem's logical stored value (the value available from [FormItem.getValue](#method-formitemgetvalue)).

This method only applies to form items which show an editable text entry area, such at the [TextItem](TextItem.md#class-textitem) or [TextAreaItem](TextAreaItem.md#class-textareaitem).

See also [FormItem.formatEditorValue](#method-formitemformateditorvalue)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [String](#type-string) | false | — | value as entered by the user |
| form | [DynamicForm](#type-dynamicform) | false | — | pointer to the dynamicForm containing this item |
| item | [FormItem](#type-formitem) | false | — | pointer to this item |

### Returns

`[Any](#type-any)` — Data value to store for this item.

---
## Method: FormItem.getGridColNum

### Description
If this formItem is part of a [ListGrid](ListGrid_1.md#class-listgrid)'s [inline edit form](ListGrid_1.md#attr-listgridcanedit), returns the number of the grid column this formItem is responsible for editing, but **only** if a row is currently being edited. If the formItem is not part of a ListGrid inline edit for any reason, this method returns null. Reasons for a formItem not being part of an inline edit include

*   The item is part of an ordinary DynamicForm, not an inline edit form
*   There is no row in the grid currently being edited
*   A row is being edited, but this formItem is not currently visible and is being excluded because of horizontal incremental rendering (where SmartClient avoids drawing grid columns that would not be visible without scrolling)

### Returns

`[Integer](../reference_2.md#type-integer)` — The grid column number being edited by this formItem, or null, as described above

---
## Method: FormItem.hideIcon

### Description
This method will hide some icon in this item's [FormItem.icons](#attr-formitemicons) array, if it is currently visible. Note that once this method has been called, any previously specified [FormItemIcon.showIf](FormItemIcon.md#method-formitemiconshowif) will be discarded.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [Identifier](../reference.md#type-identifier) | false | — | [name](FormItemIcon.md#attr-formitemiconname) of the icon to be hidden. |

---
## Method: FormItem.getValueAsFloat

### Description
Return the value tracked by this form item as a Float. If the value cannot be parsed to a valid float, null will be returned.

### Returns

`[Float](../reference.md#type-float)` — value of this element

### See Also

- [FormItem.getValue](#method-formitemgetvalue)

---
## Method: FormItem.getIconTabPosition

### Description
Returns the desired tab-position of some icon with respect to other focusable sub-elements for this formItem.

Default implementation returns the index of the icon in the icons array, (plus one if a pickerIcon is showing) meaning users can tab through icons in order. Has no effect for non-focusable icons.

### Returns

`[Integer](../reference_2.md#type-integer)` — desired position in the tab-order within this item's sub-elements

---
## Method: FormItem.hide

### Description
Hide this form item.  
  
This will cause the form to redraw. If this item had an item.showIf expression, it will be destroyed.

---
## Method: FormItem.getFieldName

### Description
Return the name for the this formItem.

### Returns

`[String](#type-string)` — name for this form item

### Groups

- drawing

**Flags**: A

---
## Method: FormItem.getValueIcon

### Description
Except when [printing](../kb_topics/printing.md#kb-topic-printing) and [getPrintValueIcon()](#method-formitemgetprintvalueicon) is implemented, implementing this stringMethod allows the developer to specify the image source for an icon to be displayed for the current form item value.

The special value "blank" means that no image will be displayed. This is typically used in conjunction with [FormItem.getValueIconStyle](#method-formitemgetvalueiconstyle) to implement spriting of the value icon. Note that when spriting the value icon, it is recommended to implement `getPrintValueIcon()` and [getPrintValueIconStyle()](#method-formitemgetprintvalueiconstyle) when printing.

Takes precedence over [FormItem.valueIcons](#attr-formitemvalueicons)

The returned [SCImgURL](../reference.md#type-scimgurl), if not `null` or "blank", will be suffixed with [FormItem.imageURLSuffix](#attr-formitemimageurlsuffix).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | value of the item. |

### Returns

`[SCImgURL](../reference.md#type-scimgurl)` — the image source or `null` if no value icon should be displayed.

### Groups

- valueIcons

### See Also

- [FormItem.getPrintValueIcon](#method-formitemgetprintvalueicon)

---
## Method: FormItem.focusInItem

### Description
Move the keyboard focus into this item's focusable element

### Groups

- eventHandling
- focus

---
## Method: FormItem.setValue

### Description
Set the value of the form item to the value passed in

NOTE: for valueMap'd items, newValue should be data value not displayed value

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [Any](#type-any) | false | — | value to set the element to |

---
## Method: FormItem.titleDoubleClick

### Description
Notification method fired when the user double-clicks the title for this item

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | the managing DynamicForm instance |
| item | [FormItem](#type-formitem) | false | — | the form item whose title was double-clicked |

### Returns

`[Boolean](#type-boolean)` — Return false to cancel the doubleclick event. This will prevent the event from bubbling up, suppressing [doubleClick](Canvas.md#method-canvasdoubleclick) on the form containing this item.

---
## Method: FormItem.canEditCriterion

### Description
When a dynamic form is editing an advanced criteria object via [DynamicForm.setValuesAsCriteria](DynamicForm.md#method-dynamicformsetvaluesascriteria), this method is used to determine which sub-criteria apply to which form item(s).

This method will be called on each item, and passed the sub-criterion of the AdvancedCriteria object. It should return true if the item can edit the criterion, otherwise false. If it returns true, setValuesAsCriteria() will call [FormItem.setCriterion](#method-formitemsetcriterion) to actually apply the criterion to the form item, and [DynamicForm.getValuesAsCriteria](DynamicForm.md#method-dynamicformgetvaluesascriteria) can subsequently retrieve the edited criterion by calling [FormItem.getCriterion](#method-formitemgetcriterion).

Default implementation will return true if the criterion `fieldName` and `operator` match the fieldName and operator (or default operator) for this item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criterion | [Criterion](#type-criterion) | false | — | sub-criterion from an AdvancedCriteria object |

### Returns

`[boolean](../reference.md#type-boolean)` — return true if this item can edit the criterion in question.

### Groups

- criteriaEditing

**Flags**: A

---
## Method: FormItem.getGridRowNum

### Description
If this formItem is part of a [ListGrid](ListGrid_1.md#class-listgrid)'s [inline edit form](ListGrid_1.md#attr-listgridcanedit), returns the number of the row currently being edited. If the formItem is not part of a ListGrid inline edit for any reason, this method returns null. Reasons for a formItem not being part of an inline edit include

*   The item is part of an ordinary DynamicForm, not an inline edit form
*   There is no row in the grid currently being edited
*   A row is being edited, but this formItem is not currently visible and is being excluded because of horizontal incremental rendering (where SmartClient avoids drawing grid columns that would not be visible without scrolling)

### Returns

`[Integer](../reference_2.md#type-integer)` — The grid row number being edited or null, as described above

---
## Method: FormItem.keyDown

### Description
StringMethod fired in response to a keydown while focused in this form item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | Item over which the keydown occurred |
| form | [DynamicForm](#type-dynamicform) | false | — | Pointer to the item's form |
| keyName | [KeyName](../reference_2.md#type-keyname) | false | — | Name of the key pressed (Example: `"A"`, `"Enter"`) |

### Returns

`[Boolean](#type-boolean)` — return false to attempt to cancel the event. Note for general purpose APIs for managing whether user input is allowed, use [FormItem.change](#method-formitemchange) or [FormItem.transformInput](#method-formitemtransforminput) instead.

### Groups

- eventHandling

---
## Method: FormItem.selectedRecordChanged

### Description
Notification method fired for [data bound items](#attr-formitemoptiondatasource) with [FormItem.fetchMissingValues](#attr-formitemfetchmissingvalues) enabled when the [selected record](#method-formitemgetselectedrecord) is updated as a result of the value changing or a fetch for a new record completing.  
Note that a formItem with an optionDataSource may avoid fetching an associated record altogether in some cases. See [FormItem.fetchMissingValues](#attr-formitemfetchmissingvalues) and [FormItem.alwaysFetchMissingValues](#attr-formitemalwaysfetchmissingvalues). Developers should also be aware that if [PickList.fetchDisplayedFieldsOnly](PickList.md#attr-picklistfetchdisplayedfieldsonly) is set (or some custom [fetch operation](#attr-formitemoptionoperationid) has been specified), the data returned from the server may include only a subset of dataSource fields rather than complete records.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | new selected record. May be null if the item has been set to a value with no associated record. |

---
## Method: FormItem.getDisplayValue

### Description
Returns this item's value with any valueMap applied to it - the value as currently displayed to the user.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | true | — | optional stored value to be mapped to a display value. Default is to use the form's current value |

### Returns

`[Any](#type-any)` — value displayed to the user

### Groups

- valueMap

---
## Method: FormItem.getTop

### Description
Returns the top coordinate of the form item in pixels. Note that this method is only reliable after the item has been drawn out.

### Returns

`[int](../reference.md#type-int)` — top position in pixels

### Groups

- positioning
- sizing

---
## Method: FormItem.showIf

### Description
Expression that's evaluated to see if an item should be dynamically hidden.

`showIf()` is evaluated whenever the form draws or redraws.

Note that explicit calls to [FormItem.show](#method-formitemshow) or [FormItem.hide](#method-formitemhide) will will wipe out the `showIf` expression.

Alternatively, you can use [Criteria](../reference_2.md#type-criteria) to declare when a FormItem is visible via [FormItem.visibleWhen](#attr-formitemvisiblewhen).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | the form item itself (also available as "this") |
| value | [Any](#type-any) | false | — | current value of the form item |
| form | [DynamicForm](#type-dynamicform) | false | — | the managing DynamicForm instance |
| values | [Object](../reference.md#type-object) | false | — | the current set of values for the form as a whole |

### Returns

`[boolean](../reference.md#type-boolean)` — whether the item should be shown

**Flags**: A

---
## Method: FormItem.getIconHeight

### Description
Takes an icon definition object, and returns the height for that icon in px.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [Object](../reference.md#type-object) | false | — | icon definition object for this item. |

### Returns

`[int](../reference.md#type-int)` — height of the form item icon in px

### Groups

- sizing

**Flags**: A

---
## Method: FormItem.addIcon

### Description
Adds a [FormItemIcon](../reference.md#object-formitemicon) to this item. If the optional index parameter is not passed, the icon is added to the end of the existing [icon list](#attr-formitemicons).

If the passed icon already exists in the [icon list](#attr-formitemicons), by [name](FormItemIcon.md#attr-formitemiconname), the original icon is moved to the new index and no new icon is added.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [FormItemIcon](#type-formitemicon) | false | — | the icon to add |
| index | [int](../reference.md#type-int) | true | — | the index to add the icon at - if omitted, add the icon to the end of the current icon list |

### Returns

`[FormItemIcon](#type-formitemicon)` — the live form item icon

---
## Method: FormItem.valueHover

### Description
Optional stringMethod to fire when the user hovers over this item's value. Return false to suppress default behavior of showing a hover canvas containing the HTML returned by [FormItem.valueHoverHTML](#method-formitemvaluehoverhtml) / [DynamicForm.valueHoverHTML](DynamicForm.md#method-dynamicformvaluehoverhtml).

If [FormItem.canHover](#attr-formitemcanhover) is set to false, this method is not called.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | Pointer to this item |
| form | [DynamicForm](#type-dynamicform) | false | — | This items form |

### Groups

- Hovers

### See Also

- [FormItem.itemHover](#method-formitemitemhover)

**Flags**: A

---
## Method: FormItem.setShowIconsOnFocus

### Description
Sets [FormItem.showIconsOnFocus](#attr-formitemshowiconsonfocus) and causes the visibility of all [FormItem.icons](#attr-formitemicons) to be updated and the item redrawn as appropriate.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showIconsOnFocus | [Boolean](#type-boolean) | false | — | new value of [FormItem.showIconsOnFocus](#attr-formitemshowiconsonfocus) |

### Groups

- formIcons

---
## Method: FormItem.setShowPickerIconOnFocus

### Description
Sets [FormItem.showPickerIconOnFocus](#attr-formitemshowpickericononfocus) and causes the visibility of the picker icon to be updated and the item redrawn as appropriate.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showPickerIconOnFocus | [Boolean](#type-boolean) | false | — | new value of [FormItem.showPickerIconOnFocus](#attr-formitemshowpickericononfocus) |

### Groups

- formIcons

---
## Method: FormItem.setCriterion

### Description
Update this form item to reflect a criterion object from within an AdvancedCriteria. Called by [DynamicForm.setValuesAsCriteria](DynamicForm.md#method-dynamicformsetvaluesascriteria) when [FormItem.canEditCriterion](#method-formitemcaneditcriterion) returns true for this item.

Default implementation simply calls [FormItem.setValue](#method-formitemsetvalue) with the `value` of the criterion passed in

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criterion | [Criterion](#type-criterion) | false | — | criterion to edit |

### Groups

- criteriaEditing

**Flags**: A

---
## Method: FormItem.setReadOnlyDisplay

### Description
Setter for [FormItem.readOnlyDisplay](#attr-formitemreadonlydisplay).

Note that calling this method for a [ButtonItem](ButtonItem.md#class-buttonitem) with [ButtonItem.enableWhen](ButtonItem.md#attr-buttonitemenablewhen) set is an error, since [FormItem.readOnlyDisplay](#attr-formitemreadonlydisplay) is then considered to always be "disabled".

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| appearance | [ReadOnlyDisplayAppearance](../reference_2.md#type-readonlydisplayappearance) | false | — | new `readOnlyDisplay` value. |

---
## Method: FormItem.isDrawn

### Description
Returns true if this item has been written out into the DOM.

### Returns

`[Boolean](#type-boolean)` — whether this item is drawn

### Groups

- drawing

---
## Method: FormItem.getWidth

### Description
Output the width for this element. Note this returns the specified width for the element, which may be "\*" or a percentage value. Use 'getVisibleWidth()' to get the drawn width in pixels.

### Returns

`[int](../reference.md#type-int)|[String](#type-string)` — width of the form element

### Groups

- sizing

**Flags**: A

---
## Method: FormItem.setTop

### Description
For a form with [itemLayout](DynamicForm.md#attr-dynamicformitemlayout):"absolute" only, set the top coordinate of this form item.

Causes the form to redraw.

**Flags**: A

---
## Method: FormItem.showContextMenu

### Description
Called when the mouse is right-clicked anywhere in this formItem. If the implementation returns false, default browser behavior is cancelled.

Note that it can be bad practice to cancel this method if the mouse is over the data element for the item, because doing so would replace the builtin browser-default menus that users may expect. You can use [DynamicForm.getEventItemInfo](DynamicForm.md#method-dynamicformgeteventiteminfo) to return an [info object](../reference_2.md#object-formitemeventinfo) that can be used to determine which part of the item is under the mouse.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | the managing DynamicForm instance |
| item | [FormItem](#type-formitem) | false | — | the form item itself (also available as "this") |

### Returns

`[Boolean](#type-boolean)` — return false to cancel default behavior

### Groups

- eventHandling

---
## Method: FormItem.getPageRect

### Description
Return the page-level coordinates of this object as a 4 element array.

### Returns

`[Array](#type-array)` — \[left, top, width, height\]

### Groups

- positioning
- sizing

---
## Method: FormItem.keyPress

### Description
StringMethod fired when the user presses a key while focused in this form item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | Item over which the keypress occurred |
| form | [DynamicForm](#type-dynamicform) | false | — | Pointer to the item's form |
| keyName | [KeyName](../reference_2.md#type-keyname) | false | — | Name of the key pressed (Example: `"A"`, `"Enter"`) |
| characterValue | [number](#type-number) | false | — | If this was a character key, this is the numeric value for the character |

### Returns

`[Boolean](#type-boolean)` — return false to attempt to cancel the event. Note for general purpose APIs for managing whether user input is allowed, use [FormItem.change](#method-formitemchange) or [FormItem.transformInput](#method-formitemtransforminput) instead.

### Groups

- eventHandling

---
## Method: FormItem.getLeft

### Description
Returns the left coordinate of this form item in pixels. Note that this method is only reliable after the item has been drawn.

### Returns

`[int](../reference.md#type-int)` — left coordinate within the form in pixels\\

### Groups

- positioning
- sizing

---
## Method: FormItem.keyUp

### Description
StringMethod fired in response to a keyup while focused in this form item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | Item over which the keyup occurred |
| form | [DynamicForm](#type-dynamicform) | false | — | Pointer to the item's form |
| keyName | [KeyName](../reference_2.md#type-keyname) | false | — | Name of the key pressed (Example: `"A"`, `"Enter"`) |

### Returns

`[Boolean](#type-boolean)` — return false to attempt to cancel the event. Note for general purpose APIs for managing whether user input is allowed, use [FormItem.change](#method-formitemchange) or [FormItem.transformInput](#method-formitemtransforminput) instead.

### Groups

- eventHandling

---
## Method: FormItem.iconKeyPress

### Description
StringMethod. Default action to fire when an icon has keyboard focus and the user types a key. May be overridden by setting `keyPress` on the form item icon directly.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| keyName | [KeyName](../reference_2.md#type-keyname) | false | — | name of the key pressed |
| character | [Character](#type-character) | false | — | character produced by the keypress |
| form | [DynamicForm](#type-dynamicform) | false | — | a pointer to this item's form |
| item | [FormItem](#type-formitem) | false | — | a pointer to this form item |
| icon | [FormItemIcon](#type-formitemicon) | false | — | a pointer to the icon that received the click event. |

### Groups

- formIcons

---
## Method: FormItem.formatValue

### Description
Allows customization of how the FormItem's stored value is formatted for display. If you are considering using this method, you should first consider using [FormItem.format](#attr-formitemformat), which provides for simple and flexible declarative formatting of dates, times and numbers, without the need to write formatting code.

By default, this formatter will only be applied to static displays such as [StaticTextItem](StaticTextItem.md#class-statictextitem) or [SelectItem](SelectItem.md#class-selectitem), and does not apply to values displayed in a freely editable text entry field (such as a [TextItem](TextItem.md#class-textitem) or [TextAreaItem](TextAreaItem.md#class-textareaitem)).

To define formatting logic for editable text, developers may:

*   set [TextItem.formatOnBlur](TextItem.md#attr-textitemformatonblur) to true, which causes the static formatter to be applied while the item does not have focus, and then be cleared when the user moves focus to the text field
*   use [FormItem.formatEditorValue](#method-formitemformateditorvalue) and supply a corresponding [FormItem.parseEditorValue](#method-formitemparseeditorvalue) that can convert a formatted and subsequently user-edited value back to a stored value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | Underlying data value to format. May be null. |
| record | [ListGridRecord](#type-listgridrecord) | false | — | The record currently being edited by this form. Essentially the form's current values object. |
| form | [DynamicForm](#type-dynamicform) | false | — | pointer to the DynamicForm |
| item | [FormItem](#type-formitem) | false | — | pointer to the FormItem |

### Returns

`[String](#type-string)` — Display value to show.

---
## Method: FormItem.removeIcon

### Description
Given an icon's [name](FormItemIcon.md#attr-formitemiconname), remove it from this item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [Identifier](../reference.md#type-identifier) | false | — | the name of the icon to remove |

### Returns

`[boolean](../reference.md#type-boolean)` — true if an icon was removed, false otherwise

---
## Method: FormItem.stopHover

### Description
This method is fired when the user rolls off this item (or the title for this item) and will clear any hover canvas shown by the item.

### Groups

- Hovers

**Flags**: A

---
## Method: FormItem.setCanEdit

### Description
Is this form item editable (canEdit:true) or read-only (canEdit:false)? Setting the form item to non-editable causes it to render as read-only, using the appearance specified via [FormItem.readOnlyDisplay](#attr-formitemreadonlydisplay).

The default appearance for canEdit:false items (`readOnlyDisplay:"readOnly"`) differs from the disabled state in that the form item is not rendered with disabled styling and most form items will allow copying of the contents while read-only but do not while disabled.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canEdit | [Boolean](#type-boolean) | false | — | Can this form item be edited? |

### Groups

- readOnly

### See Also

- [FormItem.canEdit](#attr-formitemcanedit)
- [FormItem.setDisabled](#method-formitemsetdisabled)

---
## Method: FormItem.valueHoverHTML

### Description
If defined, this method should return the HTML to display in a hover canvas when the user holds the mousepointer over this item's value. Return null to suppress the hover canvas altogether.

If not defined, [DynamicForm.valueHoverHTML](DynamicForm.md#method-dynamicformvaluehoverhtml) will be evaluated to determine hover content instead.

**Note:** This method is only called when hovering the value/textbox area if [FormItem.showClippedValueOnHover](#attr-formitemshowclippedvalueonhover) is not `true`. Since `showClippedValueOnHover` defaults to `true` for most text-based items, you must explicitly set it to `null` for this method to be invoked. When `showClippedValueOnHover` is `true`, textbox hovers are instead handled via [FormItem.itemHoverHTML](#method-formitemitemhoverhtml).

Additionally, if [FormItem.itemHoverHTML](#method-formitemitemhoverhtml) is customized on the item or form, it takes priority and this method will not be called for textbox hovers.

If [FormItem.canHover](#attr-formitemcanhover) is set to false, this method is not called.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | Pointer to this item |
| form | [DynamicForm](#type-dynamicform) | false | — | This items form |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML to be displayed in the hover

### Groups

- Hovers

### See Also

- [FormItem.canHover](#attr-formitemcanhover)
- [FormItem.showClippedValueOnHover](#attr-formitemshowclippedvalueonhover)
- [FormItem.itemHoverHTML](#method-formitemitemhoverhtml)
- [FormItem.titleHoverHTML](#method-formitemtitlehoverhtml)

**Flags**: A

---
## Method: FormItem.setTabIndex

### Description
Setter for [FormItem.tabIndex](#attr-formitemtabindex).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tabIndex | [Integer](../reference_2.md#type-integer) | false | — | new tabIndex for the item |

---
## Method: FormItem.validate

### Description
Validate this item.

### Returns

`[Boolean](#type-boolean)` — returns true if validation was successful (no errors encountered), false otherwise.

---
## Method: FormItem.disableIcon

### Description
This method will disable some icon in this item's [FormItem.icons](#attr-formitemicons) array, if it is currently enabled.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [Identifier](../reference.md#type-identifier) | false | — | [name](FormItemIcon.md#attr-formitemiconname) of the icon to be disabled. |

### Groups

- enable

### See Also

- [FormItemIcon.disabled](FormItemIcon.md#attr-formitemicondisabled)

---
## Method: FormItem.focus

### Description
Called when this FormItem receives focus.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | the managing DynamicForm instance |
| item | [FormItem](#type-formitem) | false | — | the form item itself (also available as "this") |

### Groups

- eventHandling

---
## Method: FormItem.setDisabled

### Description
Set this item to be enabled or disabled at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| disabled | [boolean](../reference.md#type-boolean) | false | — | true if this item should be disabled |

### Groups

- enable

### See Also

- [FormItem.disabled](#attr-formitemdisabled)
- [FormItem.setCanEdit](#method-formitemsetcanedit)

**Flags**: A

---
## Method: FormItem.valueClipped

### Description
Is the value clipped?

The form item must have value clipping enabled. If a form item type supports the clipValue attribute, then clipValue must be true. [TextItem](TextItem.md#class-textitem)s and derivatives (e.g. [SpinnerItem](SpinnerItem.md#class-spinneritem)) automatically clip their values.

### Returns

`[boolean](../reference.md#type-boolean)` — true if the value is clipped; false otherwise.

---
## Method: FormItem.blur

### Description
Called when this FormItem loses focus.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | the managing DynamicForm instance |
| item | [FormItem](#type-formitem) | false | — | the form item itself (also available as "this") |

### Groups

- eventHandling

---
## Method: FormItem.iconClick

### Description
Notification method called when the user clicks on a form item icon.

The icon's [FormItemIcon.click](FormItemIcon.md#method-formitemiconclick) method if any is called first. Then, if the clicked icon is the [picker icon](#attr-formitemshowpickericon), the [FormItem.pickerIconClick](#method-formitempickericonclick) method is called. Then, this method is called.

This event may be cancelled by returning false to suppress the [FormItem.click](#method-formitemclick) handler from also firing in response to the user interaction.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | a pointer to this item's form |
| item | [FormItem](#type-formitem) | false | — | a pointer to this form item |
| icon | [FormItemIcon](#type-formitemicon) | false | — | a pointer to the icon that received the click event. |

### Returns

`[Boolean](#type-boolean)` — return false to cancel this event

### Groups

- formIcons

---
## Method: FormItem.changed

### Description
Called when a FormItem's value has been changed as the result of user interaction. This method fires after the newly specified value has been stored.

Change/Changed notifications vs _"...When"_ rules: the `change` and `changed` events only fire when an end user modifies a field value. If you are trying to dynamically control the visibility or enabled state of other components in response to these events, consider instead using properties such as [Canvas.visibleWhen](Canvas.md#attr-canvasvisiblewhen), [item.readOnlyWhen](#attr-formitemreadonlywhen), [Canvas.enableWhen](Canvas.md#attr-canvasenablewhen) on the target component. (Similar properties are available on [FormItem](#class-formitem), [Canvas](Canvas.md#class-canvas), [MenuItem](../reference_2.md#object-menuitem) and other components).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | the managing DynamicForm instance |
| item | [FormItem](#type-formitem) | false | — | the form item itself (also available as "this") |
| value | [Any](#type-any) | false | — | The current value (after the change). |

### Groups

- eventHandling

---
## Method: FormItem.doubleClick

### Description
Called when this FormItem is double-clicked.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | the managing DynamicForm instance |
| item | [FormItem](#type-formitem) | false | — | the form item itself (also available as "this") |

### Returns

`[Boolean](#type-boolean)` — Return false to cancel the doubleClick event. This will prevent the event from bubbling up, suppressing [doubleClick](Canvas.md#method-canvasdoubleclick) on the form containing this item.

### Groups

- eventHandling

---
## Method: FormItem.focusAfterItem

### Description
Shifts focus to the next focusable element after this item, skipping any elements nested inside the tabbing group for this item, such as sub-elements, nested canvases in a CanvasItem, or icons.

This method makes use of the [TabIndexManager.shiftFocusAfterGroup](TabIndexManager.md#classmethod-tabindexmanagershiftfocusaftergroup) method to request focus be changed to the next registered entry. By default standard focusable SmartClient UI elements, including Canvases, FormItems, FormItemIcons, etc are registered with the TabIndexManager in the appropriate order, and will accept focus if [focusable](Canvas.md#attr-canvascanfocus), and not [disabled](#attr-formitemdisabled) or [masked](Canvas.md#method-canvasshowclickmask).

Canvases support a similar method: [Canvas.focusAfterGroup](Canvas.md#method-canvasfocusaftergroup).

**NOTE:** Focusable elements created directly in the raw HTML bootstrap or by application code will not be passed focus by this method unless they have also been explicitly registered with the TabIndexManager. See the [tabOrderOverview](../kb_topics/tabOrderOverview.md#kb-topic-tab-order-overview) for more information.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| forward | [boolean](../reference.md#type-boolean) | false | — | direction to shift focus - true to move forward, false to move backwards (as with a shift+tab interaction). |

### Groups

- focus

---
## Method: FormItem.getCriterion

### Description
Override this method if you need to provide a specialized criterion from this formItem when creating an AdvancedCriteria via [DynamicForm.getValuesAsCriteria](DynamicForm.md#method-dynamicformgetvaluesascriteria).

This API is provided to allow you to specify a more complex criterion than the "field-operator-value" criterions that are built-in. Note that the built-in behavior is generally quite flexible and powerful enough for most requirements. An example of a case where you might want to override this method is if you wanted to implement a date range selection (ie, date > x AND date < y) on a form that was combining its other criteria fields with an "or" operator.

Note that this method is part of the criteria editing subsystem: if overridden, it is likely that you will want to also override [FormItem.hasAdvancedCriteria](#method-formitemhasadvancedcriteria) to ensure this method is called by the form, and to support editing of existing advanced criteria you may also need to override [FormItem.canEditCriterion](#method-formitemcaneditcriterion) and [FormItem.setCriterion](#method-formitemsetcriterion).

The default implementation will return a criterion including the form item value, fieldName and specified [FormItem.operator](#attr-formitemoperator), or a default operator derived from the form item data type if no explicit operator is specified.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| textMatchStyle | [TextMatchStyle](../reference_2.md#type-textmatchstyle) | true | — | If passed assume the textMatchStyle will be used when performing a fetch operation with these criteria. This may impact the criterion's operator property. |

### Returns

`[Criterion](#type-criterion)` — criterion object based on this fields current edited value(s).

### Groups

- criteriaEditing

**Flags**: A

---
## Method: FormItem.formatEditorValue

### Description
Allows customization of how the FormItem's stored value is formatted for display in an editable text entry area, such as a [TextItem](TextItem.md#class-textitem) [TextAreaItem](TextAreaItem.md#class-textareaitem). For display values which will not be directly editable by the user, use [FormItem.formatValue](#method-formitemformatvalue) instead.

When customizing how values are displayed during editing, it is almost always necessary to provide a [FormItem.parseEditorValue](#method-formitemparseeditorvalue) as well, in order to convert a formatted and subsequently user-edited value back to a stored value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | Underlying data value to format. May be null. |
| record | [ListGridRecord](#type-listgridrecord) | false | — | The record currently being edited by this form. Essentially the form's current values object. |
| form | [DynamicForm](#type-dynamicform) | false | — | pointer to the DynamicForm |
| item | [FormItem](#type-formitem) | false | — | pointer to the FormItem |

### Returns

`[String](#type-string)` — display value to show in the editor.

---
## Method: FormItem.transformInput

### Description
Called when a FormItem's value is about to change as the result of user interaction. This method fires after the user performed an action that would change the value of this field, and allows the developer to modify / reformat the value before it gets validated / saved. Fires before [FormItem.change](#method-formitemchange).

Return the reformatted value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | the managing DynamicForm instance |
| item | [FormItem](#type-formitem) | false | — | the form item itself (also available as "this") |
| value | [Any](#type-any) | false | — | The new value of the form item |
| oldValue | [Any](#type-any) | false | — | The previous (current) value of the form item |

### Returns

`[Any](#type-any)` — The desired new value for the form item

---
## Method: FormItem.itemHover

### Description
Optional stringMethod to fire when the user hovers over this item. Return false to suppress default behavior of showing a hover canvas containing the HTML returned by `formItem.itemHoverHTML()` / `form.itemHoverHTML()`.

If [FormItem.canHover](#attr-formitemcanhover) is set to false, this method is not called.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | Pointer to this item |
| form | [DynamicForm](#type-dynamicform) | false | — | This items form |

### Groups

- Hovers

### See Also

- [FormItem.titleHover](#method-formitemtitlehover)
- [FormItem.itemHoverHTML](#method-formitemitemhoverhtml)

**Flags**: A

---
## Method: FormItem.isInGrid

### Description
Returns true if this item's [containerWidget](#attr-formitemcontainerwidget) is a [GridRenderer](GridRenderer.md#class-gridrenderer) or GridRenderer subclass

### Returns

`[Boolean](#type-boolean)` — whether the item's container is a GridRenderer (and thus ultimately a ListGrid)

---
## Method: FormItem.getPrintValueIcon

### Description
If implemented, this stringMethod is called when [printing](../kb_topics/printing.md#kb-topic-printing) to obtain the image source for an icon to be displayed for the current form item value. The special value "blank" means that no image will be displayed.

Implementing `getPrintValueIcon()` may be useful in order to swap out the value icon with a more printer-friendly image (perhaps a grayscale-only image). Another use is to avoid spriting when printing. Value icon spriting may be problematic when printing because browsers typically default to not printing background images.

Takes precedence over [FormItem.valueIcons](#attr-formitemvalueicons) and [FormItem.getValueIcon](#method-formitemgetvalueicon) when printing.

The returned [SCImgURL](../reference.md#type-scimgurl), if not `null` or "blank", will be suffixed with [FormItem.imageURLSuffix](#attr-formitemimageurlsuffix).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | value of the item. |

### Returns

`[SCImgURL](../reference.md#type-scimgurl)` — the image source or `null` if no value icon should be displayed.

### Groups

- valueIcons
- printing

### See Also

- [FormItem.getValueIcon](#method-formitemgetvalueicon)

---
## Method: FormItem.getListGrid

### Description
If this item is being used to edit cells in a ListGrid (see [FormItem.isInGrid](#method-formitemisingrid)), this method returns the grid in question.

### Returns

`[ListGrid](#type-listgrid)` — For listGrid edit items, the listGrid containing the item. Will return null for items that are edit items of a listGrid.

---
## Method: FormItem.setHintStyle

### Description
Set the hintStyle for this item

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| hintStyle | [CSSStyleName](../reference.md#type-cssstylename) | false | — | new style for hint text |

---
## Method: FormItem.valueIconClick

### Description
Notification method fires when the user clicks a [value icon](#attr-formitemvalueicons) for this item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | the form containing this item |
| item | [FormItem](#type-formitem) | false | — | the FormItem containing the valueIcon |
| value | [Any](#type-any) | false | — | the current value of the item. |

### Returns

`[Boolean](#type-boolean)` — Return false to suppress standard click handling for the item.

---
## Method: FormItem.shouldStopKeyPressBubbling

### Description
Should some keypress event on this item be prevented from bubbling (such that the containing form and ancestors do not receive the event).

This method is called after standard item keypress handlers when the user presses a key while focused in this item. Returning true will suppress bubbling of the event to the containing form. This is useful to avoid having the form react to key events which "have meaning" to the focused item.

Default implementation varies by item type. In short character keys are suppressed for all editable fields, as are keys which will modify the current state of the field ("Arrow" keys for moving around free form text editors, etc).

Developers may override this method to allow the form to react to certain keypresses, for example allowing scrolling of the form when the user presses the arrow keys, but they should be aware that doing so could lead to confusing user experience if the keypress will also move the position of the caret within a text box (say). Note that when this method returns true, no [keyPress](Canvas.md#method-canvaskeypress) event will fire on the form for the key pressed. However developers will still receive the separate [DynamicForm.itemKeyPress](DynamicForm.md#method-dynamicformitemkeypress) event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| keyName | [KeyName](../reference_2.md#type-keyname) | false | — | name of the key pressed |
| characterValue | [number](#type-number) | false | — | If this was a character key, this is the numeric value for the character |

### Returns

`[Boolean](#type-boolean)` — return true to prevent bubbling of the pressed key.

**Flags**: A

---
## Method: FormItem.applyFormula

### Description
Manually sets this FormItem to the result of [FormItem.formula](#attr-formitemformula) or [FormItem.textFormula](#attr-formitemtextformula). Formulas are normally automatically recomputed and the result automatically applied to the FormItem according to the rules described under [FormItem.formula](#attr-formitemformula). `applyFormula()` exists to cover any rare cases where these rules are not correct.

Calling `applyFormula()` has no effect if no [FormItem.formula](#attr-formitemformula) or [FormItem.textFormula](#attr-formitemtextformula) is configured for this FormItem.

---
## Method: FormItem.getTitle

### Description
Returns the title HTML for this item.

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — title for the formItem

### Groups

- drawing

**Flags**: A

---
## Method: FormItem.itemHoverHTML

### Description
If defined, this method should return the HTML to display in a hover canvas when the user holds the mousepointer over this item. Return null to suppress the hover canvas altogether.

If not defined, `dynamicForm.itemHoverHTML()` will be evaluated to determine hover content instead.

**Note:** When customized on the item or form, this method takes priority over [FormItem.valueHoverHTML](#method-formitemvaluehoverhtml) for hovers over the value/textbox area. This means that if you define `itemHoverHTML()`, it will be called for textbox hovers instead of `valueHoverHTML()`. To use `valueHoverHTML()` for textbox hovers, do not customize `itemHoverHTML()` and set [FormItem.showClippedValueOnHover](#attr-formitemshowclippedvalueonhover) to `null`.

If [FormItem.canHover](#attr-formitemcanhover) is set to false, this method is not called.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | Pointer to this item |
| form | [DynamicForm](#type-dynamicform) | false | — | This items form |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML to be displayed in the hover

### Groups

- Hovers

### See Also

- [FormItem.canHover](#attr-formitemcanhover)
- [FormItem.prompt](#attr-formitemprompt)
- [FormItem.itemHover](#method-formitemitemhover)
- [FormItem.titleHoverHTML](#method-formitemtitlehoverhtml)
- [FormItem.valueHoverHTML](#method-formitemvaluehoverhtml)

**Flags**: A

---
## Method: FormItem.getVisibleTitleWidth

### Description
Returns the visible width of this item's title in px. If that is not applicable (for example, the form item has no title) or cannot be determined (for example, the form is not drawn), returns 0.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| labelOnly | [Boolean](#type-boolean) | false | — | If true, returns the visible width of the title text only; if false (the default) returns the width of the title cell |

### Returns

`[number](#type-number)` — width of the form item's title in px

### Groups

- sizing

**Flags**: A

---
## Method: FormItem.editorEnter

### Description
Notification method fired when the user enters this formItem. Differs from [FormItem.focus](#method-formitemfocus) in that while `focus` and `blur` may fire multiple as the user navigates sub elements of an item (such as interacting with a pick list), `editorEnter` will typically fire once when the user starts to edit this item as a whole, and once when the user moves onto a different item or component

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | form containing this item |
| item | [FormItem](#type-formitem) | false | — | form item recieving focus |
| value | [Any](#type-any) | false | — | current item value. |

### Groups

- eventHandling

---
## Method: FormItem.disable

### Description
Set this item to be disabled at runtime.

### Groups

- enable

### See Also

- [FormItem.disabled](#attr-formitemdisabled)

---
## Method: FormItem.setErrors

### Description
Set the error message(s) for this item

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| errors | [String](#type-string)|[Array of String](#type-array-of-string) | false | — | error message(s) |

### Groups

- errorHandling

---
## Method: FormItem.getCanFocus

### Description
Returns true for items that can accept keyboard focus such as data items ([TextItems](TextItem.md#class-textitem), [TextAreaItems](TextAreaItem.md#class-textareaitem), etc), [CanvasItems](CanvasItem.md#class-canvasitem) with a focusable canvas, or items where [FormItem.canFocus](#attr-formitemcanfocus) was explicitly set to true.

### Returns

`[boolean](../reference.md#type-boolean)` — true if the form item is visible

### Groups

- focus

---
## Method: FormItem.getPixelHeight

### Description
Returns the specified [FormItem.height](#attr-formitemheight) of this formItem in pixels. For heights specified as a percentage value or `"*"`, the pixel height may not be available prior to the item being drawn. In cases where the height has not yet been resolved to a pixel value, this method will return `-1`.

### Returns

`[int](../reference.md#type-int)` — Specified height resolved to a pixel value.

---
## Method: FormItem.getSelectedRecord

### Description
Get the record returned from the [FormItem.optionDataSource](#attr-formitemoptiondatasource) when [fetchMissingValues](#attr-formitemfetchmissingvalues) is true, and the missing value is fetched.

[FormItem.fetchMissingValues](#attr-formitemfetchmissingvalues) kicks off the fetch when the form item is initialized with a non null value or when setValue() is called on the item. Note that this method will return null before the fetch completes, or if no record is found in the optionDataSource matching the underlying value.

### Returns

`[ListGridRecord](#type-listgridrecord)` — selected record

### Groups

- display_values

---
## Method: FormItem.shouldApplyHeightToTextBox

### Description
If [FormItem.height](#attr-formitemheight) is specified, should it be applied to the item's text box element? If this method returns false, the text box will not have an explicit height applied, though the containing cell will be sized to accommodate any specified height.

This is used in cases where the text box does not have distinctive styling (for example in standard [StaticTextItem](StaticTextItem.md#class-statictextitem)s). As the textBox has no explicit height, it fits the content. Since the text box is not visually distinct to the user, this makes [FormItem.vAlign](#attr-formitemvalign) behave as expected with the text value of the item being vertically aligned within the cell.

Default implementation will return [FormItem.applyHeightToTextBox](#attr-formitemapplyheighttotextbox) if explicitly set otherwise `false` if [FormItem.readOnlyDisplay](#attr-formitemreadonlydisplay) is set to `"static"` and the item is [not editable](#method-formitemgetcanedit), otherwise true.

### Returns

`[boolean](../reference.md#type-boolean)` — true if the height should be written into the items' text box.

**Flags**: A

---
## Method: FormItem.setLeft

### Description
For a form with [itemLayout](DynamicForm.md#attr-dynamicformitemlayout):"absolute" only, set the left coordinate of this form item.

Causes the form to redraw.

**Flags**: A

---
## Method: FormItem.getPageLeft

### Description
Returns the drawn page-left coordinate of this form item in pixels.

### Returns

`[int](../reference.md#type-int)` — page-left coordinate in px

### Groups

- positioning

---
## Method: FormItem.isDisabled

### Description
Is this item disabled?

### Returns

`[Boolean](#type-boolean)` — disabledtrue if this item is be disabled

### Groups

- enable

### See Also

- [FormItem.disabled](#attr-formitemdisabled)

**Flags**: A

---
## Method: FormItem.getPixelWidth

### Description
Returns the specified [FormItem.width](#attr-formitemwidth) of this formItem in pixels. For widths specified as a percentage value or `"*"`, the pixel width may not be available prior to the item being drawn. In cases where the width has not yet been resolved to a pixel value, this method will return `-1`.

### Returns

`[int](../reference.md#type-int)` — Specified width resolved to a pixel value.

---
## Method: FormItem.titleClick

### Description
Notification method fired when the user clicks the title for this item

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | the managing DynamicForm instance |
| item | [FormItem](#type-formitem) | false | — | the form item whose title was clicked |

### Returns

`[Boolean](#type-boolean)` — Return false to cancel the click event. This will prevent the event from bubbling up, suppressing [click](Canvas.md#method-canvasclick) on the form containing this item.

---
## Method: FormItem.setHint

### Description
Sets the [hint](#attr-formitemhint) for this item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newHint | [HTMLString](../reference.md#type-htmlstring) | false | — | new hint for the item. |

---
## Method: FormItem.getDisplayFieldName

### Description
Returns the `displayField` for this item.

Behavior varies based on the configuration of this item, as follows:

*   If this item has an [FormItem.optionDataSource](#attr-formitemoptiondatasource) and an explicit [FormItem.foreignDisplayField](#attr-formitemforeigndisplayfield) is specified, this will be returned.
*   Otherwise if an explicit [FormItem.displayField](#attr-formitemdisplayfield) is specified it will be returned by default. If the `displayField` was specified on the underlying dataSource field, and no matching field is present in the [FormItem.optionDataSource](#attr-formitemoptiondatasource) for the item, we avoid returning the specified displayField value and instead return the title field of the option DataSource. We do this to avoid confusion for the case where the displayField is intended as a display-field value for showing another field value within the same record in the underlying dataSource only.
*   If no explicit foreignDisplay or displayField specification was found, and the [FormItem.valueField](#attr-formitemvaluefield) for this item is hidden in the [FormItem.optionDataSource](#attr-formitemoptiondatasource), this method will return the title field for the `optionDataSource`.

### Returns

`[FieldName](../reference.md#type-fieldname)` — display field name, or null if there is no separate display field to use.

---
## Method: FormItem.redraw

### Description
Redraw this form item.

Depending on the item and the [FormItem.containerWidget](#attr-formitemcontainerwidget) it's embedded in, this may redraw this particular item or require a redraw of all items in the form.

Do not call this method unless the documentation directs you to do so. Calling `redraw()` unnecessarily has significant performance consequences.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| reason | [String](#type-string) | true | — | optional reason for performing the redraw, which may appear in diagnostic logs if enabled |

---
## Method: FormItem.setShowDisabled

### Description
Setter method for [FormItem.showDisabled](#attr-formitemshowdisabled)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showDisabled | [boolean](../reference.md#type-boolean) | false | — | new showDisabled setting |

---
## Method: FormItem.setPrompt

### Description
Sets the [prompt](#attr-formitemprompt) for this item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newPrompt | [HTMLString](../reference.md#type-htmlstring) | false | — | new prompt for the item. |

---
## Method: FormItem.shouldSaveOnEnter

### Description
Returns true if 'Enter' key presses in this formItem should allow a saveOnEnter: true parent form to save it's data. The default implementation returns the value of [FormItem.saveOnEnter](#attr-formitemsaveonenter) or false if that property is unset.

### Returns

`[Boolean](#type-boolean)` — boolean indicating whether saving should be allowed to proceed

**Flags**: A

---
## Method: FormItem.getCursorPosition

### Description
For text-based items, this method returns the index of the start of the current selection if the item currently has the focus (if no text is selected, this equates to the current position of the text editing cursor). See [TextItem.getSelectionRange](TextItem.md#method-textitemgetselectionrange) for details of what is returned if the item does not have the focus (note, it is important to read this documentation, because the behavior when the item does not have the focus varies by browser)

### Returns

`[Integer](../reference_2.md#type-integer)` — Index of the current or past selection's start point

---
## Method: FormItem.getCustomState

### Description
Optional method to retrieve a custom state suffix to append to the style name that is applied to some element of a formItem - see [FormItemBaseStyle](../reference_2.md#type-formitembasestyle) for more information on how state-based FormItem style names are derived.

If this method exists on a formItem, the framework will call it, passing in the state suffix it has derived. Your `getCustomState()` implementation can make use of this derived state or ignore it. For example, if you wanted two different types of focus styling depending on some factor unrelated to focus, you would probably make use of the incoming "Focused" state and return something like "Focused1" or "Focused2". On the other hand, if you want your custom state to just override whatever the system derived, you would ignore the incoming state. Finally, if you do not wish to provide a custom style for this formItem element at this time - for example, you are only interested in providing a custom "textBox" style and this call is for a "cell" element type - your `getCustomStyle()` method should just return the state it was passed.

This method is an advanced API, and you should only provide an implementation of it if you have specialized styling requirements. If you do implement it, note that it will be called very frequently, from rendering code: if your custom logic does significant processing, it could introduce a system-wide performance problem.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| elementType | [FormItemElementType](../reference.md#type-formitemelementtype) | false | — | The element type to return a custom state for |
| derivedState | [String](#type-string) | false | — | The state suffix the system derived |

### Returns

`[String](#type-string)` — custom state suffix to use for the parameter elementType for this FormItem

### See Also

- [FormItemBaseStyle](../reference_2.md#type-formitembasestyle)

**Flags**: A

---
## Method: FormItem.pickerIconClick

### Description
Notification method called when the [picker icon](#attr-formitemshowpickericon) is clicked. This method will fire after the [FormItemIcon.click](FormItemIcon.md#method-formitemiconclick) handler for the [pickerIcon](#attr-formitempickericonproperties). If the event is not cancelled, the standard [FormItem.iconClick](#method-formitemiconclick) will also fire.

The default implementation will call [FormItem.showPicker](#method-formitemshowpicker).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | the DynamicForm containing the picker icon's item. |
| item | [FormItem](#type-formitem) | false | — | the FormItem containing the picker icon. |
| pickerIcon | [FormItemIcon](#type-formitemicon) | false | — | the picker icon. |

### Returns

`[Boolean](#type-boolean)` — Return false to cancel the event.

### Groups

- pickerIcon

---
## Method: FormItem.getVisibleHeight

### Description
Output the drawn height for this item in pixels. Note: this is only reliable after this item has been written out into the DOM.

### Returns

`[Integer](../reference_2.md#type-integer)` — height of the form item

### Groups

- sizing

**Flags**: A

---
## Method: FormItem.enable

### Description
Set this item to be enabled at runtime.

### Groups

- enable

### See Also

- [FormItem.disabled](#attr-formitemdisabled)

---
## Method: FormItem.getErrors

### Description
Return the validation errors in the form associated with this item, if any. Errors will be returned as either a string (single error message) or an array of strings (multiple error messages).

### Returns

`[String](#type-string)|[Array of String](#type-array-of-string)` — Error message(s) for this item.

### Groups

- errors

**Flags**: A

---
## Method: FormItem.getValue

### Description
Return the value tracked by this form item.

Note that for FormItems that have a [ValueMap](../reference_2.md#type-valuemap) or where a [formatter](#method-formitemformatvalue) has been defined, `getValue()` returns the underlying value of the FormItem, not the displayed value.

### Returns

`[Any](#type-any)` — value of this element

### Groups

- formValues

---
## Method: FormItem.defaultDynamicValue

### Description
Expression evaluated to determine the [FormItem.defaultValue](#attr-formitemdefaultvalue) when no value is provided for this item.

_formItem.defaultDynamicValue_ may be specified as a method or [sting of script](../reference_2.md#type-stringmethod) to evaluate. It should return a calculated default value for the item.

If you don't need dynamic evaluation, you can just use `item.defaultValue`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | the form item itself (also available as "this") |
| form | [DynamicForm](#type-dynamicform) | false | — | the managing DynamicForm instance |
| values | [Object](../reference.md#type-object) | false | — | the current set of values for the form as a whole |

### Returns

`[Any](#type-any)` — dynamically calculated default value for this item

### Groups

- formValues

### See Also

- [FormItem.defaultValue](#attr-formitemdefaultvalue)

**Flags**: A

---
## Method: FormItem.setValueByDisplayValue

### Description
Sets the form item's value by looking up the corresponding data value from a display value using a series of fallback strategies.

The lookup proceeds through the following steps, stopping as soon as a mapping is found:

1.  **valueMap/cache**: Checks if the display value maps to a data value via [FormItem.mapDisplayToValue](#method-formitemmapdisplaytovalue), which consults the [FormItem.valueMap](#attr-formitemvaluemap) and [FormItem.optionDataSource](#attr-formitemoptiondatasource) cache
2.  **optionDataSource fetch**: If [FormItem.optionDataSource](#attr-formitemoptiondatasource) is configured with [FormItem.displayField](#attr-formitemdisplayfield) and [FormItem.valueField](#attr-formitemvaluefield), fetches from the server to find a matching record
3.  **parseEditorValue**: If [FormItem.parseEditorValue](#method-formitemparseeditorvalue) is defined, calls it to transform the display value
4.  **identity**: As a final fallback, assumes the display value and data value are the same, and uses the display value directly

This method is asynchronous when fetching from the optionDataSource. Use the callback parameter to be notified when the operation completes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| displayValue | [Any](#type-any) | false | — | The display value to look up |
| callback | [SetValueByDisplayValueCallback](#type-setvaluebydisplayvaluecallback) | true | — | Callback fired when the operation completes |

---
## Method: FormItem.hasAdvancedCriteria

### Description
Does this form item produce an [AdvancedCriteria](../reference.md#object-advancedcriteria) sub criterion object? If this method returns true, [DynamicForm.getValuesAsCriteria](DynamicForm.md#method-dynamicformgetvaluesascriteria) on the form containing this item will always return an [AdvancedCriteria](../reference.md#object-advancedcriteria) object, calling [FormItem.getCriterion](#method-formitemgetcriterion) on each item to retrieve the individual criteria.

Default implementation will return `true` if [FormItem.operator](#attr-formitemoperator) is explicitly specified.

### Returns

`[Boolean](#type-boolean)` — true if this item will return an AdvancedCriteria sub-criterion.

### Groups

- criteriaEditing

---
## Method: FormItem.getPickerIconTabPosition

### Description
Returns the desired tab-position of the picker icon with respect to other focusable sub-elements for this formItem.

Default implementation returns zero, making the picker the first focusable element after the items text box.

### Returns

`[Integer](../reference_2.md#type-integer)` — desired position in the tab-order within this item's sub-elements

---
## Method: FormItem.change

### Description
Called when a FormItem's value is about to change as the result of user interaction. This method fires after the user performed an action that would change the value of this field, but before the element itself is changed.

Returning false cancels the change. Note that if what you want to do is **transform** the user's input, for example, automatically change separator characters to a standard separator character, you should implement [transformInput](#method-formitemtransforminput) rather than using a combination of change() and setValue() to accomplish the same thing. Returning false from `change` is intended for rejecting input entirely, such as typing invalid characters.

Note that if you ask the form for the current value in this handler, you will get the old value because the change has not yet been committed. The new value is available as a parameter to this method.

Change/Changed notifications vs _"...When"_ rules: the `change` and `changed` events only fire when an end user modifies a field value. If you are trying to dynamically control the visibility or enabled state of other components in response to these events, consider instead using properties such as [Canvas.visibleWhen](Canvas.md#attr-canvasvisiblewhen), [item.readOnlyWhen](#attr-formitemreadonlywhen), [Canvas.enableWhen](Canvas.md#attr-canvasenablewhen) on the target component. (Similar properties are available on [FormItem](#class-formitem), [Canvas](Canvas.md#class-canvas), [MenuItem](../reference_2.md#object-menuitem) and other components).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | the managing DynamicForm instance |
| item | [FormItem](#type-formitem) | false | — | the form item itself (also available as "this") |
| value | [Any](#type-any) | false | — | The new value of the form item |
| oldValue | [Any](#type-any) | false | — | The previous value of the form item |

### Returns

`[Boolean](#type-boolean)` — In your handler, return false to cancel the change, true or null to allow the change

### Groups

- eventHandling

---
## Method: FormItem.getRect

### Description
Return the coordinates of this object as a 4 element array.

### Returns

`[Array](#type-array)` — \[left, top, width, height\]

### Groups

- positioning
- sizing

---
## Method: FormItem.getIconWidth

### Description
Takes an icon definition object, and returns the width for that icon in px.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [Object](../reference.md#type-object) | false | — | icon definition object for this item. |

### Returns

`[int](../reference.md#type-int)` — width of the form item icon in px

### Groups

- sizing

**Flags**: A

---
## Method: FormItem.setIconDisabled

### Description
Set an icon as enabled or disabled at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [Identifier](../reference.md#type-identifier) | false | — | [name](FormItemIcon.md#attr-formitemiconname) of the icon to be disabled/enabled. |
| disabled | [boolean](../reference.md#type-boolean) | false | — | true if icon should be disabled |

### Groups

- enable

### See Also

- [FormItemIcon.disabled](FormItemIcon.md#attr-formitemicondisabled)

**Flags**: A

---
## Method: FormItem.blurItem

### Description
Takes focus from this form item's focusable element.

### Groups

- eventHandling
- focus

---
## Method: FormItem.showIcon

### Description
This method will show some icon in this item's [FormItem.icons](#attr-formitemicons) array, if it is not already visible. Note that once this method has been called, any previously specified [FormItemIcon.showIf](FormItemIcon.md#method-formitemiconshowif) will be discarded.

Note that if the form item's showIcons property is set to false, no icons will be displayed for the item. In this case this method will not cause the icon to be displayed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [Identifier](../reference.md#type-identifier) | false | — | [name](FormItemIcon.md#attr-formitemiconname) of the icon to be shown. |

---
## Method: FormItem.getValueAsInteger

### Description
Return the value tracked by this form item as an Integer. If the value cannot be parsed to an int that matches the original value, null will be returned.

### Returns

`[Integer](../reference_2.md#type-integer)` — value of this element

### See Also

- [FormItem.getValue](#method-formitemgetvalue)

---
## Method: FormItem.showPicker

### Description
Method to show a picker for this item. By default this method is called if the user clicks on a [pickerIcon](#attr-formitemshowpickericon). May also be called programmatically.

Default implementation lazily creates and shows the [Picker Autochild](#attr-formitempicker).

Developers wishing to show a custom picker widget can either implement a [FormItem.pickerIconClick](#method-formitempickericonclick) handler with an entirely custom implementation (and bypass the call to `showPicker()` altogether), override this method, or use the [AutoChild pattern](../reference.md#type-autochild) to customize the automatically generated [picker autoChild](#attr-formitempicker).

**Flags**: A

---
## Method: FormItem.clearValue

### Description
Clear the value for this form item.

Note that if a default value is specified, value will be set to that default value, otherwise value will be cleared, (and removed from the containing form's values).

---
## Method: FormItem.setRequired

### Description
Setter to mark this formItem as [FormItem.required](#attr-formitemrequired), or not required at runtime. Note that an alternative approach to updating the `required` flag directly would be to simply use a [requiredIf](../reference.md#type-validatortype) type validator.

Note that this method will not re-validate this item by default or clear any existing validation errors. If desired, this may be achieved by calling [FormItem.validate](#method-formitemvalidate) or [DynamicForm.clearErrors](DynamicForm.md#method-dynamicformclearerrors).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| required | [boolean](../reference.md#type-boolean) | false | — | new [FormItem.required](#attr-formitemrequired) value. |

---
## Method: FormItem.hasErrors

### Description
Return whether this item currently has any validation errors as a result of a previous validation pass.

### Returns

`[boolean](../reference.md#type-boolean)` — true == item currently has validation errors.

### Groups

- errorHandling

---
## Method: FormItem.getPrintValueIconStyle

### Description
If implemented, this method is called when [printing](../kb_topics/printing.md#kb-topic-printing) to obtain the base CSS style to use on the [print value icon](#method-formitemgetprintvalueicon) for the item's current value.

If not `null`, the base style is suffixed with the state of the value icon ("", "Over", "Down", "Disabled").

NOTE: It is not recommended to apply CSS `background-image` styling to the value icon style. This is because browsers typically default to not printing background images.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | value of this item. |

### Returns

`[CSSStyleName](../reference.md#type-cssstylename)` — CSS style to use, or `null` if no style should be used.

### Groups

- printing

### See Also

- [FormItem.getValueIconStyle](#method-formitemgetvalueiconstyle)

**Flags**: A

---
## Method: FormItem.getCanEdit

### Description
Is this form item editable or read-only?

This setting differs from the enabled/disabled state in that most form items will allow copying of the contents while read-only but do not while disabled.

**Important note:** this method is not intended as an override point to make an item conditionally read-only. It is not called at the appropriate times to serve as a dynamic control over editability. Developers may instead use [readOnlyWhen rules](#attr-formitemreadonlywhen) to dynamically control editability of items.

### Returns

`[boolean](../reference.md#type-boolean)` — true if editable

### Groups

- readOnly

---
## Method: FormItem.enableIcon

### Description
This method will enable some icon in this item's [FormItem.icons](#attr-formitemicons) array, if it is currently disabled.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [Identifier](../reference.md#type-identifier) | false | — | [name](FormItemIcon.md#attr-formitemiconname) of the icon to be enabled. |

### Groups

- enable

### See Also

- [FormItemIcon.disabled](FormItemIcon.md#attr-formitemicondisabled)

---
## Method: FormItem.mapValueToDisplay

### Description
Given a value for this FormItem, return the value to be displayed.

This method is called by the framework to derive a display value for a given data value in a FormItem. Your own code can call this method if you need to programmatically obtain the display value (for example, to display in a hover prompt or error message). However, it is **not** intended as an override point, and you should not treat it as one. There are several supported ways to apply custom formatting to your form values:

*   If you want to apply a consistent custom format to every instance of a given [SimpleType](SimpleType.md#class-simpletype), specify a [format](SimpleType.md#attr-simpletypeformat) on the SimpleType. This is the most general approach. Note, this is a static formatter: it will only affect the format of values the user can interact with if [TextItem.formatOnBlur](TextItem.md#attr-textitemformatonblur) is set
*   If you want to apply a consistent custom format to a [DataSource-described field](../reference_2.md#object-datasourcefield), the best approach is [DataSourceField.format](DataSourceField.md#attr-datasourcefieldformat). This overrides SimpleType-level formatting and, again, is static formatting
*   For a FormItem that is not DataSource-described, or for special formats that should only be used on a particular form, [format](#attr-formitemformat) can also be declared for individual FormItems. This overrides DataSource-level formatting
*   For temporal values, you can declare [dateFormatter](#attr-formitemdateformatter) and [timeFormatter](#attr-formitemtimeformatter) at both `FormItem` and [DynamicForm](DynamicForm.md#class-dynamicform) levels. Generally, however, we recommend the generic declarative [format](#attr-formitemformat) as the simpler approach
*   If you want to apply a specialized format that cannot be expressed declaratively, use [formatValue()](#method-formitemformatvalue) for static-valued items like [StaticTextItem](StaticTextItem.md#class-statictextitem) or [SelectItem](SelectItem.md#class-selectitem), and [formatEditorValue()](#method-formitemformateditorvalue) for other types of FormItem

#### Deriving the display value
The process of deriving a display value from a data value involves the following steps:

*   If the item declares a [valueMap](#attr-formitemvaluemap), the display value is derived by looking up the value in the valueMap
*   If the item does not have a valueMap - or the value was not found in the item's valueMap - and the item declares a [displayField](#attr-formitemdisplayfield) and an [optionDataSource](#attr-formitemoptiondatasource), the display value is derived by looking up the "displayField" corresponding to the value in the optionDataSource's local cache
*   Formatting is now applied to the derived display value. Note, it is perfectly normal at this point for no display value has to be derived - this will be the case for any field with no `valueMap` and no `optionDataSource`. In this case, the passed-in value is treated as the display value for all further purposes.
    *   If the FormItem involves static display value(s), like [StaticTextItem](StaticTextItem.md#class-statictextitem) or [SelectItem](SelectItem.md#class-selectitem)
        *   If the FormItem has a [formatValue()](#method-formitemformatvalue) method, it is called
        *   Otherwise, if the formItem declares a [format](#attr-formitemformat), the formst is applied in line with the rules of [FormatString](../reference.md#type-formatstring)
        *   Otherwise, if the FormItem is of a [SimpleType](SimpleType.md#class-simpletype) that declares a [format](SimpleType.md#attr-simpletypeformat), the format is applied
    *   Otherwise, if the FormItem has a [formatEditorValue()](#method-formitemformateditorvalue) method, it is called
    *   Otherwise, if the FormItem is of a [SimpleType](SimpleType.md#class-simpletype) that declares an [editFormatter()](SimpleType.md#method-simpletypeeditformatter), the edit formatter is called
    *   Otherwise, if the value is a Date:
        *   If the formItem declares a [timeFormatter](#attr-formitemtimeformatter) and no [dateFormatter](#attr-formitemdateformatter), the timeFormatter is called
        *   Otherwise, if the formItem is of a [SimpleType](SimpleType.md#class-simpletype) that [inheritsFrom](SimpleType.md#attr-simpletypeinheritsfrom) "time", the value is formatted using the [default time format](Time.md#classattr-timeshortdisplayformat)
        *   Otherwise, the date or datetime is formatted using the rules described for [FormItem.dateFormatter](#attr-formitemdateformatter).
    *   Otherwise, if the FormItem involves static display value(s) and is of a `SimpleType` that declares a [normalDisplayFormatter](SimpleType.md#method-simpletypenormaldisplayformatter), this is used
    *   Otherwise, if the value is not null and is of a "simple" type (ie, it is not an object or an array), a display value is derived by calling the Javascript `toLocaleString()` method, if the value has one, or the `toString()` method if it does not
    *   Otherwise, if the value is null or a zero-length string, the display value is set to the formItem's [emptyDisplayValue](#attr-formitememptydisplayvalue)
    *   Otherwise, the "display value" is the simple, unformatted data value that was passed in

#### Treatment of arrays
Ordinarily, arrays are treated like any other value. This means you can, for example, create a [formatEditorValue()](#method-formitemformateditorvalue) implementation that is capable of formatting an array-valued field in some way that makes sense for the particular application domain.

However, for items that are marked to handle [multiple](DataSourceField.md#attr-datasourcefieldmultiple) values, array values are treated differently. In this case, the display value is built up by calling `mapValueToDisplay()` recursively for each array entry, and concatenating these partial display values together using the [multipleValueSeparator](#attr-formitemmultiplevalueseparator).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | value to be mapped to a display value |

### Returns

`[String](#type-string)` — value to display. Note, for items with static value(s), such as [SelectItem](SelectItem.md#class-selectitem) or [StaticTextItem](StaticTextItem.md#class-statictextitem), the display value string will be interpreted as HTML by the browser. See [SelectItem.escapeHTML](SelectItem.md#attr-selectitemescapehtml) for more details

### See Also

- [FormItem.mapDisplayToValue](#method-formitemmapdisplaytovalue)

---
## Method: FormItem.getErrorHTML

### Description
Output the HTML for an error message in a form element. Default behavior respects [FormItem.showErrorIcon](#attr-formitemshowerroricon) and [FormItem.showErrorText](#attr-formitemshowerrortext) as described in the documentation for those attributes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| error | [String](#type-string)|[Array of String](#type-array-of-string) | false | — | error message string or array of error messages |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML to display the error

**Flags**: A

---
## Method: FormItem.editorExit

### Description
Notification method fired when the user leaves this formItem. Differs from [FormItem.blur](#method-formitemblur) in that while `focus` and `blur` may fire multiple as the user navigates sub elements of an item (such as interacting with a pick list), `editorEnter` will typically fire once when the user starts to edit this item as a whole, and `editorExit` fires once when the user moves onto a different item or component

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | form managing this form item |
| item | [FormItem](#type-formitem) | false | — | pointer to the form item being managed |
| value | [Any](#type-any) | false | — | current value of the form item |

### Groups

- eventHandling

---
## Method: FormItem.clearErrors

### Description
Clear all error messages for this item

### Groups

- errorHandling

---
## Method: FormItem.setOptionDataSource

### Description
Method to set the [FormItem.optionDataSource](#attr-formitemoptiondatasource) at runtime

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataSource | [DataSource](#type-datasource) | false | — | new optionDatasource |

**Flags**: A

---
## Method: FormItem.setValueMap

### Description
Set the valueMap for this item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| valueMap | [Array](#type-array)|[Object](../reference.md#type-object) | false | — | new valueMap |

### Groups

- valueMap

### See Also

- [FormItem.valueMap](#attr-formitemvaluemap)

**Flags**: A

---
## Method: FormItem.titleHover

### Description
Optional stringMethod to fire when the user hovers over this item's title. Return false to suppress default behavior of showing a hover canvas containing the HTML returned by `formItem.titleHoverHTML()` / `form.titleHoverHTML()`.

If [FormItem.canHover](#attr-formitemcanhover) is set to false, this method is not called.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | Pointer to this item |
| form | [DynamicForm](#type-dynamicform) | false | — | This items form |

### Groups

- Hovers

### See Also

- [FormItem.itemHover](#method-formitemitemhover)
- [FormItem.titleHoverHTML](#method-formitemtitlehoverhtml)

**Flags**: A

---
## Method: FormItem.updateState

### Description
Update the visual state of a FormItem to reflect any changes in state or any changes in style settings (e.g. [FormItem.textBoxStyle](#attr-formitemtextboxstyle)).

Calls to `updateState()` normally occur automatically as a consequence of focus changes, items becoming disabled, etc. This method is advanced and intended only for use in workarounds.

**Flags**: A

---
## Method: FormItem.storeValue

### Description
Store (and optionally show) a value for this form item.

This method will fire standard [FormItem.change](#method-formitemchange) and [DynamicForm.itemChanged](DynamicForm.md#method-dynamicformitemchanged) handlers, and store the value passed in such that subsequent calls to [FormItem.getValue](#method-formitemgetvalue) or [DynamicForm.getValue](DynamicForm.md#method-dynamicformgetvalue) will return the new value for this item.

This method is intended to provide a way for custom formItems - most commonly [canvasItems](CanvasItem.md#class-canvasitem) - to provide a new interface to the user, allowing them to manipulate the item's value, for example in an embedded [CanvasItem.canvas](CanvasItem.md#attr-canvasitemcanvas), or a pop-up dialog launched from an [icon](../reference.md#object-formitemicon), etc. Developers should call this method when the user interacts with this custom interface in order to store the changed value.

[shouldSaveValue](CanvasItem.md#attr-canvasitemshouldsavevalue) for CanvasItems is false by default. Custom CanvasItems will need to override shouldSaveValue to true if the values stored via this API should be included in the form's [getValues()](DynamicForm.md#method-dynamicformgetvalues) and saved with the form when [saveData()](DynamicForm.md#method-dynamicformsavedata) is called.

If you cannot easily detect interactions that should change the value as the user performs them, a workaround is to call `storeValue` right before the form saves.

Note that this method is not designed for customizing a value which is already being saved by a standard user interaction. For example you should not call this method from a [change handler](#method-formitemchange). Other APIs such as [FormItem.transformInput](#method-formitemtransforminput) exist for this.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | value to save for this item |
| showValue | [Boolean](#type-boolean) | true | — | Should the formItem be updated to display the new value? |

---
## Method: FormItem.getValueIconStyle

### Description
Except when [printing](../kb_topics/printing.md#kb-topic-printing) and [getPrintValueIconStyle()](#method-formitemgetprintvalueiconstyle) is implemented, this method is called to obtain the base CSS style to use on the [value icon](#method-formitemgetvalueicon) for the item's current value.

If not `null`, the base style is suffixed with the state of the value icon ("", "Over", "Down", "Disabled").

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | value of this item. |

### Returns

`[CSSStyleName](../reference.md#type-cssstylename)` — CSS style to use, or `null` if no style should be used.

### See Also

- [FormItem.getPrintValueIconStyle](#method-formitemgetprintvalueiconstyle)

**Flags**: A

---
## Method: FormItem.setCellStyle

### Description
Setter for [FormItem.cellStyle](#attr-formitemcellstyle).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newCellStyle | [FormItemBaseStyle](../reference_2.md#type-formitembasestyle) | false | — | the new `cellStyle` value. |

### Groups

- appearance

---
## Method: FormItem.isFocused

### Description
Returns true if this formItem has the keyboard focus. Note that in Internet Explorer focus notifications can be asynchronous (see [EventHandler.synchronousFocusNotifications](EventHandler.md#classattr-eventhandlersynchronousfocusnotifications)). In this case, this method can correctly return false when, intuitively, you would expect it to return true:
```
     someItem.focusInItem();
     if (someItem.isFocused()) {
         // In most browsers we would get here, but not in Internet Explorer with
         // EventHandler.synchronousFocusNotifications disabled
     }
 
```

### Returns

`[Boolean](#type-boolean)` — whether this formItem has the keyboard focus

---
## Method: FormItem.getVAlign

### Description
Returns the vertical-alignment for this item within its cell. By default, when [titleOrientation](#attr-formitemtitleorientation) is "top", this method will return "top", so that items of varying height are top-aligned, beneath their titles.

### Returns

`[VerticalAlignment](../reference.md#type-verticalalignment)` — vertical alignment for this item

---
## Method: FormItem.click

### Description
Called when this FormItem is clicked on.

Note: `click()` is available on StaticTextItem, BlurbItems, ButtonItem, and derivatives. Other form items (such as HiddenItem) do not support `click()`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | true | — | the managing DynamicForm instance |
| item | [FormItem](#type-formitem) | true | — | the form item itself (also available as "this") |

### Returns

`[Boolean](#type-boolean)` — Return false to cancel the click event. This will prevent the event from bubbling up, suppressing [click](Canvas.md#method-canvasclick) on the form containing this item.

### Groups

- eventHandling

---
## Method: FormItem.isVisible

### Description
Return true if the form item is currently visible. Note that like the similar [Canvas API](Canvas.md#method-canvasisvisible), it indicates visibility settings only and so will return true for an item that is not drawn.

### Returns

`[Boolean](#type-boolean)` — true if the form item is visible

### Groups

- visibility

---
## Method: FormItem.isPasteEvent

### Description
Is the user performing a native "paste" event to modify the value of a freeform text field? This method may be invoked during change notification flow methods including [FormItem.change](#method-formitemchange), [FormItem.changed](#method-formitemchanged) and [FormItem.transformInput](#method-formitemtransforminput). See [FormItem.supportsCutPasteEvents](#attr-formitemsupportscutpasteevents).

### Returns

`[boolean](../reference.md#type-boolean)` — true if this is a cut event.

---
## Method: FormItem.getOptionDataSource

### Description
Returns the [FormItem.optionDataSource](#attr-formitemoptiondatasource) for this item.

Always uses `item.optionDataSource` if specified. Otherwise, if [DataSourceField.foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) was specified, uses the target DataSource. Otherwise, uses the DataSource of this item's form (if one is configured).

### Returns

`[DataSource](#type-datasource)` — the optionDataSource, or null if none is configured

### Groups

- display_values

---
## Method: FormItem.pendingStatusChanged

### Description
Notification method called when [showPending](#attr-formitemshowpending) is enabled and this form item should either clear or show its "Pending" visual state.

The default behavior is that the [titleStyle](#attr-formitemtitlestyle) and [cellStyle](#attr-formitemcellstyle) are updated to include/exclude the "Pending" suffix. Standard form item types may implement additional default behavior (see any item-specific pendingStatusChanged() documentation). Returning `false` will cancel the default behavior.

The pendingStatusChanged() notification method is typically used by [CanvasItem](CanvasItem.md#class-canvasitem)-derived form items, where a custom or supplemental pending visual state is desired.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | the managing `DynamicForm` instance. |
| item | [FormItem](#type-formitem) | false | — | the form item itself (also available as "this"). |
| pendingStatus | [boolean](../reference.md#type-boolean) | false | — | `true` if the item should show its pending visual state; `false` otherwise. |
| newValue | [Any](#type-any) | false | — | the current form item value. |
| value | [Any](#type-any) | false | — | the value that would be restored by a call to [DynamicForm.resetValues](DynamicForm.md#method-dynamicformresetvalues). |

### Returns

`[Boolean](#type-boolean)` — `false` to cancel the default behavior.

**Flags**: A

---
## Method: FormItem.isCutEvent

### Description
Is the user performing a native "cut" event to modify the value of a freeform text field? This method may be invoked during change notification flow methods including [FormItem.change](#method-formitemchange), [FormItem.changed](#method-formitemchanged) and [FormItem.transformInput](#method-formitemtransforminput). See [FormItem.supportsCutPasteEvents](#attr-formitemsupportscutpasteevents).

### Returns

`[boolean](../reference.md#type-boolean)` — true if this is a cut event.

---
## Method: FormItem.getValueFieldName

### Description
Getter method to retrieve the [FormItem.valueField](#attr-formitemvaluefield) for this item. For items with a specified [FormItem.optionDataSource](#attr-formitemoptiondatasource), this determines which field in that dataSource corresponds to the value for this item.

If unset, if a [foreignKey relationship](DataSourceField.md#attr-datasourcefieldforeignkey) exists between this field and the optionDataSource, this will be used, otherwise default behavior will return the [FormItem.name](#attr-formitemname) of this field.

### Returns

`[String](#type-string)` — fieldName to use a "value field" in records from this items [FormItem.optionDataSource](#attr-formitemoptiondatasource)

### Groups

- display_values

---
## Method: FormItem.getIcon

### Description
Given a [FormItemIcon.name](FormItemIcon.md#attr-formitemiconname), returns the `FormItemIcon` object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [Identifier](../reference.md#type-identifier) | false | — | specified [FormItemIcon.name](FormItemIcon.md#attr-formitemiconname) |

### Returns

`[FormItemIcon](#type-formitemicon)` — form item icon matching the specified name, or `null` if there is no such icon.

---
## Method: FormItem.getFullDataPath

### Description
Return the fully-qualified dataPath for the this formItem (ie, the dataPath expressed in absolute terms from the root of the hierarchy, rather than relative to the item's parent form). Note that the item's name is substituted into the full dataPath if the item does not specify an explicit dataPath. For example, if we have a field called `name` that specifies no dataPath, on a form that specifies a dataPath of `/order/items`, this method will return `/order/items/name`

### Returns

`[DataPath](../reference_2.md#type-datapath)` — Fully-qualified dataPath for this form item

**Flags**: A

---
## Method: FormItem.getDataPath

### Description
Return the dataPath for the this formItem.

### Returns

`[DataPath](../reference_2.md#type-datapath)` — dataPath for this form item

**Flags**: A

---
## Method: FormItem.invalidateDisplayValueCache

### Description
If this item has a specified [FormItem.displayField](#attr-formitemdisplayfield), the value displayed to the user for this item may be derived from another field.

The display field can be either another field value in the same record or a field that must be retrieved from a related [optionDataSource](#attr-formitemoptiondatasource) if [FormItem.fetchMissingValues](#attr-formitemfetchmissingvalues) is true. In this latter case, we perform a fetch against the option dataSource when the item value changes in order to determine the display value to show (and we make the associated record available via [FormItem.getSelectedRecord](#method-formitemgetselectedrecord)).

We cache this data on the form item, so if the item value changes to a new value, then reverts to a previously-seen value, the display value and selected record are already available without the need for an additional fetch. The cached values will also be kept in synch with the dataSource data assuming it is modified via standard add, update or delete operations.

This method explicitly invalidates this cache of optionDataSource data, and if the item value is non null and fetchMissingValues is still true, re-fetches the data.

### Groups

- display_values

---
## Method: FormItem.setValueIcons

### Description
Sets the [valueIcons](#attr-formitemvalueicons) for this item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| map | [Object](../reference.md#type-object) | false | — | mapping of logical values for this item to icon src [SCImgURL](../reference.md#type-scimgurl)s or the special value "blank". |

### Groups

- valueIcons

---
## Method: FormItem.shouldFetchMissingValue

### Description
If this field has a specified [FormItem.optionDataSource](#attr-formitemoptiondatasource), should we perform a fetch against that dataSource to find the record that matches this field's value?

If the value is non-null, this method is called when the item is first rendered or whenever the value is changed via a call to [FormItem.setValue](#method-formitemsetvalue). If it returns true, a fetch will be dispatched against the optionDataSource to get the record matching the value

When the fetch completes, if a record was found that matches the data value (and the form item value has not subsequently changed again), the item will be re-rendered to reflect any changes to the display value, and the record matching the value will be available via [this.getSelectedRecord()](#method-formitemgetselectedrecord).

Default behavior will return false if [this.fetchMissingValues](#attr-formitemfetchmissingvalues) is set to false. Otherwise it will return true if [this.alwaysFetchMissingValues](#attr-formitemalwaysfetchmissingvalues) is set to true, or if a [FormItem.displayField](#attr-formitemdisplayfield) is specified for this item and the item value is not already present in the item's valueMap.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [Any](#type-any) | false | — | The new data value of the item. |

### Returns

`[Boolean](#type-boolean)` — should we fetch the record matching the new value from the item's optionDataSource?

---
