# FormItem Styling

[← Back to API Index](../reference.md)

---

## KB Topic: FormItem Styling

### Description
Different FormItem types are rendered using different DOM structures. This is an overview explaining the various elements that may be produced and how they can be styled:

Form items written out by a DynamicForm with [itemLayout:"table"](../classes/DynamicForm.md#attr-dynamicformitemlayout) are written into table cells. A formItem can govern the appearance of these cells using properties such as [FormItem.cellStyle](../classes/FormItem.md#attr-formitemcellstyle), [FormItem.cellHeight](../classes/FormItem.md#attr-formitemcellheight). These properties have no effect for formItems rendered outside a form (for example the during [grid editing](../classes/ListGrid_1.md#attr-listgridcanedit)), or if `itemLayout` is "absolute".

If a formItem is showing a [picker icon](../classes/FormItem.md#attr-formitemshowpickericon), the picker icon and text box will be written into an element referred to as the control table. Styling applied to this element (via [FormItem.controlStyle](../classes/FormItem.md#attr-formitemcontrolstyle)) will extend around both the text box and the picker (but not other icons, hints, etc). The control table is not written out if the pickerIcon is not visible except in the case where the [FormItem.showPickerIconOnFocus](../classes/FormItem.md#attr-formitemshowpickericononfocus) is true, and the item does not have focus, or if a developer explicitly sets [FormItem.alwaysShowControlBox](../classes/FormItem.md#attr-formitemalwaysshowcontrolbox) to true.

The textBox of an item is the area containing its main textual content. This may natively be achieved as a data element (such as an `<input ...>`), or a static DOM element. See [FormItem.textBoxStyle](../classes/FormItem.md#attr-formitemtextboxstyle), and related [FormItem.readOnlyTextBoxStyle](../classes/FormItem.md#attr-formitemreadonlytextboxstyle) and [FormItem.printTextBoxStyle](../classes/FormItem.md#attr-formitemprinttextboxstyle) for styling options. See also [FormItem.shouldApplyHeightToTextBox](../classes/FormItem.md#method-formitemshouldapplyheighttotextbox) for a discussion on sizing the text box.

Any visible [valueIcon](../classes/FormItem.md#attr-formitemvalueicons) will be rendered inside the text box for static items, or adjacent to it for items where the text is editable (such as [TextItem](../classes/TextItem.md#class-textitem)). Explicit styling for the valueIcon can be specified via the [FormItem.getValueIconStyle](../classes/FormItem.md#method-formitemgetvalueiconstyle) method.

FormItems can also show explicitly defined [FormItem.icons](../classes/FormItem.md#attr-formitemicons). By default these show up next to the item, outside its text box and control table / after the [picker icon](../classes/FormItem.md#attr-formitemshowpickericon) (if present), though [inline positioning](../classes/FormItemIcon.md#attr-formitemiconinline) is also supported for some cases. Their appearance and behavior are heavily customizable - see [FormItemIcon.baseStyle](../classes/FormItemIcon.md#attr-formitemiconbasestyle), [FormItemIcon.src](../classes/FormItemIcon.md#attr-formitemiconsrc) and related properties.

[FormItem hints](../classes/FormItem.md#attr-formitemhint) may be written out as static text after any icons, and styled according to the [FormItem.hintStyle](../classes/FormItem.md#attr-formitemhintstyle) - or where supported, written directly into the text box with styling derived from the textBoxStyle plus a suffix of `"Hint"`. (See [TextItem.showHintInField](../classes/TextItem.md#attr-textitemshowhintinfield)).

In addition to this, form items may show validation error icons or text (see [DynamicForm.showInlineErrors](../classes/DynamicForm.md#attr-dynamicformshowinlineerrors), [FormItem.showErrorIcon](../classes/FormItem.md#attr-formitemshowerroricon) and [FormItem.showErrorText](../classes/FormItem.md#attr-formitemshowerrortext)). The position of these error indicators is controlled by [DynamicForm.errorOrientation](../classes/DynamicForm.md#attr-dynamicformerrororientation).

Most formItem user-interface elements support stateful styling - showing a different appearance for [focused](../classes/FormItem.md#attr-formitemshowfocused), [over](../classes/FormItem.md#attr-formitemshowover), [disabled](../classes/FormItem.md#attr-formitemshowdisabled) and [error](../classes/FormItem.md#attr-formitemshowerrorstyle) states.

Default styling for items will vary by skin, and note that subclasses of FormItem may have additional styling properties not explicitly called out here.  
Developers performing global styling modifications for formItems should also be aware of compound items (such as [DateItem](../classes/DateItem.md#class-dateitem)) which achieve their user interface by embedding simpler items in an outer structure. See [CompoundFormItem_skinning](../reference.md#kb-topic-compoundformitem_skinning).

### Related

- [FormItemBaseStyle](../reference.md#type-formitembasestyle)
- [FormItem.cellHeight](../classes/FormItem.md#attr-formitemcellheight)
- [FormItem.showFocused](../classes/FormItem.md#attr-formitemshowfocused)
- [FormItem.showOver](../classes/FormItem.md#attr-formitemshowover)
- [FormItem.updateTextBoxOnOver](../classes/FormItem.md#attr-formitemupdatetextboxonover)
- [FormItem.updateControlOnOver](../classes/FormItem.md#attr-formitemupdatecontrolonover)
- [FormItem.updatePickerIconOnOver](../classes/FormItem.md#attr-formitemupdatepickericononover)
- [FormItem.showDisabled](../classes/FormItem.md#attr-formitemshowdisabled)
- [FormItem.cellStyle](../classes/FormItem.md#attr-formitemcellstyle)
- [FormItem.hintStyle](../classes/FormItem.md#attr-formitemhintstyle)
- [FormItem.titleStyle](../classes/FormItem.md#attr-formitemtitlestyle)
- [FormItem.textBoxStyle](../classes/FormItem.md#attr-formitemtextboxstyle)
- [FormItem.printTextBoxStyle](../classes/FormItem.md#attr-formitemprinttextboxstyle)
- [FormItem.printReadOnlyTextBoxStyle](../classes/FormItem.md#attr-formitemprintreadonlytextboxstyle)
- [FormItem.pickerIconStyle](../classes/FormItem.md#attr-formitempickericonstyle)
- [FormItem.controlStyle](../classes/FormItem.md#attr-formitemcontrolstyle)
- [SelectItem.pickerIconStyle](../classes/SelectItem.md#attr-selectitempickericonstyle)
- [SelectItem.showFocused](../classes/SelectItem.md#attr-selectitemshowfocused)
- [SelectItem.showOver](../classes/SelectItem.md#attr-selectitemshowover)
- [SelectItem.updateTextBoxOnOver](../classes/SelectItem.md#attr-selectitemupdatetextboxonover)
- [SelectItem.updateControlOnOver](../classes/SelectItem.md#attr-selectitemupdatecontrolonover)
- [UploadItem.textBoxStyle](../classes/UploadItem.md#attr-uploaditemtextboxstyle)
- [MiniDateRangeItem.textBoxStyle](../classes/MiniDateRangeItem.md#attr-minidaterangeitemtextboxstyle)

---
