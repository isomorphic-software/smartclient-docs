# DynamicForm Documentation

[← Back to API Index](../reference.md)

---

## Class: DynamicForm

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
The DynamicForm manages a collection of FormItems which represent user input controls. The DynamicForm provides [layout](../kb_topics/formLayout.md#kb-topic-form-layout), value management, validation and databinding for the controls it manages.

To create a DynamicForm, set [DynamicForm.fields](#attr-dynamicformfields) to an Array of Objects describing the FormItems you want to use. For example:

```
    isc.DynamicForm.create({
        fields:[
            {name:"userName", type:"text"},  // creates a TextItem
            {name:"usState", type:"select"}  // creates a SelectItem
        ]
    })
 
```
The item `name` is an identifier for the item that must be unique just within this form. It is used:

*   as the name under which the item's value is stored in the form (the form's current values are accessible as [form.getValues()](#method-dynamicformgetvalues)
*   when retrieving the FormItem's current value (via [form.getValue()](#method-dynamicformgetvalue))
*   to retrieve the item itself via [form.getItem()](#method-dynamicformgetitem)

FormItems can also be created by binding the form to a DataSource via `setDataSource()`. In this case, FormItems are chosen based on the data type of the field - see [FormItemType](../reference.md#type-formitemtype). You can override the automatically chosen FormItem via [DataSourceField.editorType](DataSourceField.md#attr-datasourcefieldeditortype).

FormItem lifecycle is managed by the DynamicForm itself. FormItem instances are created and destroyed automatically when new fields are added to the form.

When using DataSource binding, you can also add additional FormItems not specified in the DataSource, or override any properties on the automatically generated FormItems, without having to re-declare any information that comes from the DataSource. See the QuickStart Guide chapter on Data Binding for an overview.

All FormItems share a common set of properties for controlling [form\\n layout](../kb_topics/formLayout.md#kb-topic-form-layout). Other properties common to all FormItems are documented on the [FormItem](FormItem.md#class-formitem) class, and properties specific to particular FormItems are documented on the respective FormItems.

NOTE: For very simple forms consisting of exactly one item, you still use a DynamicForm. See the "fontSelector" form in the *Toolstrip example*.

---
## ClassAttr: DynamicForm.NORMAL

### Description
A declared value of the enum type [Encoding](../reference_2.md#type-encoding).

**Flags**: R

---
## ClassAttr: DynamicForm.POST

### Description
A declared value of the enum type [FormMethod](../reference.md#type-formmethod).

**Flags**: R

---
## ClassAttr: DynamicForm.MULTIPART

### Description
A declared value of the enum type [Encoding](../reference_2.md#type-encoding).

**Flags**: R

---
## ClassAttr: DynamicForm.GET

### Description
A declared value of the enum type [FormMethod](../reference.md#type-formmethod).

**Flags**: R

---
## Attr: DynamicForm.checkFileAccessOnSubmit

### Description
For dynamicForms containing a [FileItem](FileItem.md#class-fileitem) for uploading files, should the browser verify that the file is accessible before submitting the uploaded file to the server?

In some cases the browser may not be able to access the selected file.  
This can occur when the file has been modified in the file system after selection in the browser, or if the current user doesn't have permission to view the file.

By default, before submitting the file to the server the browser will verify that it can access the file's contents and display the [DynamicForm.fileAccessFailedWarning](#attr-dynamicformfileaccessfailedwarning) if file access fails.  
Note that accessing the file's contents is an asynchronous process, so form submission is not performed synchronously.

This means that if application code calls [DynamicForm.saveData](#method-dynamicformsavedata) on a form containing a fileItem and then synchronously [clears](Canvas.md#method-canvasclear) it from the DOM, the upload will never be kicked off.  
Setting `checkFileAccessOnSubmit` to false will suppress the (asynchronous) check, and can be used to bypass this limitation, but this is not recommended except as a short term backwards-compatibility workaround. Instead we'd recommend using the [saveData callback](#method-dynamicformsavedata) to clear the form when the upload has completed. This also gives the user an opportunity to correct validation errors and re-submit the form if necessary.

**Flags**: IRWA

---
## Attr: DynamicForm.readOnlyDisplay

### Description
If [DynamicForm.canEdit](#attr-dynamicformcanedit) is set to `false`, how should the items in this form be displayed to the user?

Can be overridden via [FormItem.readOnlyDisplay](FormItem.md#attr-formitemreadonlydisplay) on individual form items.

### Groups

- appearance
- readOnly

**Flags**: IRW

---
## Attr: DynamicForm.errorItemProperties

### Description
If [DynamicForm.showInlineErrors](#attr-dynamicformshowinlineerrors) is false we show all errors for the form item in a single item rendered at the top of the form.  
This attribute contains a properties block for this item.

### Groups

- validation

**Flags**: IRA

---
## Attr: DynamicForm.clipItemTitles

### Description
Should the titles for form items be clipped if they are too large for the available space?

Can be overridden for individual items via [FormItem.clipTitle](FormItem.md#attr-formitemcliptitle).

**Flags**: IRW

---
## Attr: DynamicForm.target

### Description
The name of a window or frame that will receive the results returned by the form's action. The default null indicates to use the current frame.

**NOTE:** this is used only in the very rare case that a form is used to submit data directly to a URL. Normal server contact is through [DataBound Component Methods](../kb_topics/dataBoundComponentMethods.md#kb-topic-databound-component-methods).

### Groups

- submitting

**Flags**: IRWA

---
## Attr: DynamicForm.revertValueKey

### Description
Keyboard shortcut that causes the value of the currently focused form item to be reverted to whatever value would be shown if [DynamicForm.resetValues](#method-dynamicformresetvalues) were called.

**Flags**: IR

---
## Attr: DynamicForm.canTabToIcons

### Description
Should users be able to tab into the [icons](FormItem.md#attr-formitemicons) and [picker icon](FormItem.md#attr-formitemshowpickericon) for items within this form by default?

May be overridden at the item level by [FormItem.canTabToIcons](FormItem.md#attr-formitemcantabtoicons).

Developers may also suppress tabbing to individual icons by setting [FormItemIcon.tabIndex](FormItemIcon.md#attr-formitemicontabindex) to `-1`.

### Groups

- formIcons

**Flags**: IRWA

---
## Attr: DynamicForm.showInlineErrors

### Description
If true, field errors are written into the form next to the item(s) where the errors occurred. Errors may appear as text or just an icon (via [DynamicForm.showErrorText](#attr-dynamicformshowerrortext):false).

If false, errors are written at the top of the form.

To do some other kind of error display, override [DynamicForm.showErrors](#method-dynamicformshowerrors).

### Groups

- validation

**Flags**: IRW

---
## Attr: DynamicForm.operator

### Description
When [FormItem.operator](FormItem.md#attr-formitemoperator) has been set for any [FormItem](FormItem.md#class-formitem) in this form, what logical operator should be applied across the [criteria](../reference_2.md#object-criterion) produced by the form items? Only applicable to forms that have a [dataSource](DataBoundComponent.md#attr-databoundcomponentdatasource).

**Flags**: IR

---
## Attr: DynamicForm.showErrorIcons

### Description
[showErrorIcons](#attr-dynamicformshowerroricons), [showErrorText](#attr-dynamicformshowerrortext), [errorOrientation](#attr-dynamicformerrororientation), and [showErrorStyle](#attr-dynamicformshowerrorstyle) control how validation errors are displayed when they are displayed inline in the form (next to the form item where there is a validation error). To instead display all errors at the top of the form, set [showInlineErrors](#attr-dynamicformshowinlineerrors):false.

`showErrorIcons`, `showErrorText`, `errorOrientation` and `showErrorStyle` are all boolean properties, and can be set on a DynamicForm to control the behavior form-wide, or set on individual FormItems.

The HTML displayed next to a form item with errors is generated by [FormItem.getErrorHTML](FormItem.md#method-formitemgeterrorhtml). The default implementation of that method respects `showErrorIcons` and `showErrorText` as follows:

`showErrorIcons`, or `showErrorIcon` at the FormItem level controls whether an error icon should appear next to fields which have validation errors. The icon's appearance is governed by [FormItem.errorIconSrc](FormItem.md#attr-formitemerroriconsrc), [FormItem.errorIconWidth](FormItem.md#attr-formitemerroriconwidth) and [FormItem.errorIconHeight](FormItem.md#attr-formitemerroriconheight)

`showErrorText` determines whether the text of the validation error should be displayed next to fields which have validation errors. The attribute [DynamicForm.showTitlesWithErrorMessages](#attr-dynamicformshowtitleswitherrormessages) may be set to prefix error messages with the form item's title + `":"` (may be desired if the item has [FormItem.showTitle](FormItem.md#attr-formitemshowtitle) set to false).  
If `showErrorText` is unset, the error text will be shown if [DynamicForm.linearMode](#attr-dynamicformlinearmode) is true (or [DynamicForm.linearOnMobile](#attr-dynamicformlinearonmobile) is true for mobile devices), otherwise it will not be shown.

In addition to this:

[DynamicForm.errorOrientation](#attr-dynamicformerrororientation) controls where the error HTML should appear relative to form items. Therefore the combination of [DynamicForm.showErrorText](#attr-dynamicformshowerrortext)`:false` and [DynamicForm.errorOrientation](#attr-dynamicformerrororientation)`:"left"` creates a compact validation error display consisting of just an icon, to the left of the item with the error message available via a hover (similar appearance to ListGrid validation error display).  
If `errorOrientation` is unset, the error orientation will default to "top" if [DynamicForm.linearMode](#attr-dynamicformlinearmode) is enabled (or [DynamicForm.linearOnMobile](#attr-dynamicformlinearonmobile) is true for mobile devices) and error text is not showing, "left" otherwise.

`showErrorStyle` determines whether fields with validation errors should have special styling applied to them. Error styling is achieved by applying suffixes to existing styling applied to various parts of the form item. See [FormItemBaseStyle](../reference.md#type-formitembasestyle) for more on this.

### Groups

- validation

**Flags**: IRW

---
## Attr: DynamicForm.minHintWidth

### Description
Minimum horizontal space made available for [FormItem.hint](FormItem.md#attr-formitemhint) text. Typically this reflects how much space the hint text takes up before it wraps. May be overridden at the item level via [FormItem.minHintWidth](FormItem.md#attr-formitemminhintwidth).

This setting does not apply to hints that are [shown in field](TextItem.md#attr-textitemshowhintinfield).

### See Also

- [DynamicForm.wrapHintText](#attr-dynamicformwraphinttext)

**Flags**: IR

---
## Attr: DynamicForm.linearAutoSpanItems

### Description
When a form is rendered in [DynamicForm.linearMode](#attr-dynamicformlinearmode), should each item appear on its own row, spanning the full set of rendered columns by default?

**Flags**: IRW

---
## Attr: DynamicForm.linearNumCols

### Description
Specifies the [number of columns](#attr-dynamicformnumcols) when the form is being rendered in [DynamicForm.linearMode](#attr-dynamicformlinearmode), overriding any automatically derived value in that mode.

### Groups

- formLayout

**Flags**: IRW

---
## Attr: DynamicForm.disableValidation

### Description
If set to true, client-side validators will not run on the form when validate() is called. Server-side validators (if any) will still run on attempted save.

### Groups

- validation

### See Also

- [DynamicForm.saveData](#method-dynamicformsavedata)
- [DynamicForm.submit](#method-dynamicformsubmit)

**Flags**: IRW

---
## Attr: DynamicForm.showTitlesWithErrorMessages

### Description
Indicates whether on validation failure, the error message displayed to the user should be pre-pended with the title for the item.

### Groups

- validation

**Flags**: IRW

---
## Attr: DynamicForm.showDetailFields

### Description
For databound forms, whether to show fields marked as detail fields.

**Flags**: IR

---
## Attr: DynamicForm.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: DynamicForm.valuesManager

### Description
If set at init time, this dynamicForm will be created as a member form of the specified valuesManager. To update the form's valuesManager after init, use the [form-level setter](#method-dynamicformsetvaluesmanager), or the [addMember(form)](ValuesManager.md#method-valuesmanageraddmember) / [removeMember(form)](ValuesManager.md#method-valuesmanagerremovemember) APIs on `ValuesManager`.

### Groups

- formValuesManager

### See Also

- [ValuesManager](ValuesManager.md#class-valuesmanager)

**Flags**: I

---
## Attr: DynamicForm.wrapItemTitles

### Description
Whether titles for form items should wrap. If not specified, titles will wrap by default. Can be overridden for individual items via [FormItem.wrapTitle](FormItem.md#attr-formitemwraptitle)

### Groups

- formTitles

**Flags**: IRW

---
## Attr: DynamicForm.timeFormatter

### Description
Default [TimeDisplayFormat](../reference.md#type-timedisplayformat) for [type:"time"](FormItem.md#attr-formitemtype) field values displayed in this form.

Note that if specified, [FormItem.dateFormatter](FormItem.md#attr-formitemdateformatter) and [FormItem.timeFormatter](FormItem.md#attr-formitemtimeformatter) take precedence over the format specified at the component level.

If no explicit formatter is specified at the field or component level, time values will be formatted according to the system-wide [normal time display format](Time.md#classmethod-timesetnormaldisplayformat). specified field type.

**Flags**: IRW

---
## Attr: DynamicForm.showImageAsURL

### Description
For fields of [type:"image"](../reference.md#type-formitemtype), if the field is non editable, and being displayed with [readOnlyDisplay:"static"](FormItem.md#attr-formitemreadonlydisplay), should the value (URL) be displayed as text, or should an image be rendered?

May be overridden for individual items via [FormItem.showImageAsURL](FormItem.md#attr-formitemshowimageasurl).

**Flags**: IRW

---
## Attr: DynamicForm.requiredRightTitleSuffix

### Description
The string appended to the title of every required item in this form if [DynamicForm.hiliteRequiredFields](#attr-dynamicformhiliterequiredfields) is true and the [TitleOrientation](../reference.md#type-titleorientation) property is set to "right".

### Groups

- formTitles

**Flags**: IRW

---
## Attr: DynamicForm.implicitSave

### Description
When true, indicates that changes to items in this form will be automatically saved on a [delay](#attr-dynamicformimplicitsavedelay), as well as when the entire form is submitted. Unless [form.implicitSaveOnBlur](#attr-dynamicformimplicitsaveonblur) is set to false, changes will also be automatically saved on editorExit for each item. This attribute can also be set directly on FormItems.

**Flags**: IRW

---
## Attr: DynamicForm.cellPadding

### Description
The amount of empty space, in pixels, surrounding each form item within its cell in the layout grid.

### Groups

- formLayout

**Flags**: IRW

---
## Attr: DynamicForm.unknownErrorMessage

### Description
The error message for a failed validator that does not specify its own errorMessage.

### Groups

- validation
- i18nMessages

**Flags**: IRW

---
## Attr: DynamicForm.canTabToSectionHeaders

### Description
If true, the headers for any [SectionItems](SectionStackSection.md#attr-sectionstacksectionitems) will be included in the page's tab order for accessibility. May also be set at the item level via [SectionItem.canTabToHeader](SectionItem.md#attr-sectionitemcantabtoheader)

If unset, section headers will be focusable if [isc.setScreenReaderMode](isc.md#staticmethod-iscsetscreenreadermode) has been called. See [accessibility](../kb_topics/accessibility.md#kb-topic-accessibility--section-508-compliance).

**Flags**: IRA

---
## Attr: DynamicForm.implicitSaveDelay

### Description
When [implicitSave](#attr-dynamicformimplicitsave) is true, this attribute dictates the millisecond delay after which form items are automatically saved during editing.

**Flags**: IRW

---
## Attr: DynamicForm.synchronousValidation

### Description
If enabled, whenever validation is triggered and a request to the server is required, user interactivity will be blocked until the request returns. Can be set for the entire form or individual FormItems.

If false, the form will try to avoid blocking user interaction until it is strictly required. That is until the user attempts to use a FormItem whose state could be affected by a server request that has not yet returned.

**Flags**: IR

---
## Attr: DynamicForm.userTask

### Description
Associated userTask if current dynamic form used along with workflow. See [userTask](UserTask.md#class-usertask) for more details.

**Flags**: IR

---
## Attr: DynamicForm.nestedListEditorType

### Description
[FormItem](FormItem.md#class-formitem) class to use for any list-type complex fields on this DynamicForm. List-type fields are denoted by marking them `multiple: true` in the DataSource.

### See Also

- [DynamicForm.nestedEditorType](#attr-dynamicformnestededitortype)

**Flags**: IRW

---
## Attr: DynamicForm.requiredMessage

### Description
The required message for required field errors.

### Groups

- formTitles

**Flags**: IRW

---
## Attr: DynamicForm.titlePrefix

### Description
The string pre-pended to the title of every item in this form. See also +{requiredTitlePrefix} for fields that are required.

### Groups

- formTitles

**Flags**: IRW

---
## Attr: DynamicForm.action

### Description
The URL to which the form will submit its values.

**NOTE:** this is used only in the very rare case that a form is used to submit data directly to a URL. Normal server contact is through RPCManager.  
See [DynamicForm.canSubmit](#attr-dynamicformcansubmit) for more on this.

### Groups

- submitting

### See Also

- [operations](../kb_topics/operations.md#kb-topic-operations-overview)
- [RPCManager](RPCManager.md#class-rpcmanager)

**Flags**: IRW

---
## Attr: DynamicForm.validateOnExit

### Description
If true, form items will be validated when each item's "editorExit" handler is fired as well as when the entire form is submitted or validated.

Note that this property can also be set at the item level to enable finer granularity validation in response to user interaction - if true at either level, validation will occur on editorExit.

### See Also

- [FormItem.validateOnExit](FormItem.md#attr-formitemvalidateonexit)

**Flags**: IRW

---
## Attr: DynamicForm.itemHoverAlign

### Description
Text alignment for hovers shown for items

### Groups

- Hovers

### See Also

- [FormItem.hoverAlign](FormItem.md#attr-formitemhoveralign)

**Flags**: IRW

---
## Attr: DynamicForm.implicitSaveOnBlur

### Description
If true, form item values will be automatically saved when each item's "editorExit" handler is fired as well as on a delay and when the entire form is submitted. This attribute can also be set directly on FormItems.

**Flags**: IRW

---
## Attr: DynamicForm.validationURL

### Description
validationURL can be set to do server-side validation against a different URL from where the form will ultimately save, as part of an incremental upgrade strategy for Struts-like applications.

If set, calling [DynamicForm.submit](#method-dynamicformsubmit) causes an RPC to be sent to this URL to perform server-side validation of the form values. If the validation fails, the validation errors returned by the server are rendered in the form. If the validation succeeds, the form is submitted to the URL specified by [DynamicForm.action](#attr-dynamicformaction).

The form values are available on the server as request parameters (just like a normal form submit) and also as the values of a DSRequest sent as an RPC alongside the normal submit.

The expected response to this request is a DSResponse sent via the RPC mechanism. If validation is successful, an empty response with the STATUS\_SUCCESS status code is sufficient. If there are validation errors, the DSResponse should have the status set to STATUS\_VALIDATION\_ERROR and the errors should be set on the response via the addError()/setErrorReport() API on DSResponse. See the javadoc for DSResponse for details.

### Groups

- validation

### See Also

- [DynamicForm.saveData](#method-dynamicformsavedata)
- [DynamicForm.submit](#method-dynamicformsubmit)

**Flags**: IRW

---
## Attr: DynamicForm.canFocus

### Description
DynamicForms are considered to have focus if any of their form items have focus. Note that setting `dynamicForm.canFocus` to false will have no effect on whether form items within the form may receive focus. This property will only govern whether the form may receive focus if the form contains no focusable items.

### Groups

- focus

**Flags**: IRWA

---
## Attr: DynamicForm.errorsPreamble

### Description
If [DynamicForm.showInlineErrors](#attr-dynamicformshowinlineerrors) is `false`, all errors for the items in the form are rendered as a single item at the top of the form. This attribute specifies an introductory message rendered out before the individual error messages.

### Groups

- validation
- i18nMessages

**Flags**: IR

---
## Attr: DynamicForm.titleSuffix

### Description
The string appended to the title of every item in this form. See also +{requiredTitleSuffix} for fields that are required.

### Groups

- formTitles

**Flags**: IRW

---
## Attr: DynamicForm.colWidths

### Description
An array of widths for the columns of items in this form's layout grid.

If specified, these widths should sum to the total width of the form (form.width). If not specified, we assume every other column will contain form item titles, and so should have `form.titleWidth`, and all other columns should share the remaining space.

Acceptable values for each element in the array are:  

*   A number (e.g. 100) representing the number of pixel widths to allocate to a column.
*   A percent (e.g. 20%) representing the percentage of the total form.width to allocate to a column.
*   "\*" (all) to allocate remaining width (form.width minus all specified column widths). Multiple columns can use "\*", in which case remaining width is divided between all columns marked "\*".

Note that if title columns are left at the default [DynamicForm.titleWidth](#attr-dynamicformtitlewidth) or assigned a fixed width, while the others are configured to use the remaining horizontal space (i.e. with a percent or "\*" as described above), then care must be taken if you have long titles with no spaces or [DynamicForm.wrapItemTitles](#attr-dynamicformwrapitemtitles) is false.

Depending on the title font and exact column width applied, the title may overflow its assigned column, causing the form itself to overflow. If the form's parent has [overflow](Canvas.md#attr-canvasoverflow): "auto" and the form has width: "100%" or its parent is a [Layout](Layout.md#class-layout) with [hPolicy](Layout.md#attr-layouthpolicy): "fill", this could cause a horizontal scrollbar to appear in a situation where it doesn't seem necessary.

If the parent's height is just right so that the space taken by the unwanted horizontal scrollbar introduces a vertical scrollbar, this may even lead to oscillating scrollbars on the parent. To avoid, you must address the original problem of the title overflowing its assigned column, by widening it, using a smaller font, or allowing wrapping to occur.

### Groups

- formLayout

**Flags**: IRW

---
## Attr: DynamicForm.titleOrientation

### Description
Default orientation for titles for items in this form. [TitleOrientation](../reference.md#type-titleorientation) lists valid options.

Note that titles on the left or right take up a cell in tabular [form layouts](../kb_topics/formLayout.md#kb-topic-form-layout), but titles on top do not.

### Groups

- formTitles

**Flags**: IRW

---
## Attr: DynamicForm.autoComplete

### Description
Should this form allow browser auto-completion of its items' values? Applies only to items based on native HTML form elements ([TextItem](TextItem.md#class-textitem), [PasswordItem](../reference.md#class-passworditem), etc), and will only have a user-visible impact for browsers where native autoComplete behavior is actually supported and enabled via user settings.

This property may be explicitly specified per item via [FormItem.autoComplete](FormItem.md#attr-formitemautocomplete).

Note that even with this value set to `"none"`, native browser auto-completion may occur for log in forms (forms containing username and [password](../reference.md#class-passworditem) fields). This behavior varies by browser, and is a result of an [intentional change by some browser developers](https://www.google.com/search?q=password+ignores+autocomplete+off) to disregard the HTML setting _autocomplete=off_ for password items or log-in forms.

### Groups

- autoComplete

### See Also

- [FormItem.autoComplete](FormItem.md#attr-formitemautocomplete)

**Flags**: IRW

---
## Attr: DynamicForm.fields

### Description
An array of field objects, specifying the order, layout, and types of each field in the DynamicForm.

When both `dynamicForm.fields` and `dynamicForm.dataSource` are set, `dynamicForm.fields` acts as a set of overrides as explained in [DataBoundComponent.fields](DataBoundComponent.md#attr-databoundcomponentfields).

See [Form Layout](../kb_topics/formLayout.md#kb-topic-form-layout) for information about how flags specified on the FormItems control how the form is laid out.

### Groups

- items

### See Also

- [FormItem](FormItem.md#class-formitem)

**Flags**: IRW

---
## Attr: DynamicForm.dateFormatter

### Description
Default [DateDisplayFormat](../reference.md#type-datedisplayformat) for Date type values displayed in this form.

If some field's value is set to a native Date object, how should it be displayed to the user? If specified this is the default display format to use, and will apply to all fields except those specified as [type:"time"](FormItem.md#attr-formitemtype) (See [DynamicForm.timeFormatter](#attr-dynamicformtimeformatter)).

May be overridden at the component level for fields of type `datetime` via [DynamicForm.datetimeFormatter](#attr-dynamicformdatetimeformatter).

Note that if specified, [FormItem.dateFormatter](FormItem.md#attr-formitemdateformatter) and [FormItem.timeFormatter](FormItem.md#attr-formitemtimeformatter) take precedence over the format specified at the component level.

If no explicit formatter is specified at the field or component level, dates will be formatted according to the system-wide [short date display format](DateUtil.md#classmethod-dateutilsetshortdisplayformat) or [short datetime display format](DateUtil.md#classmethod-dateutilsetshortdatetimedisplayformat) depending on the specified field type.

**Flags**: IRW

---
## Attr: DynamicForm.suppressBrowserClearIcons

### Description
Default [TextItem.suppressBrowserClearIcon](TextItem.md#attr-textitemsuppressbrowserclearicon) value for TextItems within this form.

**Flags**: IRW

---
## Attr: DynamicForm.titleAlign

### Description
Default alignment for item titles. If unset default alignment will be derived from [text direction](Page.md#classmethod-pageisrtl) as described in [DynamicForm.getTitleAlign](#method-dynamicformgettitlealign)

**Flags**: IRW

---
## Attr: DynamicForm.itemHoverHeight

### Description
A default height for hovers shown for items

### Groups

- Hovers

### See Also

- [FormItem.hoverHeight](FormItem.md#attr-formitemhoverheight)

**Flags**: IRW

---
## Attr: DynamicForm.linearMode

### Description
Switches the entire form to render in a style that is typical for form on a mobile device with one [FormItem](FormItem.md#class-formitem) per row.

The [DynamicForm.linearOnMobile](#attr-dynamicformlinearonmobile) attribute allows linear mode to be enabled on mobile interfaces automatically.

While `linearMode` is active, the form's table layout is determined using the following logic:

*   If [TitleOrientation](../reference.md#type-titleorientation) is not explicitly specified, it will be defaulted to `top`, causing each item's title to appear above its element.  
    **Note:** in linear mode, each item will have the same title orientation. The item-level [FormItem.titleOrientation](FormItem.md#attr-formitemtitleorientation) attribute will be ignored.
*   For those items with a [hint](FormItem.md#attr-formitemhint) that support [showing the hint in the field](TextItem.md#attr-textitemshowhintinfield), `showHintInField` will be defaulted true if unset.
*   For items showing validation errors inline, by default [error text](#attr-dynamicformshowerrortext) will be displayed, and errors will [be rendered above the item element](#attr-dynamicformerrororientation).
*   The [DynamicForm.numCols](#attr-dynamicformnumcols) property for the form is ignored. The form will render as a single column of items - or two columns if `titleOrientation` is specified as `"left"` or `"right"` by default. To override this, a developer may specify an explicit [DynamicForm.linearNumCols](#attr-dynamicformlinearnumcols) allowing multiple items to potentially be placed next to each other.
*   [FormItem.width](FormItem.md#attr-formitemwidth) is ignored and all items receive "\*" width unless [FormItem.linearWidth](FormItem.md#attr-formitemlinearwidth) is specified.

Note that if column widths have been specified via [DynamicForm.colWidths](#attr-dynamicformcolwidths), but the number of columns doesn't match the number of columns being rendered in linear mode, it will be ignored.

If [DynamicForm.linearAutoSpanItems](#attr-dynamicformlinearautospanitems) is true, each item in linear mode will span the full set of columns by default. With this setting enabled, `linearNumCols` can be understood as a way to allow some items that are known to not require the full width of the UI to appear next to each other in an otherwise single-column form.

When `linearAutoSpanItems` is enabled, the following properties are available for further customizing the placement and sizing of items in a linear form:

*   [FormItem.colSpan](FormItem.md#attr-formitemcolspan) is ignored and defaulted to "\*", unless [FormItem.linearColSpan](FormItem.md#attr-formitemlinearcolspan) is specified.
*   [FormItem.startRow](FormItem.md#attr-formitemstartrow) and [FormItem.endRow](FormItem.md#attr-formitemendrow) are ignored and all items will default to `startRow:false` and `endRow:true`. This may be overridden per item via [FormItem.linearStartRow](FormItem.md#attr-formitemlinearstartrow) and [FormItem.linearEndRow](FormItem.md#attr-formitemlinearendrow).

For the best appearance, try to get your form to horizontally fill the screen, or almost all of it, on handset-sized devices. Any kind of fixed width on mobile is probably not going to work as well. One way to achieve this is by using a [SplitPane](SplitPane.md#class-splitpane).

### Groups

- formLayout

### See Also

- [DynamicForm.linearOnMobile](#attr-dynamicformlinearonmobile)

**Flags**: IRW

---
## Attr: DynamicForm.allowExpressions

### Description
For a form that produces filter criteria (see [form.getValuesAsCriteria()](#method-dynamicformgetvaluesascriteria)), allows the user to enter simple expressions in any field in this form that takes text input.

Also note that enabling `allowExpressions` for an entire form changes the [DynamicForm.defaultSearchOperator](#attr-dynamicformdefaultsearchoperator) to ["iContainsPattern"](DataSource.md#attr-datasourcetranslatepatternoperators), so that simple search expressions similar to SQL "LIKE" patterns can be entered in most fields.

See [FormItem.allowExpressions](FormItem.md#attr-formitemallowexpressions) for details.

### Groups

- advancedFilter

**Flags**: IRW

---
## Attr: DynamicForm.clipStaticValue

### Description
Default [FormItem.clipStaticValue](FormItem.md#attr-formitemclipstaticvalue) setting for items in this form. When unset, this is equivalent to `false`.

**Flags**: IR

---
## Attr: DynamicForm.storeDisplayValues

### Description
For editable fields with a specified [FormItem.displayField](FormItem.md#attr-formitemdisplayfield) and [FormItem.optionDataSource](FormItem.md#attr-formitemoptiondatasource), if the user selects a new value (typically from PickList based item such as a SelectItem), should the selected displayValue be updated on the record being edited in addition to the value for the actual item.  
Note that this only applies for fields using [local display field values](FormItem.md#attr-formitemuselocaldisplayfieldvalue) - typically [foreignKey fields](DataSourceField.md#attr-datasourcefieldforeignkey) where the display field is [included from](DataSourceField.md#attr-datasourcefieldincludefrom) another dataSource.

Default value is `true`. This is typically desirable for editing records with a displayField-mapped field, as it ensures the edited record will be be updated to contain the correct display value as well as the correct data value. As such, the expected display value is available on the record for display (for example in a ListGrid cell).

It may not be desirable for an interface specifically intended for [gathering criteria](#method-dynamicformgetvaluesascriteria) - in this case, results ought to be limited by an item's actual selected value, not by whatever text is displayed to the user.

See [DataSourceField.displayField](DataSourceField.md#attr-datasourcefielddisplayfield) for more details.

Note: the modified display field value will be passed to the server along with the modified foreignKey field value if a [databound update operation](#method-dynamicformsavedata) is performed. This occurs even if the displayField is [included from another DataSource](DataSourceField.md#attr-datasourcefieldincludefrom) and therefore read-only. In this case the server will simply ignore the modified display field value. This is as expected - a subsequent fetch for the same record would recalculate the displayField value on the server using the updated foreignKey field value (and return the same display value previously displayed to the user).

This attribute can also be set for [individual items](FormItem.md#attr-formitemstoredisplayvalues).

**Flags**: IRA

---
## Attr: DynamicForm.longTextEditorThreshold

### Description
When creating form items for fields with text type data, if the specified length of the field exceeds this threshold we will create form item of type `this.longTextEditorType` (a TextAreaItem by default), rather than a simple text item. Overridden by explicitly specifying `editorType` for the field.

### Groups

- appearance

**Flags**: IRW

---
## Attr: DynamicForm.titleWidth

### Description
The width in pixels allocated to the title of every item in this form. If you don't specify explicit [DynamicForm.colWidths](#attr-dynamicformcolwidths), you can set this value to the string "\*" to divide the usable space evenly between titles and fields.

### Groups

- formTitles

**Flags**: IRW

---
## Attr: DynamicForm.minColWidth

### Description
Minimum width of a form column.

### Groups

- formLayout

**Flags**: IRW

---
## Attr: DynamicForm.showErrorStyle

### Description
[showErrorIcons](#attr-dynamicformshowerroricons), [showErrorText](#attr-dynamicformshowerrortext), [errorOrientation](#attr-dynamicformerrororientation), and [showErrorStyle](#attr-dynamicformshowerrorstyle) control how validation errors are displayed when they are displayed inline in the form (next to the form item where there is a validation error). To instead display all errors at the top of the form, set [showInlineErrors](#attr-dynamicformshowinlineerrors):false.

`showErrorIcons`, `showErrorText`, `errorOrientation` and `showErrorStyle` are all boolean properties, and can be set on a DynamicForm to control the behavior form-wide, or set on individual FormItems.

The HTML displayed next to a form item with errors is generated by [FormItem.getErrorHTML](FormItem.md#method-formitemgeterrorhtml). The default implementation of that method respects `showErrorIcons` and `showErrorText` as follows:

`showErrorIcons`, or `showErrorIcon` at the FormItem level controls whether an error icon should appear next to fields which have validation errors. The icon's appearance is governed by [FormItem.errorIconSrc](FormItem.md#attr-formitemerroriconsrc), [FormItem.errorIconWidth](FormItem.md#attr-formitemerroriconwidth) and [FormItem.errorIconHeight](FormItem.md#attr-formitemerroriconheight)

`showErrorText` determines whether the text of the validation error should be displayed next to fields which have validation errors. The attribute [DynamicForm.showTitlesWithErrorMessages](#attr-dynamicformshowtitleswitherrormessages) may be set to prefix error messages with the form item's title + `":"` (may be desired if the item has [FormItem.showTitle](FormItem.md#attr-formitemshowtitle) set to false).  
If `showErrorText` is unset, the error text will be shown if [DynamicForm.linearMode](#attr-dynamicformlinearmode) is true (or [DynamicForm.linearOnMobile](#attr-dynamicformlinearonmobile) is true for mobile devices), otherwise it will not be shown.

In addition to this:

[DynamicForm.errorOrientation](#attr-dynamicformerrororientation) controls where the error HTML should appear relative to form items. Therefore the combination of [DynamicForm.showErrorText](#attr-dynamicformshowerrortext)`:false` and [DynamicForm.errorOrientation](#attr-dynamicformerrororientation)`:"left"` creates a compact validation error display consisting of just an icon, to the left of the item with the error message available via a hover (similar appearance to ListGrid validation error display).  
If `errorOrientation` is unset, the error orientation will default to "top" if [DynamicForm.linearMode](#attr-dynamicformlinearmode) is enabled (or [DynamicForm.linearOnMobile](#attr-dynamicformlinearonmobile) is true for mobile devices) and error text is not showing, "left" otherwise.

`showErrorStyle` determines whether fields with validation errors should have special styling applied to them. Error styling is achieved by applying suffixes to existing styling applied to various parts of the form item. See [FormItemBaseStyle](../reference.md#type-formitembasestyle) for more on this.

### Groups

- validation

**Flags**: IRW

---
## Attr: DynamicForm.hiliteRequiredFields

### Description
Indicates whether the titles of required items in this form should use the special prefix and suffix specified by the [DynamicForm.requiredTitlePrefix](#attr-dynamicformrequiredtitleprefix) and [DynamicForm.requiredTitleSuffix](#attr-dynamicformrequiredtitlesuffix) attributes, instead of the standard prefix and suffix.

### Groups

- formTitles

**Flags**: IRW

---
## Attr: DynamicForm.defaultSearchOperator

### Description
Default [search operator](../reference.md#type-operatorid) to use for fields in a form that produces [AdvancedCriteria](../reference.md#object-advancedcriteria). Default is "iContains" unless [DynamicForm.allowExpressions](#attr-dynamicformallowexpressions) is enabled for the form as a whole, in which case the default is ["iContainsPattern"](DataSource.md#attr-datasourcetranslatepatternoperators).

Does not apply to special fields where exact match is obviously the right default setting, such as fields of type:"enum", or fields with a [valueMap](FormItem.md#attr-formitemvaluemap) or [optionDataSource](FormItem.md#attr-formitemoptiondatasource).

`defaultSearchOperator` also has no effect in a form that does not produce `AdvancedCriteria` - see [DynamicForm.getValuesAsCriteria](#method-dynamicformgetvaluesascriteria) for settings that cause a form to produce AdvancedCriteria.

**Flags**: IR

---
## Attr: DynamicForm.fileAccessFailedWarning

### Description
Warning to display to the user if a selected file in an UploadItem cannot be accessed. This will be displayed on form submission when the browser is unable to access the selected file for upload.

Typically this indicates a browser-level security restriction - for example the file has been edited on the disk, or had its permissions changed after the user selected it, but before they attempted to submit the form.

When this occurs the selected file will be cleared from the upload item and this message will be displayed to the user in a [warn dialog](isc.md#staticmethod-iscwarn).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: DynamicForm.canEdit

### Description
If set to `false`, the form will be marked read-only. A widget on the form is editable if either (1) beginning with the widget and continuing up the containment hierarchy, including the form, the first widget to have a non-null `canEdit` attribute has canEdit:true, or (2) neither the widget nor any parent has a non-null `canEdit` attribute. This setting allows you to enable or disable the default editability of the form's items at one time.

This setting differs from the enabled/disabled state in that most form items will allow copying of the contents while read-only but do not while disabled.

Note that a form is considered editable if `canEdit` is null (default) or `true`.

### Groups

- readOnly

### See Also

- [DynamicForm.readOnlyDisplay](#attr-dynamicformreadonlydisplay)

**Flags**: IRWA

---
## Attr: DynamicForm.items

### Description
Synonym for [DynamicForm.fields](#attr-dynamicformfields)

### Groups

- items

### See Also

- [DynamicForm.fields](#attr-dynamicformfields)

**Flags**: IRW

---
## Attr: DynamicForm.linearOnMobile

### Description
Switches the entire form to render in a style that is typical for form on a [handset device](Browser.md#classattr-browserishandset) with one [FormItem](FormItem.md#class-formitem) per row by automatically defaulting [DynamicForm.linearMode](#attr-dynamicformlinearmode) to `true` on handsets.

**Note:** This property should not be changed framework-wide via [addProperties()](Class.md#classmethod-classaddproperties) as the framework itself assumes and relies upon normal behavior for forms. If you want most of your forms to use [DynamicForm.linearMode](#attr-dynamicformlinearmode) on mobile, create a subclass where `linearOnMobile` defaults to true, and pervasively use that subclass.

### Groups

- formLayout

**Flags**: IR

---
## Attr: DynamicForm.stopOnError

### Description
Indicates that if validation fails, the user should not be allowed to exit the field - focus will be forced back into the field until the error is corrected.

Enabling this property also implies [FormItem.validateOnExit](FormItem.md#attr-formitemvalidateonexit) is automatically enabled. If there are server-based validators on this item, setting this property also implies that [FormItem.synchronousValidation](FormItem.md#attr-formitemsynchronousvalidation) is forced on.

**Flags**: IR

---
## Attr: DynamicForm.suppressValidationErrorCallback

### Description
When calling [DynamicForm.saveData](#method-dynamicformsavedata) on a form or valuesManager, by default if the server returns an error code, any callback passed into saveData() will not be fired. If the error code returned by the server indicates a validation error, it will be displayed to the user by updating the form items to show the error messages, and firing any specified hiddenValidationErrors handler, otherwise the standard RPCManager error handling logic would be invoked.

Developers who want to handle errors themselves can override this default by specifying [dsRequest.willHandleError](RPCRequest.md#attr-rpcrequestwillhandleerror) on the DSRequest. In this case the callback passed in will be fired even if the server returns an error status code.

If `suppressValidationErrorCallback` is set to true, if a save attempt returns a _validation_ error code, the user-specified callback will not be fired _even if `willHandleError:true` was specified on the dsRequest_ - though for other error codes, the callback would be fired if willHandleError is specified on the request. Note that this is the historical behavior for SmartClient builds 8.0 and earlier

**Flags**: IRWA

---
## Attr: DynamicForm.readOnlyTextBoxStyle

### Description
Default [FormItem.readOnlyTextBoxStyle](FormItem.md#attr-formitemreadonlytextboxstyle) setting for items in this form.

**Flags**: IRW

---
## Attr: DynamicForm.canEditFieldAttribute

### Description
If this component is bound to a dataSource, this attribute may be specified to customize what fields from the dataSource may be edited by default. For example the [SearchForm](SearchForm.md#class-searchform) class has this attribute set to `"canFilter"` which allows search forms to edit dataSource fields marked as `canEdit:false` (but not those marked as `canFilter:false`).

Note that if `canEdit` is explicitly specified on a field in the [DataBoundComponent.fields](DataBoundComponent.md#attr-databoundcomponentfields) array, that property will be respected in preference to the canEditAttribute value. (See [FormItem.canEdit](FormItem.md#attr-formitemcanedit), [ListGridField.canEdit](ListGridField.md#attr-listgridfieldcanedit)). Also note that individual dataBoundComponents may have additional logic around whether a field can be edited - for example [ListGrid.canEditCell](ListGrid_2.md#method-listgridcaneditcell) may be overridden.

**Flags**: IRA

---
## Attr: DynamicForm.dataSource

### Description
The DataSource that this component should bind to for default fields and for performing [DataSource requests](../reference.md#object-dsrequest).

Can be specified as either a DataSource instance or the String ID of a DataSource.

### Groups

- databinding

**Flags**: IRW

---
## Attr: DynamicForm.showPending

### Description
This property applies to all of the items that a form has, and works according to [FormItem.showPending](FormItem.md#attr-formitemshowpending).

Also, in a form with showPending:true, an individual [FormItem](FormItem.md#class-formitem) can set showPending:false and vice versa.

**Flags**: IRA

---
## Attr: DynamicForm.itemHoverDelay

### Description
If the user rolls over an item, how long a delay before we fire any hover action / show a hover for that item?

### Groups

- Hovers

### See Also

- [FormItem.hoverDelay](FormItem.md#attr-formitemhoverdelay)

**Flags**: IRW

---
## Attr: DynamicForm.selectOnFocus

### Description
If this property is set to true, whenever a text-based field in this form ([TextItem](TextItem.md#class-textitem), [TextAreaItem](TextAreaItem.md#class-textareaitem)) is given focus programmatically (see [DynamicForm.focusInItem](#method-dynamicformfocusinitem)), all text within the item will be selected.

Note that this flag affects only programmatic focus. It's the normal behavior of text fields to select all text if the user navigates into them via keyboard, or if the user navigates via mouse, to place the text insertion point at the mouse click, and SmartClient preserves these behaviors. `selectOnFocus` is only needed for cases like a form within a pop-up dialog that should have the first field selected.

If you also want the value to be selected when the user clicks on the field, set [selectOnClick](#attr-dynamicformselectonclick) instead.

If `selectOnFocus` is false, the selection is not modified on focus - any previous selection within the item will be maintained.

May be overridden at the form item level via [FormItem.selectOnFocus](FormItem.md#attr-formitemselectonfocus).

### Groups

- focus

**Flags**: IRW

---
## Attr: DynamicForm.dataFetchMode

### Description
How to fetch and manage records retrieve from the server. See [FetchMode](../reference_2.md#type-fetchmode).

This setting only applies to the [ResultSet](ResultSet.md#class-resultset) automatically created by calling [fetchData()](ListGrid_1.md#method-listgridfetchdata). If a pre-existing ResultSet is passed to setData() instead, it's existing setting for [ResultSet.fetchMode](ResultSet.md#attr-resultsetfetchmode) applies.

### Groups

- databinding

**Flags**: IRW

---
## Attr: DynamicForm.rejectInvalidValueOnChange

### Description
If validateOnChange is true, and validation fails for an item on change, with no suggested value, should we revert to the previous value, or continue to display the bad value entered by the user. May be set at the item or form level.

**Flags**: IRWA

---
## Attr: DynamicForm.values

### Description
An Object containing the initial values of the form as properties, where each propertyName is the name of a [form item](../reference.md#kb-topic-form-items) in the form, and each property value is the value held by that form item.

The form's values may contain values that are not managed by any FormItem, and these values will be preserved and available when the form values are subsequently retrieved via [DynamicForm.getValues](#method-dynamicformgetvalues).

Providing values on initialization is equivalent to calling [DynamicForm.setValues](#method-dynamicformsetvalues).

As the user manipulates form items to change values, change events fire [on the items](FormItem.md#method-formitemchange) and [on the form as a whole](#method-dynamicformitemchange).

Note that form values are logical values, for example, the value of a [DateItem](DateItem.md#class-dateitem) is a JavaScript Date object, not a String, even if the user enters the date via a text input. Likewise the value of a [TextItem](TextItem.md#class-textitem) or [CheckboxItem](CheckboxItem.md#class-checkboxitem) that started out null remains null until the user changes it; the value will not be automatically converted to the null string ("") or false respectively, as happens with native HTML elements.

### Groups

- formValues

**Flags**: IRW

---
## Attr: DynamicForm.autoFetchTextMatchStyle

### Description
If [DynamicForm.autoFetchData](#attr-dynamicformautofetchdata) is `true`, this attribute allows the developer to specify a textMatchStyle for the initial [fetchData()](ListGrid_1.md#method-listgridfetchdata) call.

### Groups

- databinding

**Flags**: IR

---
## Attr: DynamicForm.dataArity

### Description
A DynamicForm is a [dataArity](DataBoundComponent.md#attr-databoundcomponentdataarity):single component.

### Groups

- databinding

**Flags**: IRWA

---
## Attr: DynamicForm.autoFocusOnError

### Description
If true, when [validation](#method-dynamicformvalidate) fails focus will automatically be put into the first focusable field which failed validation.

### Groups

- focus

**Flags**: IRW

---
## Attr: DynamicForm.noErrorDetailsMessage

### Description
A message to display to the user if server-side validation fails with an error but the server did not provide an error message

### Groups

- validation
- i18nMessages

**Flags**: IRW

---
## Attr: DynamicForm.fixedColWidths

### Description
If true, we ensure that column widths are at least as large as you specify them. This means that if any single column overflows (due to, eg, a long unbreakable title), the form as a whole overflows.

If false, columns will have their specified sizes as long as no column overflows. If any column overflows, space will be taken from any other columns that aren't filling the available room, until there is no more free space, in which case the form as a whole overflows.

### Groups

- formLayout

**Flags**: IRW

---
## Attr: DynamicForm.itemHoverWidth

### Description
A default width for hovers shown for items

### Groups

- Hovers

### See Also

- [FormItem.hoverWidth](FormItem.md#attr-formitemhoverwidth)

**Flags**: IRW

---
## Attr: DynamicForm.implicitCriteria

### Description
Criteria that are never shown to or edited by the user and are cumulative with any criteria provided via [DataBoundComponent.initialCriteria](DataBoundComponent.md#attr-databoundcomponentinitialcriteria) and related methods.

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope).

**Flags**: IRW

---
## Attr: DynamicForm.errorOrientation

### Description
[showErrorIcons](#attr-dynamicformshowerroricons), [showErrorText](#attr-dynamicformshowerrortext), [errorOrientation](#attr-dynamicformerrororientation), and [showErrorStyle](#attr-dynamicformshowerrorstyle) control how validation errors are displayed when they are displayed inline in the form (next to the form item where there is a validation error). To instead display all errors at the top of the form, set [showInlineErrors](#attr-dynamicformshowinlineerrors):false.

`showErrorIcons`, `showErrorText`, `errorOrientation` and `showErrorStyle` are all boolean properties, and can be set on a DynamicForm to control the behavior form-wide, or set on individual FormItems.

The HTML displayed next to a form item with errors is generated by [FormItem.getErrorHTML](FormItem.md#method-formitemgeterrorhtml). The default implementation of that method respects `showErrorIcons` and `showErrorText` as follows:

`showErrorIcons`, or `showErrorIcon` at the FormItem level controls whether an error icon should appear next to fields which have validation errors. The icon's appearance is governed by [FormItem.errorIconSrc](FormItem.md#attr-formitemerroriconsrc), [FormItem.errorIconWidth](FormItem.md#attr-formitemerroriconwidth) and [FormItem.errorIconHeight](FormItem.md#attr-formitemerroriconheight)

`showErrorText` determines whether the text of the validation error should be displayed next to fields which have validation errors. The attribute [DynamicForm.showTitlesWithErrorMessages](#attr-dynamicformshowtitleswitherrormessages) may be set to prefix error messages with the form item's title + `":"` (may be desired if the item has [FormItem.showTitle](FormItem.md#attr-formitemshowtitle) set to false).  
If `showErrorText` is unset, the error text will be shown if [DynamicForm.linearMode](#attr-dynamicformlinearmode) is true (or [DynamicForm.linearOnMobile](#attr-dynamicformlinearonmobile) is true for mobile devices), otherwise it will not be shown.

In addition to this:

[DynamicForm.errorOrientation](#attr-dynamicformerrororientation) controls where the error HTML should appear relative to form items. Therefore the combination of [DynamicForm.showErrorText](#attr-dynamicformshowerrortext)`:false` and [DynamicForm.errorOrientation](#attr-dynamicformerrororientation)`:"left"` creates a compact validation error display consisting of just an icon, to the left of the item with the error message available via a hover (similar appearance to ListGrid validation error display).  
If `errorOrientation` is unset, the error orientation will default to "top" if [DynamicForm.linearMode](#attr-dynamicformlinearmode) is enabled (or [DynamicForm.linearOnMobile](#attr-dynamicformlinearonmobile) is true for mobile devices) and error text is not showing, "left" otherwise.

`showErrorStyle` determines whether fields with validation errors should have special styling applied to them. Error styling is achieved by applying suffixes to existing styling applied to various parts of the form item. See [FormItemBaseStyle](../reference.md#type-formitembasestyle) for more on this.

### Groups

- validation
- appearance

**Flags**: IRW

---
## Attr: DynamicForm.initialCriteria

### Description
Criteria to be used when [DynamicForm.autoFetchData](#attr-dynamicformautofetchdata) is set.

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope).

### Groups

- searchCriteria

**Flags**: IR

---
## Attr: DynamicForm.encoding

### Description
encoding for the form, use MULTIPART\_ENCODING for file upload forms

### Groups

- submitting

**Flags**: IRWA

---
## Attr: DynamicForm.errors

### Description
A property list of itemName:errorMessage pairs, specifying the set of error messages displayed with the corresponding form elements. Each errorMessage may be either a single string or an array of strings, for example:  
  
`{fieldName:errors, fieldName:errors}`  
  
where each `errors` object will be either an error message string or an array of error message strings.

### Groups

- validation

**Flags**: IRW

---
## Attr: DynamicForm.formSubmitFailedWarning

### Description
Warning to display to the user if an attempt to [natively submit](#method-dynamicformsubmitform) a form is unable to submit to the server. The most common cause for this failure is that the user has typed an invalid file-path into an upload type field.

### Groups

- i18nMessages

**Deprecated**

**Flags**: IRWA

---
## Attr: DynamicForm.selectOnClick

### Description
If this property is set to true, whenever a text-based field in this form ([TextItem](TextItem.md#class-textitem), [TextAreaItem](TextAreaItem.md#class-textareaitem)) is given focus - whether programmatically (see [DynamicForm.focusInItem](#method-dynamicformfocusinitem)), or via a mouse click, all text within the item will be selected.

If you only want the value to be selected when on programmatic focus or keyboard navigation (this is the native browser behavior), set [selectOnFocus](#attr-dynamicformselectonfocus) instead.

May be overridden at the form item level via [FormItem.selectOnClick](FormItem.md#attr-formitemselectonclick).

### Groups

- focus

**Flags**: IRW

---
## Attr: DynamicForm.saveOperationType

### Description
Default [DSOperationType](../reference.md#type-dsoperationtype) to be performed when [DynamicForm.saveData](#method-dynamicformsavedata) is called. This property is automatically set on a call to [DynamicForm.editRecord](#method-dynamicformeditrecord) or [DynamicForm.editNewRecord](#method-dynamicformeditnewrecord), or may be set directly via [DynamicForm.setSaveOperationType](#method-dynamicformsetsaveoperationtype).

If `saveOperationType` is unset, the form will heuristically determine whether an "add" or "update" operation is intended based on whether the primaryKey field is present and editable.

**Flags**: IRW

---
## Attr: DynamicForm.longTextEditorType

### Description
Name of the Form Item class to use for text fields which exceed the longTextEditorThreshold for this form.

### Groups

- appearance

**Flags**: IRW

---
## Attr: DynamicForm.itemHoverVAlign

### Description
Vertical text alignment for hovers shown for items

### Groups

- Hovers

### See Also

- [FormItem.hoverVAlign](FormItem.md#attr-formitemhovervalign)

**Flags**: IRW

---
## Attr: DynamicForm.requiredRightTitlePrefix

### Description
The string pre-pended to the title of every required item in this form if [DynamicForm.hiliteRequiredFields](#attr-dynamicformhiliterequiredfields) is true and the [TitleOrientation](../reference.md#type-titleorientation) property is set to "right".

### Groups

- formTitles

**Flags**: IRW

---
## Attr: DynamicForm.errorItemCellStyle

### Description
If [DynamicForm.showInlineErrors](#attr-dynamicformshowinlineerrors) is false we show all errors for the form item in a single item rendered at the top of the form.  
This attribute specifies the cellStyle to apply to this item.

### Groups

- validation

**Flags**: IR

---
## Attr: DynamicForm.method

### Description
The mechanism by which form data is sent to the action URL. See FormMethod type for details.

**NOTE:** this is used only in the very rare case that a form is used to submit data directly to a URL. Normal server contact is through [DataBound Component Methods](../kb_topics/dataBoundComponentMethods.md#kb-topic-databound-component-methods).

### Groups

- submitting

**Flags**: IRW

---
## Attr: DynamicForm.saveOnEnter

### Description
If `true`, when the user hits the Enter key while focused in a text-item in this form, we automatically submit the form to the server using the [DynamicForm.submit](#method-dynamicformsubmit) method.

### Groups

- submitting

**Flags**: IRW

---
## Attr: DynamicForm.nestedEditorType

### Description
[FormItem](FormItem.md#class-formitem) class to use for any singular (ie, non-list) complex fields on this DynamicForm.

### See Also

- [DynamicForm.nestedListEditorType](#attr-dynamicformnestedlisteditortype)

**Flags**: IRW

---
## Attr: DynamicForm.showDeletions

### Description
Default [FormItem.showDeletions](FormItem.md#attr-formitemshowdeletions) setting for items in this form.

**Flags**: IRA

---
## Attr: DynamicForm.rightTitlePrefix

### Description
The string pre-pended to the title of an item in this form if its titleOrientation property is set to "right".

### Groups

- formTitles

**Flags**: IRW

---
## Attr: DynamicForm.datetimeFormatter

### Description
Default [DateDisplayFormat](../reference.md#type-datedisplayformat) for Date type values displayed in this form in fields of type `datetime`.

For datetime fields, this attribute will be used instead of [DynamicForm.dateFormatter](#attr-dynamicformdateformatter) when formatting Date values.

Note that if specified, [FormItem.dateFormatter](FormItem.md#attr-formitemdateformatter) and [FormItem.timeFormatter](FormItem.md#attr-formitemtimeformatter) take precedence over the format specified at the component level.

If no explicit formatter is specified at the field or component level, datetime field values will be formatted according to the system-wide [short datetime display format](DateUtil.md#classmethod-dateutilsetshortdatetimedisplayformat).

**Flags**: IRW

---
## Attr: DynamicForm.autoFetchData

### Description
If true, when this component is first drawn, automatically call `this.fetchData()`. Criteria for this fetch may be picked up from [DynamicForm.initialCriteria](#attr-dynamicforminitialcriteria), and textMatchStyle may be specified via [autoFetchTextMatchStyle](ListGrid_1.md#attr-listgridautofetchtextmatchstyle).

NOTE: if `autoFetchData` is set, calling [fetchData()](ListGrid_1.md#method-listgridfetchdata) before draw will cause two requests to be issued, one from the manual call to fetchData() and one from the autoFetchData setting. The second request will use only [DynamicForm.initialCriteria](#attr-dynamicforminitialcriteria) and not any other criteria or settings from the first request. Generally, turn off autoFetchData if you are going to manually call [fetchData()](ListGrid_1.md#method-listgridfetchdata) at any time. Note: If you are using saved searches - either via [SavedSearchItem](SavedSearchItem.md#class-savedsearchitem) or [ListGrid.saveDefaultSearch](ListGrid_1.md#attr-listgridsavedefaultsearch), autoFetchData will be automatically suspended and replaced with the saved criteria/view state, if applicable.

### Groups

- databinding

### See Also

- [ListGrid.fetchData](ListGrid_1.md#method-listgridfetchdata)

**Flags**: IR

---
## Attr: DynamicForm.requiredTitlePrefix

### Description
The string pre-pended to the title of every required item in this form if [DynamicForm.hiliteRequiredFields](#attr-dynamicformhiliterequiredfields) is true.

### Groups

- formTitles

**Flags**: IRW

---
## Attr: DynamicForm.itemHoverStyle

### Description
CSS Style for hovers shown for items

### Groups

- Hovers

### See Also

- [FormItem.hoverStyle](FormItem.md#attr-formitemhoverstyle)

**Flags**: IRW

---
## Attr: DynamicForm.cellBorder

### Description
Width of border for the table that form is drawn in. This is primarily used for debugging form layout.

### Groups

- formLayout

**Flags**: IRW

---
## Attr: DynamicForm.showComplexFieldsRecursively

### Description
If set, this `DynamicForm` will set both [showComplexFields](DataBoundComponent.md#attr-databoundcomponentshowcomplexfields) and `showComplexFieldsRecursively` on any nested component used for showing/editing a complex field. Thus any of this form's items that handle complex fields will themselves also show complex fields. This allows for handling of field structures of any complexity.

If set, this value automatically sets [showComplexFields](DataBoundComponent.md#attr-databoundcomponentshowcomplexfields) as well.

**Flags**: IR

---
## Attr: DynamicForm.showErrorText

### Description
[showErrorIcons](#attr-dynamicformshowerroricons), [showErrorText](#attr-dynamicformshowerrortext), [errorOrientation](#attr-dynamicformerrororientation), and [showErrorStyle](#attr-dynamicformshowerrorstyle) control how validation errors are displayed when they are displayed inline in the form (next to the form item where there is a validation error). To instead display all errors at the top of the form, set [showInlineErrors](#attr-dynamicformshowinlineerrors):false.

`showErrorIcons`, `showErrorText`, `errorOrientation` and `showErrorStyle` are all boolean properties, and can be set on a DynamicForm to control the behavior form-wide, or set on individual FormItems.

The HTML displayed next to a form item with errors is generated by [FormItem.getErrorHTML](FormItem.md#method-formitemgeterrorhtml). The default implementation of that method respects `showErrorIcons` and `showErrorText` as follows:

`showErrorIcons`, or `showErrorIcon` at the FormItem level controls whether an error icon should appear next to fields which have validation errors. The icon's appearance is governed by [FormItem.errorIconSrc](FormItem.md#attr-formitemerroriconsrc), [FormItem.errorIconWidth](FormItem.md#attr-formitemerroriconwidth) and [FormItem.errorIconHeight](FormItem.md#attr-formitemerroriconheight)

`showErrorText` determines whether the text of the validation error should be displayed next to fields which have validation errors. The attribute [DynamicForm.showTitlesWithErrorMessages](#attr-dynamicformshowtitleswitherrormessages) may be set to prefix error messages with the form item's title + `":"` (may be desired if the item has [FormItem.showTitle](FormItem.md#attr-formitemshowtitle) set to false).  
If `showErrorText` is unset, the error text will be shown if [DynamicForm.linearMode](#attr-dynamicformlinearmode) is true (or [DynamicForm.linearOnMobile](#attr-dynamicformlinearonmobile) is true for mobile devices), otherwise it will not be shown.

In addition to this:

[DynamicForm.errorOrientation](#attr-dynamicformerrororientation) controls where the error HTML should appear relative to form items. Therefore the combination of [DynamicForm.showErrorText](#attr-dynamicformshowerrortext)`:false` and [DynamicForm.errorOrientation](#attr-dynamicformerrororientation)`:"left"` creates a compact validation error display consisting of just an icon, to the left of the item with the error message available via a hover (similar appearance to ListGrid validation error display).  
If `errorOrientation` is unset, the error orientation will default to "top" if [DynamicForm.linearMode](#attr-dynamicformlinearmode) is enabled (or [DynamicForm.linearOnMobile](#attr-dynamicformlinearonmobile) is true for mobile devices) and error text is not showing, "left" otherwise.

`showErrorStyle` determines whether fields with validation errors should have special styling applied to them. Error styling is achieved by applying suffixes to existing styling applied to various parts of the form item. See [FormItemBaseStyle](../reference.md#type-formitembasestyle) for more on this.

### Groups

- validation

**Flags**: IRW

---
## Attr: DynamicForm.itemLayout

### Description
Layout style to use with this form.

The default of "table" uses a tabular layout similar to HTML tables, but with much more powerful control over sizing, item visibility and reflow, overflow handling, etc.

`itemLayout:"absolute"` allows absolute positioning of every form item. This provides maximum flexibility in placement, with the following limitations:

*   titles, which normally take up an adjacent cell, are not shown. Use StaticTextItems to show titles
*   no automatic reflow when showing or hiding items. [FormItem.setLeft](FormItem.md#method-formitemsetleft) and [FormItem.setTop](FormItem.md#method-formitemsettop) can be used for manual reflow.
*   only pixel and percent sizes are allowed, no "\*". Percent widths mean percentage of the overall form size rather than the column size
*   with different font styling or internationalized titles, items may overlap that did not overlap in the skin used at design time

### Groups

- formLayout

### See Also

- [formLayout](../kb_topics/formLayout.md#kb-topic-form-layout)
- [FormItem.width](FormItem.md#attr-formitemwidth)
- [FormItem.height](FormItem.md#attr-formitemheight)

**Flags**: IRWA

---
## Attr: DynamicForm.originalValueMessage

### Description
Default template HTML string when an item does not set its own [FormItem.originalValueMessage](FormItem.md#attr-formitemoriginalvaluemessage).

Variables in the template are substituted as follows:

| Variable | Substitution |
|---|---|
| $value | The item's old value as stored in the object returned by [DynamicForm.getOldValues](#method-dynamicformgetoldvalues). |
| $newValue | The item's new value. |

For `$value` and `$newValue`, any formatters or stored/display value mapping will be applied.

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: DynamicForm.autoFocus

### Description
If true, when the form is drawn, focus will automatically be put into the first focusable element in the form.  
Note that to put focus in a different item you can explicitly call `dynamicForm.focusInItem(_itemName_)`

### Groups

- focus

### See Also

- [DynamicForm.focusInItem](#method-dynamicformfocusinitem)

**Flags**: IRW

---
## Attr: DynamicForm.sectionVisibilityMode

### Description
If the form has sections, \[implemented as [SectionItem](SectionItem.md#class-sectionitem)s\], this attribute controls whether multiple sections can be expanded at once.

### Groups

- formLayout

### See Also

- [VisibilityMode](../reference.md#type-visibilitymode)
- [SectionItem](SectionItem.md#class-sectionitem)

**Flags**: IRW

---
## Attr: DynamicForm.showOldValueInHover

### Description
Default setting for the form items' [FormItem.showOldValueInHover](FormItem.md#attr-formitemshowoldvalueinhover) setting.

**Flags**: IRWA

---
## Attr: DynamicForm.validateOnChange

### Description
If true, form fields will be validated when each item's "change" handler is fired as well as when the entire form is submitted or validated.

Note that this property can also be set at the item level or on each validator to enable finer granularity validation in response to user interaction. If true at the form or field level, validators not explicitly set with `validateOnChange:false` will be fired on change - displaying errors and rejecting the change on validation failure.

### Groups

- validation

### See Also

- [FormItem.validateOnChange](FormItem.md#attr-formitemvalidateonchange)

**Flags**: IRW

---
## Attr: DynamicForm.numCols

### Description
The number of columns of titles and items in this form's layout grid. A title and corresponding item each have their own column, so to display two form elements per row (each having a title and item), you would set this property to 4.

### Groups

- formLayout

**Flags**: IRW

---
## Attr: DynamicForm.wrapHintText

### Description
Should items within this form that are showing a [FormItem.hint](FormItem.md#attr-formitemhint) have the hint text wrap? May be overridden at the item level via [FormItem.wrapHintText](FormItem.md#attr-formitemwraphinttext). If `wrapHintText` is unset on both the form and item, then the default behavior is not wrapping the hint.

This setting does not apply to hints that are [shown in field](TextItem.md#attr-textitemshowhintinfield).

### See Also

- [DynamicForm.minHintWidth](#attr-dynamicformminhintwidth)

**Flags**: IR

---
## Attr: DynamicForm.requiredTitleSuffix

### Description
The string appended to the title of every required item in this form if [DynamicForm.hiliteRequiredFields](#attr-dynamicformhiliterequiredfields) is true.

### Groups

- formTitles

**Flags**: IRW

---
## Attr: DynamicForm.itemHoverOpacity

### Description
Opacity for hovers shown for items

### Groups

- Hovers

### See Also

- [FormItem.hoverOpacity](FormItem.md#attr-formitemhoveropacity)

**Flags**: IRW

---
## Attr: DynamicForm.browserSpellCheck

### Description
If this browser has a 'spellCheck' feature for text-based form item elements, should it be used for items in this form? Can be overridden at the item level via [FormItem.browserSpellCheck](FormItem.md#attr-formitembrowserspellcheck)

Notes:  
\- this property only applies to text based items such as TextItem and TextAreaItem.  
\- this property is not supported on all browsers.

### See Also

- [FormItem.browserSpellCheck](FormItem.md#attr-formitembrowserspellcheck)

**Flags**: IRW

---
## Attr: DynamicForm.canSubmit

### Description
Governs whether this form will be used to perform a standard HTML form submission. Note that if true, [DynamicForm.submit](#method-dynamicformsubmit) will perform a native HTML submission to the specified [DynamicForm.action](#attr-dynamicformaction) URL.  
Wherever possible we strongly recommend using the [DataBound Component Methods](../kb_topics/dataBoundComponentMethods.md#kb-topic-databound-component-methods) to send data to the server as they provide a far more sophisticated interface, with built in options for server validation, required fields, etc.

### Groups

- submitting

**Flags**: IRWA

---
## Attr: DynamicForm.rightTitleSuffix

### Description
The string appended to the title of an item in this form if its titleOrientation property is set to "right".

### Groups

- formTitles

**Flags**: IRW

---
## Method: DynamicForm.getField

### Description
Synonym for dynamicForm.getItem()

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| itemName | [FieldName](../reference.md#type-fieldname) | false | — | name of the item you're looking for |

### Returns

`[FormItem](#type-formitem)` — FormItem object or null if not found

### Groups

- items

### See Also

- [DynamicForm.getItem](#method-dynamicformgetitem)

---
## Method: DynamicForm.getEditorType

### Description
Returns the form item type (Class Name) to be created for some field.  
By default `field.editorType` will be used if present - otherwise backs off to deriving the appropriate form item type from the data type of the field (see [FormItemType](../reference.md#type-formitemtype) for details).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [Object](../reference.md#type-object) | false | — | field definition for which we are deriving form item type. |
| values | [Object](../reference.md#type-object) | true | — | Current set of values being edited by this form. May be null. |

### Returns

`[String](#type-string)` — form item type for the field

### Groups

- editing

**Flags**: A

---
## Method: DynamicForm.valuesAreValid

### Description
Method to determine whether the current form values would pass validation. This method operates client-side, without contacting the server, running validators on the form's values and returning a value indicating whether validation was successful.

Unlike [DynamicForm.validate](#method-dynamicformvalidate) this method will not store the errors on the DynamicForm or display them to the user.

Note that [DynamicForm.checkForValidationErrors](#method-dynamicformcheckforvalidationerrors) allows for checking for server-side errors, and finding out what those errors are via a callback.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| validateHiddenFields | [boolean](../reference.md#type-boolean) | false | — | Should validators be processed for non-visible fields such as dataSource fields with no associated item or fields with visibility set to `"hidden"`? |
| returnErrors | [boolean](../reference.md#type-boolean) | true | — | If unset, this method returns a simple boolean value indicating success or failure of validation. If this parameter is passed, this method will return an object mapping each field name to the errors(s) encountered on validation failure, or null if validation was successful. |

### Returns

`[boolean](../reference.md#type-boolean)|[Map](#type-map)` — Boolean value indicating validation success, or if `returnErrors` was specified, an object mapping field names to the associated errors, for those fields that failed validation, or null if validation succeeded.

### Groups

- validation

---
## Method: DynamicForm.setTarget

### Description
Sets the [target](#attr-dynamicformtarget) for this form.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| target | [String](#type-string) | false | — | New submission target |

---
## Method: DynamicForm.fetchData

### Description
Retrieve data that matches the provided criteria, and edit the first record returned

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | true | — | search criteria |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

---
## Method: DynamicForm.getValuesAsAdvancedCriteria

### Description
Return an AdvancedCriteria object based on the current set of values within this form.

Similar to [DynamicForm.getValuesAsCriteria](#method-dynamicformgetvaluesascriteria), except the returned criteria object is guaranteed to be an AdvancedCriteria object, even if none of the form's fields has a specified [FormItem.operator](FormItem.md#attr-formitemoperator)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| textMatchStyle | [TextMatchStyle](../reference.md#type-textmatchstyle) | true | — | If specified the text match style will be used to generate the appropriate `operator` for per field criteria. |

### Returns

`[AdvancedCriteria](#type-advancedcriteria)` — a [AdvancedCriteria](../reference.md#object-advancedcriteria) based on the form's current values

### Groups

- criteriaEditing

---
## Method: DynamicForm.setAction

### Description
Sets the [action](#attr-dynamicformaction) for this form.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| action | [URL](../reference_2.md#type-url) | false | — | New action URL |

---
## Method: DynamicForm.getSaveOperationType

### Description
Returns the [DSOperationType](../reference.md#type-dsoperationtype) to be performed when [DynamicForm.saveData](#method-dynamicformsavedata) or [ValuesManager.saveData](ValuesManager.md#method-valuesmanagersavedata) is called.  
Valid options are `"add"` or `"update"`.

If a [DSRequest](../reference.md#object-dsrequest) configuration object is passed in containing an explicit operationType this will be returned. Otherwise [this.saveOperationType](#attr-dynamicformsaveoperationtype) will be returned if set. Note that `saveOperationType` is automatically set via calls to data binding methods such as [DynamicForm.editNewRecord](#method-dynamicformeditnewrecord), or it may be [set explicitly](#method-dynamicformsetsaveoperationtype).

If no explicit saveOperationType is present, the system will use the following heuristic to determine the save operationType:

*   If the form has no value for the [primaryKey field](DataSource.md#method-datasourcegetprimarykeyfield) this method will return "add". The assumption is that this is a new record, and the field will be populated when the record is created, (as with a "sequence" type field).
*   If, ${isc.DocUtils.linkForRef('method:DynamicForm.setValues','when the form\\'s values were populated')}, the form had value for the [primaryKey field](DataSource.md#method-datasourcegetprimarykeyfield) but it has subsequently be changed, this method will return "add". In this case the value has been changed, either by the user or programmatically so a different (new) record is assumed. This is determined by looking at the [oldValues](#method-dynamicformgetoldvalues) for the form.
*   If the [primaryKey field](DataSource.md#method-datasourcegetprimarykeyfield) is editable and a value is now present for the primary key field, but was not present in the [oldValues](#method-dynamicformgetoldvalues) for the form, this method will return "add". In this case either no initial values were provided, or a 'sparse' set of values for a new record (with no primary key) were provided to the form and the user has subsequently explicitly entered a new primaryKey field value.
*   Otherwise this method will return "update". Either the primaryKey field is non editable, or the user has not changed it from its initial value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | Optional DSRequest config block for the save operation |

### Returns

`[DSOperationType](../reference.md#type-dsoperationtype)` — Operation type for the save request.

---
## Method: DynamicForm.showFieldErrors

### Description
If this form has any outstanding validation errors for the field passed in, show them now. Called when field errors are set directly via [DynamicForm.setFieldErrors](#method-dynamicformsetfielderrors) / [DynamicForm.addFieldErrors](#method-dynamicformaddfielderrors) / [DynamicForm.clearFieldErrors](#method-dynamicformclearfielderrors).  
Default implementation simply falls through to [DynamicForm.showErrors](#method-dynamicformshowerrors).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | field to show errors for |

### Groups

- errors

---
## Method: DynamicForm.isPendingAsyncValidation

### Description
Is this component waiting for an asynchronous validation to complete? This method will return true after [DynamicForm.validate](#method-dynamicformvalidate) is called on a component with server-side validators for some field(s), until the server responds.

Note that the notification method [DynamicForm.handleAsyncValidationReply](#method-dynamicformhandleasyncvalidationreply) will be fired when validation completes.

### Returns

`[Boolean](#type-boolean)` — true if this widget has pending asynchronous validations in process

---
## Method: DynamicForm.itemKeyPress

### Description
Handler fired when a FormItem within this form receives a keypress event.

Fires after the keyPress handler on the FormItem itself, and only if the item did not cancel the event and chooses to allow it to propagate to the form as a whole.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | the FormItem where the change event occurred |
| keyName | [KeyName](../reference.md#type-keyname) | false | — | name of the key that was pressed (EG: "A", "Space") |
| characterValue | [number](#type-number) | false | — | numeric character value of the pressed key. |

### Returns

`[boolean](../reference.md#type-boolean)` — return false to cancel the keyPress, or true to allow it

---
## Method: DynamicForm.getItem

### Description
Retrieve a [FormItem](FormItem.md#class-formitem) in this form by it's [name](FormItem.md#attr-formitemname), [dataPath](FormItem.md#attr-formitemdatapath), or index within the [items](#attr-dynamicformitems) array.

FormItems that also have a [FormItem.ID](FormItem.md#attr-formitemid) may be accessed directly as a global variable `window[itemID]` or just `itemID`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| itemName | [String](#type-string)|[int](../reference.md#type-int) | false | — | name of the item you're looking for |

### Returns

`[FormItem](#type-formitem)` — FormItem object or null if not found

### Groups

- items

### See Also

- [DynamicForm.getItem](#method-dynamicformgetitem)

---
## Method: DynamicForm.focus

### Description
Give keyboard focus to this form. If this form has had focus before, focus will be passed to the item which last had focus (see [DynamicForm.getFocusItem](#method-dynamicformgetfocusitem)) - otherwise focus will be passed to the first focusable item in the form.

To put focus in a specific item, use [DynamicForm.focusInItem](#method-dynamicformfocusinitem) instead.

### Groups

- focus

---
## Method: DynamicForm.getTitleAlign

### Description
Get the alignment for the title for some item. Default implementation is as follows:

*   If [FormItem.titleAlign](FormItem.md#attr-formitemtitlealign) is specified, it will be respected
*   If not, and [this.titleAlign](#attr-dynamicformtitlealign) is set, it will be respected
*   Otherwise titles will be aligned according to [text direction](Page.md#classmethod-pageisrtl); for [titleOrientation](#attr-dynamicformtitleorientation) "top", this method returns `"left"` if text direction is LTR, and `"right"` if not; for horizontal orientations, this method returns `"right"` if text direction is LTR, or `"left"` if text direction is RTL.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | item for which we're getting title alignment |

### Returns

`[Alignment](../reference.md#type-alignment)` — alignment for title

**Flags**: A

---
## Method: DynamicForm.getItemErrorHTML

### Description
If [DynamicForm.showInlineErrors](#attr-dynamicformshowinlineerrors) is true, this method is called for each item in the form and returns the error HTML to be written out next to the item.  
Default implementation falls through to [FormItem.getErrorHTML](FormItem.md#method-formitemgeterrorhtml) on the item in question.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | Form item for which the HTML should be retrieved |
| error | [String](#type-string)|[Array](#type-array) | false | — | Error message to display for the item, or array of error message strings. |

### Groups

- validation

---
## Method: DynamicForm.setValuesManager

### Description
Binds this dynamicForm to a [valuesManager](#attr-dynamicformvaluesmanager) at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| valuesManager | [ValuesManager](#type-valuesmanager)|[GlobalId](../reference.md#type-globalid) | false | — | the ValuesManager that controls this form's values |

### Groups

- formValuesManager

---
## Method: DynamicForm.getErrorsHTML

### Description
If [DynamicForm.showInlineErrors](#attr-dynamicformshowinlineerrors) is false, the form will render all errors in a list at the top of the form. This method returns the HTML for this list of errors.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| errors | [Object](../reference.md#type-object) | false | — | Map of field names to error messages. Each field may contain a single error message (string) or an array of errors |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — error HTML.

### Groups

- validation

---
## Method: DynamicForm.fieldIsEditable

### Description
Can the field be edited? This method looks at [DynamicForm.canEdit](#attr-dynamicformcanedit) for the grid as well as the [FormItem.canEdit](FormItem.md#attr-formitemcanedit) value, to determine whether editing is actually allowed. For a detailed discussion, see the documentation at [DynamicForm.canEdit](#attr-dynamicformcanedit).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [FormItem](#type-formitem)|[number](#type-number)|[String](#type-string) | false | — | field object or identifier |

### Returns

`[boolean](../reference.md#type-boolean)` — whether field can be edited

### Groups

- editing

---
## Method: DynamicForm.sortItemsIntoTabOrder

### Description
Helper method to take our specified items and sort them into their desired tab sequence

Default behavior will respect explicitly specified tab index as a local tab index, otherwise just use specified order within the items array

### Returns

`[Array of FormItem](#type-array-of-formitem)` — Returns an array containing our items in the desired tab sequence.

---
## Method: DynamicForm.handleHiddenValidationErrors

### Description
Method to display validation error messages for fields that are not currently visible in this form.  
This will be called when validation fails for  
\- a hidden field in this form  
\- if this form is databound, a datasource field with specified validators, for which we have no specified form item.  
Implement this to provide custom validation error handling for these fields.  
By default hidden validation errors will be logged as warnings in the developerConsole. Return false from this method to suppress that behavior.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| errors | [Object](../reference.md#type-object) | false | — | The set of errors returned - this is an object of the form  
  `{fieldName:errors}`  
Where the 'errors' object is either a single string or an array of strings containing the error messages for the field. |

### Returns

`[boolean](../reference.md#type-boolean)` — false from this method to suppress that behavior

**Flags**: A

---
## Method: DynamicForm.setErrors

### Description
Setter for validation errors on this form. Errors passed in should be a Javascript object of the format  
`{fieldName1:errors, fieldName2:errors}`  
Where the `errors` value may be either a string (single error message) or an array of strings (if multiple errors should be applied to the field in question).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| errors | [Object](../reference.md#type-object) | false | — | list of errors as an object with the field names as keys |
| showErrors | [boolean](../reference.md#type-boolean) | false | — | If true redraw form to display errors now. Otherwise errors can be displayed by calling [DynamicForm.showErrors](#method-dynamicformshowerrors)  
Note: When the errors are shown, [handleHiddenValidationErrors()](#method-dynamicformhandlehiddenvalidationerrors) will be fired for errors on hidden fields, or with no associated formItem. |

### Groups

- errors

**Flags**: A

---
## Method: DynamicForm.setValue

### Description
Sets the value for some field

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | Name of the field being updated. A [DataPath](../reference_2.md#type-datapath) may be passed to set nested values |
| value | [String](#type-string) | false | — | New value. |

### Groups

- formValues

---
## Method: DynamicForm.setFields

### Description
Set the [items](#attr-dynamicformfields) for this DynamicForm. Takes an array of item definitions, which will be converted to [FormItem](FormItem.md#class-formitem)s and displayed in the form.

Note: Do not attempt to create [FormItem](FormItem.md#class-formitem) instances directly. This method should be passed the raw properties for each item only.

Objects passed to `setFields()` may not be reused in other forms and may not be used in subsequent calls to `setFields()` with the same form, new objects must be created instead.

To create a form where some items are conditionally present, rather than repeated calls to `setFields()` or `setItems()`, you should generally use [FormItem.hide](FormItem.md#method-formitemhide) and [FormItem.show](FormItem.md#method-formitemshow) and/or [FormItem.showIf](FormItem.md#method-formitemshowif) rather than calling `setItems() or setFields()`. `setItems()` and `setFields()` are appropriate for dynamically generated forms where there are few if any items that are the same each time the form is used.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| itemList | [Array of FormItem Properties](#type-array-of-formitem-properties) | false | — | list of new items to show in the form |

### Groups

- elements

---
## Method: DynamicForm.clearValues

### Description
Reset to default form values and clear errors

### Groups

- formValues

---
## Method: DynamicForm.cancelEditing

### Description
If the form or valuesManager has associated userTask workflow task than notify it about cancelling the changes.

---
## Method: DynamicForm.getChangedValues

### Description
Returns all values within this DynamicForm that have changed since [DynamicForm.rememberValues](#method-dynamicformremembervalues) last ran. Note that [DynamicForm.rememberValues](#method-dynamicformremembervalues) runs on dynamicForm initialization, and with every call to [DynamicForm.setValues](#method-dynamicformsetvalues) so this will typically contain all values the user has explicitly edited since then.

### Returns

`[Object](../reference.md#type-object)` — changed values in the form

### Groups

- formValues

### See Also

- [DynamicForm.getOldValues](#method-dynamicformgetoldvalues)

---
## Method: DynamicForm.getEventItem

### Description
If the current mouse event occurred over an item in this dynamicForm, returns that item.

### Returns

`[FormItem](#type-formitem)` — the current event target item

---
## Method: DynamicForm.setFieldErrors

### Description
Set field validation error\[s\] for some field.  
The errors parameter may be passed in as a string (a single error message), or an array of strings.  
The showErrors parameter allows the errors to be displayed immediately. Alternatively, an explicit call to [DynamicForm.showFieldErrors](#method-dynamicformshowfielderrors) will display the errors for this field.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | field to apply the new errors to |
| errors | [String](#type-string)|[Array of String](#type-array-of-string) | false | — | errors to apply to the field in question |
| show | [boolean](../reference.md#type-boolean) | false | — | If true this method will fall through to [DynamicForm.showFieldErrors](#method-dynamicformshowfielderrors) to update the display |

### Groups

- errors

---
## Method: DynamicForm.assignItemsTabPositions

### Description
This method is called automatically by the DynamicForm when the set of items changes and ensures that items show up in the correct tab order positions.

Makes use of [DynamicForm.sortItemsIntoTabOrder](#method-dynamicformsortitemsintotaborder) to order the items and ensures the items are ordered in the [TabIndexManager](TabIndexManager.md#class-tabindexmanager) correctly.

---
## Method: DynamicForm.getFocusItem

### Description
Return the current focus item for this form.

This is the item which either currently has focus, or if focus is not currently within this form, would be given focus on a call to [DynamicForm.focus](#method-dynamicformfocus). May return null if this form has never had focus, in which case a call to `form.focus()` would put focus into the first focusable item within the the form.

Note that if focus is currently in a sub-item of a [DateItem](DateItem.md#class-dateitem) or [RadioGroupItem](RadioGroupItem.md#class-radiogroupitem), this method will return the parent item, not the sub-item.

### Returns

`[FormItem](#type-formitem)` — Current focus item within this form. May be null.

### Groups

- eventHandling
- focus

### See Also

- [DynamicForm.isFocused](#method-dynamicformisfocused)
- [FormItem.isFocused](FormItem.md#method-formitemisfocused)

**Flags**: A

---
## Method: DynamicForm.clearErrors

### Description
Clears all errors for this DynamicForm.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| show | [boolean](../reference.md#type-boolean) | false | — | If true, redraw the form to clear any visible error messages. |

### Groups

- errors

---
## Method: DynamicForm.setSaveOperationType

### Description
Setter for the default [DSOperationType](../reference.md#type-dsoperationtype) when [DynamicForm.saveData](#method-dynamicformsavedata) is called. Note that this property can also be set by calling [DynamicForm.editRecord](#method-dynamicformeditrecord) or [DynamicForm.editNewRecord](#method-dynamicformeditnewrecord)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| operationType | [DSOperationType](../reference.md#type-dsoperationtype) | false | — | Operation type to use as a default. Valid values are `"add"` or `"update"`. |

---
## Method: DynamicForm.getEventItemInfo

### Description
If the current mouse event occurred over an item, or the title of an item in this dynamicForm, return details about where the event occurred.

### Returns

`[FormItemEventInfo](#type-formitemeventinfo)` — the current event target item details

---
## Method: DynamicForm.showItemContextMenu

### Description
Called when the mouse is right-clicked in some formItem. If the implementation returns false, default browser behavior is cancelled.

Note that it can be bad practice to cancel this method if the mouse is over the data element of an item, because doing so would replace the builtin browser-default menus that users may expect. You can use [DynamicForm.getEventItemInfo](#method-dynamicformgeteventiteminfo) to return an [info object](../reference_2.md#object-formitemeventinfo) that can be used to determine which part of the item is under the mouse.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | the form item showing its context menu |

### Returns

`[boolean](../reference.md#type-boolean)` — return false to cancel default behavior

### Groups

- eventHandling

---
## Method: DynamicForm.filterData

### Description
Retrieve data that matches the provided criteria, and edit the first record returned.  
Differs from [DynamicForm.fetchData](#method-dynamicformfetchdata) in that a case insensitive substring match will be performed against the criteria to retrieve the data.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | true | — | search criteria |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

---
## Method: DynamicForm.valueHoverHTML

### Description
Retrieves the HTML to display in a hover canvas when the user holds the mousepointer over some item's value. Return null to suppress the hover canvas altogether.  
Can be overridden by [FormItem.valueHoverHTML](FormItem.md#method-formitemvaluehoverhtml).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | Item the user is hovering over. |

### Groups

- Hovers

### See Also

- [FormItem.valueHoverHTML](FormItem.md#method-formitemvaluehoverhtml)

**Flags**: A

---
## Method: DynamicForm.validateData

### Description
`validateData()` can be used to check for errors in server-side validators without showing such errors to the user. Errors, if any, can be discovered by looking at the `DSResponse` object returned in the callback.

`validateData()` will first call [DynamicForm.validate](#method-dynamicformvalidate) to check for client-side errors, and will return `false` without contacting the server if errors are present. In this case, any errors detected client-side will be displayed; to avoid this and purely perform silent, server-side validation, you can use [DataSource.validateData](DataSource.md#method-datasourcevalidatedata) with the form's [current values](#method-dynamicformgetvalues). [DynamicForm.valuesAreValid](#method-dynamicformvaluesarevalid) can be used in lieu of a call to [DynamicForm.validate](#method-dynamicformvalidate) if silent checking of client-side errors is also desired.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional properties to set on the DSRequest that will be issued |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the server will be contacted, false otherwise

### Groups

- validation

---
## Method: DynamicForm.editRecord

### Description
Edit an existing record. Updates this editors values to match the values of the record passed in, via [DynamicForm.setValues](#method-dynamicformsetvalues).

This method will also call [DynamicForm.setSaveOperationType](#method-dynamicformsetsaveoperationtype) to ensure subsequent calls to `saveData()` will use an `update` rather than an `add` operation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | the record to be edited as a map of field names to their corresponding values |

### Groups

- dataBoundComponentMethods

### See Also

- [DynamicForm.saveData](#method-dynamicformsavedata)

---
## Method: DynamicForm.getOldValues

### Description
Returns the set of values last stored by [DynamicForm.rememberValues](#method-dynamicformremembervalues). Note that `rememberValues()` is called automatically by [DynamicForm.setValues](#method-dynamicformsetvalues), and on form initialization, so this typically contains all values as they were before the user edited them.

### Returns

`[Object](../reference.md#type-object)` — old values in the form

### Groups

- formValues

### See Also

- [DynamicForm.getChangedValues](#method-dynamicformgetchangedvalues)

---
## Method: DynamicForm.setReadOnlyDisplay

### Description
Setter for the [DynamicForm.readOnlyDisplay](#attr-dynamicformreadonlydisplay) attribute.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| appearance | [ReadOnlyDisplayAppearance](../reference.md#type-readonlydisplayappearance) | false | — | New read-only display appearance. |

---
## Method: DynamicForm.submit

### Description
`submit()` is automatically called when a [SubmitItem](../reference.md#class-submititem) included in the form is clicked, or, if [saveOnEnter](#attr-dynamicformsaveonenter) is set, when the "Enter" key is pressed in a text input. Submit can also be manually called.

If this form is part of a [ValuesManager](ValuesManager.md#class-valuesmanager), this method will simply fall through to the submit method on the valuesManager. If not, and [form.submitValues()](#method-dynamicformsubmitvalues) exists, it will be called, and no further action will be taken.

Otherwise, default behavior varies based on [form.canSubmit](#attr-dynamicformcansubmit): if `canSubmit` is false, [DynamicForm.saveData](#method-dynamicformsavedata) will be called to handle saving via SmartClient databinding.

If `canSubmit` is true, the form will be submitted like an ordinary HTML form via [DynamicForm.submitForm](#method-dynamicformsubmitform).

The parameters to `submit()` apply only if `submit()` will be calling [DynamicForm.saveData](#method-dynamicformsavedata). If you override `submit()`, you can safely ignore the parameters as SmartClient framework code does not pass them.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion. \[Ignored if this.canSubmit is true\] |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued \[Ignored if this.canSubmit is true\] |

### Groups

- dataBoundComponentMethods

### See Also

- [DynamicForm.submitValues](#method-dynamicformsubmitvalues)

---
## Method: DynamicForm.getTitleOrientation

### Description
Return the orientation of the title for a specific item or the default title orientation if no item is passed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | true | — | item to check |

### Returns

`[TitleOrientation](../reference.md#type-titleorientation)` — orientation of the title, or null if an item is passed and has no title

**Flags**: A

---
## Method: DynamicForm.getValues

### Description
An Object containing the values of the form as properties, where each propertyName is the name of a [form item](../reference.md#kb-topic-form-items) in the form, and each property value is the value held by that form item.

Note that modifying the returned object is not a supported way of adding or modifying values. Instead use [DynamicForm.setValue](#method-dynamicformsetvalue) or [DynamicForm.setValues](#method-dynamicformsetvalues).

### Returns

`[Object](../reference.md#type-object)` — values in the form

### Groups

- formValues

### See Also

- [ValuesManager.getValues](ValuesManager.md#method-valuesmanagergetvalues)

---
## Method: DynamicForm.valuesHaveChanged

### Description
Compares the current set of values with the values stored by the call to the [DynamicForm.rememberValues](#method-dynamicformremembervalues) method. `rememberValues()` runs when the form is initialized and on every call to [DynamicForm.setValues](#method-dynamicformsetvalues). Returns true if the values have changed, and false otherwise.

### Returns

`[Boolean](#type-boolean)` — true if current values do not match remembered values

### Groups

- formValues

### See Also

- [DynamicForm.getChangedValues](#method-dynamicformgetchangedvalues)
- [DynamicForm.getOldValues](#method-dynamicformgetoldvalues)

---
## Method: DynamicForm.hasFieldErrors

### Description
Returns whether there are currently any errors visible to the user for the specified field in this form, without performing any validation.

Note that validation errors are set up automatically by validation (see [DynamicForm.validate](#method-dynamicformvalidate)), or may be explicitly set via [DynamicForm.setErrors](#method-dynamicformseterrors) or [DynamicForm.setFieldErrors](#method-dynamicformsetfielderrors).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | field to test for validation errors |

### Returns

`[Boolean](#type-boolean)` — true if the form has outstanding errors for the field in question.

### Groups

- errors

---
## Method: DynamicForm.editSelectedData

### Description
Edit the record selected in the specified selection component (typically a [ListGrid](ListGrid_1.md#class-listgrid)).

Updates the values of this editor to match the selected record's values.

If this form has a dataSource, then saving via [DynamicForm.saveData](#method-dynamicformsavedata) will use the "update" operation type.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| selectionComponent | [ListGrid](#type-listgrid)|[TileGrid](#type-tilegrid)|[ID](#type-id) | false | — | the ListGrid or TileGrid or ID of a [ListGrid](ListGrid_1.md#class-listgrid)/[TileGrid](TileGrid.md#class-tilegrid) whose currently record(s) is/are to be edited |

### Groups

- dataBoundComponentMethods

### See Also

- [DynamicForm.saveData](#method-dynamicformsavedata)

---
## Method: DynamicForm.setValues

### Description
Replaces the current values of the entire form with the values passed in.

Note: when working with a form that is saving to a DataSource, you would typically call either [DynamicForm.editRecord](#method-dynamicformeditrecord) for an existing record, or [DynamicForm.editNewRecord](#method-dynamicformeditnewrecord) for a new record. In addition to setting the current values of the form, these APIs establish the [DSRequest.operationType](DSRequest.md#attr-dsrequestoperationtype) used to save ("update" vs "add").

Values should be provided as an Object containing the new values as properties, where each propertyName is the name of a [form item](../reference.md#kb-topic-form-items) in the form, and each property value is the value to apply to that form item via [FormItem.setValue](FormItem.md#method-formitemsetvalue).

Values with no corresponding form item may also be passed, will be tracked by the form and returned by subsequent calls to [DynamicForm.getValues](#method-dynamicformgetvalues).

Any [FormItem](FormItem.md#class-formitem) for which a value is not provided will revert to its [defaultValue](FormItem.md#attr-formitemdefaultvalue). To cause all FormItems to revert to default values, pass null.

This method also calls [DynamicForm.rememberValues](#method-dynamicformremembervalues) so that a subsequent later call to [DynamicForm.resetValues](#method-dynamicformresetvalues) will revert to the passed values.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newData | [Object](../reference.md#type-object) | true | — | values for the form, or null to reset all items to default values |

### Groups

- formValues

---
## Method: DynamicForm.getFieldErrors

### Description
Returns any errors that are currently visible to the user for the specified field in this form, without performing validation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | fieldName to check for errors |

### Returns

`[String](#type-string)|[Array of String](#type-array-of-string)` — Error message string, or if there is more than one error associated with this field, array of error message strings.

### Groups

- errors

---
## Method: DynamicForm.addFieldErrors

### Description
Adds field validation error\[s\] to the specified field. Errors passed in will be added to any existing errors on the field caused by validation or a previous call to this method.  
The errors parameter may be passed in as a string (a single error message), or an array of strings.  
The showErrors parameter allows the errors to be displayed immediately. Alternatively, call [DynamicForm.showFieldErrors](#method-dynamicformshowfielderrors) to display the errors for this field.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | field to apply the new errors to |
| errors | [String](#type-string)|[Array of String](#type-array-of-string) | false | — | errors to apply to the field in question |
| show | [boolean](../reference.md#type-boolean) | false | — | If true this method will fall through to [DynamicForm.showFieldErrors](#method-dynamicformshowfielderrors) to update the display |

### Groups

- errors

---
## Method: DynamicForm.setTitleOrientation

### Description
Modify this form's [TitleOrientation](../reference.md#type-titleorientation) at runtime

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| orientation | [TitleOrientation](../reference.md#type-titleorientation) | false | — | new default item titleOrientation |

### Groups

- formTitles

---
## Method: DynamicForm.showItem

### Description
Show a form item via [FormItem.show](FormItem.md#method-formitemshow)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| itemName | [String](#type-string) | false | — | Name of the item to show |

### Groups

- formValues

---
## Method: DynamicForm.getFields

### Description
Method to retrieve the [items](#attr-dynamicformfields) for this DynamicForm.

### Returns

`[Array of FormItem](#type-array-of-formitem)` — —

### Groups

- elements

---
## Method: DynamicForm.cancel

### Description
This method exists for clean integration with existing server frameworks that have a 'cancel' feature which typically clears session state associated with the form. When this method is called, an RPC is sent to the server. You must pass the appropriate params property in the request properties as required by your server framework.

For example:

```
 var requestProperties = {
     params: {CANCEL: "cancel"}
 };
 
```
Note that no other form data is sent. By default the current top-level page is replaced with the reply. If you wish to ignore the server reply instead, include the following request properties:
```
 var requestProperties = { 
     // other props ...
     ignoreTimeout: true,
     target: null
 };
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| requestProperties | [DSRequest](#type-dsrequest) | false | — | additional properties to set on the RPCRequest that will be issued |

### Groups

- submitting

### See Also

- [DynamicForm.cancelEditing](#method-dynamicformcancelediting)

**Deprecated**

---
## Method: DynamicForm.rememberValues

### Description
Make a snapshot of the current set of values, so we can reset to them later. Creates a new object, then adds all non-method properties of values to the new object. Use `resetValues()` to revert to these values. Note that this method is automatically called when the values for this form are set programmatically via a call to [DynamicForm.setValues](#method-dynamicformsetvalues).

### Returns

`[Object](../reference.md#type-object)` — copy of current form values

### Groups

- formValues

---
## Method: DynamicForm.completeEditing

### Description
Finish editing and store edited values in [process state](Process.md#attr-processstate).

---
## Method: DynamicForm.setValueMap

### Description
Set the valueMap for a specified item

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| itemName | [String](#type-string) | false | — | itemName of the item upon which the valueMap should be set. |
| valueMap | [ValueMap](../reference_2.md#type-valuemap) | false | — | new valueMap for the field in question. |

### Groups

- formValues

---
## Method: DynamicForm.setHilites

### Description
Only supported on ListGrid for now.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| hilites | [Array of Hilite](#type-array-of-hilite) | false | — | Array of hilite objects |

### Groups

- hiliting

---
## Method: DynamicForm.fetchRelatedData

### Description
Based on the relationship between the DataSource this component is bound to and the DataSource specified as the "schema" argument, call fetchData() to retrieve records in this data set that are related to the passed-in record.

Relationships between DataSources are declared via [DataSourceField.foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey).

For example, given two related DataSources "orders" and "orderItems", where we want to fetch the "orderItems" that belong to a given "order". "orderItems" should declare a field that is a [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) to the "orders" table (for example, it might be named "orderId" with foreignKey="orders.id"). Then, to load the records related to a given "order", call fetchRelatedData() on the component bound to "orderItems", pass the "orders" DataSource as the "schema" and pass a record from the "orders" DataSource as the "record" argument.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | DataSource record |
| schema | [Canvas](#type-canvas)|[DataSource](#type-datasource)|[ID](#type-id) | false | — | schema of the DataSource record, or DataBoundComponent already bound to that schema |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

---
## Method: DynamicForm.showErrors

### Description
If this form has any outstanding validation errors, show them now.  
This method is called when the set of errors is changed by [DynamicForm.setErrors](#method-dynamicformseterrors) or [DynamicForm.validate](#method-dynamicformvalidate).  
Default implementation will redraw the form to display error messages and call [handleHiddenValidationErrors()](#method-dynamicformhandlehiddenvalidationerrors) to display errors with no visible field.  
Note that this method may be overridden to perform custom display of validation errors.

### Groups

- errors

---
## Method: DynamicForm.getValue

### Description
Returns the value stored in the form for some field.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | name of the field for which you're retrieving a value. Nested values may be retrieved by passing in a [DataPath](../reference_2.md#type-datapath) |

### Returns

`[Any](#type-any)` — value of the field

### Groups

- formValues

---
## Method: DynamicForm.hasErrors

### Description
Returns whether there are currently any errors visible to the user for this form, without performing validation.

Note that validation errors are set up automatically by validation (see [DynamicForm.validate](#method-dynamicformvalidate)), or may be explicitly set via [DynamicForm.setErrors](#method-dynamicformseterrors) or [DynamicForm.setFieldErrors](#method-dynamicformsetfielderrors).

### Returns

`[Boolean](#type-boolean)` — true if the form currently has validation errors.

### Groups

- errors

---
## Method: DynamicForm.getValuesAsCriteria

### Description
Return search criteria based on the current set of values within this form.

The returned search criteria will be a simple [Criteria](../reference_2.md#type-criteria) object, except for in the following cases, in which case an [AdvancedCriteria](../reference.md#object-advancedcriteria) object will be returned:

*   The `advanced` parameter may be passed to explicitly request a `AdvancedCriteria` object be returned
*   If [DynamicForm.setValuesAsCriteria](#method-dynamicformsetvaluesascriteria) was called with an `AdvancedCriteria` object, this method will return advanced criteria.
*   If [DynamicForm.operator](#attr-dynamicformoperator) is set to `"or"` rather than `"and"` the generated criteria will always be advanced.
*   If any item within this form returns true for [FormItem.hasAdvancedCriteria](FormItem.md#method-formitemhasadvancedcriteria), which can be caused by setting [FormItem.operator](FormItem.md#attr-formitemoperator), and is always true for items such as [DateRangeItem](DateRangeItem.md#class-daterangeitem)
*   If [FormItem.allowExpressions](FormItem.md#attr-formitemallowexpressions) is enabled

The criteria returned will be picked up from the current values for this form. For simple criteria, each form item simply maps its value to it's fieldName. See [FormItem.getCriterion](FormItem.md#method-formitemgetcriterion) for details on how form items generate advanced criteria. Note that any values or criteria specified via [DynamicForm.setValues](#method-dynamicformsetvalues) or [DynamicForm.setValuesAsCriteria](#method-dynamicformsetvaluesascriteria) which do not correspond to an item within the form will be combined with the live item values when criteria are generated.

The returned criteria object can be used to filter data via methods such as [ListGrid.fetchData](ListGrid_1.md#method-listgridfetchdata), [DataSource.fetchData](DataSource.md#method-datasourcefetchdata), or, for more advanced usage, [ResultSet.setCriteria](ResultSet.md#method-resultsetsetcriteria).

Note that any form field which the user has left blank is omitted as criteria, that is, a blank field is assumed to mean "allow any value for this field" and not "this field must be blank". Examples of empty values include a blank text field or SelectItem with an empty selection.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| advanced | [boolean](../reference.md#type-boolean) | false | — | if true, return an [AdvancedCriteria](../reference.md#object-advancedcriteria) object even if the form item values could be represented in a simple [Criterion](../reference_2.md#object-criterion) object. |
| textMatchStyle | [TextMatchStyle](../reference.md#type-textmatchstyle) | true | — | This parameter may be passed to indicate whether the criteria are to be applied to a substring match (filter) or exact match (fetch). When advanced criteria are returned this parameter will cause the appropriate `operator` to be generated for individual fields' criterion clauses. |

### Returns

`[Criteria](../reference_2.md#type-criteria)|[AdvancedCriteria](#type-advancedcriteria)` — a [Criteria](../reference_2.md#type-criteria) object, or [AdvancedCriteria](../reference.md#object-advancedcriteria)

### Groups

- criteriaEditing

---
## Method: DynamicForm.getValidatedValues

### Description
Call [DynamicForm.validate](#method-dynamicformvalidate) to check for validation errors. If no errors are found, return the current values for this form, otherwise return null.

### Returns

`[Object](../reference.md#type-object)` — current values or null if validation failed.

### Groups

- errors

---
## Method: DynamicForm.titleClipped

### Description
Is the title for the given form item clipped? The form item must have title clipping enabled.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | the form item. |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the title is clipped; false otherwise.

### See Also

- [DynamicForm.clipItemTitles](#attr-dynamicformclipitemtitles)
- [FormItem.clipTitle](FormItem.md#attr-formitemcliptitle)

---
## Method: DynamicForm.saveData

### Description
Validate and then save the form's current values to the [DataSource](DataSource.md#class-datasource) this form is bound to.

If client-side validators are defined, they are executed first, and if any errors are found the save is aborted and the form will show the errors.

If client-side validation passes, a [DSRequest](../reference.md#object-dsrequest) will be sent, exactly as though [DataSource.addData](DataSource.md#method-datasourceadddata) or [DataSource.updateData](DataSource.md#method-datasourceupdatedata) had been called with ${isc.DocUtils.linkForRef('method:DynamicForm.getValues','the form\\'s values')} as data. The [DSRequest.operationType](DSRequest.md#attr-dsrequestoperationtype) will be either "update" or "add", depending on the current [DynamicForm.saveOperationType](#attr-dynamicformsaveoperationtype).

On either a client-side or server-side validation failure, validation errors will be displayed in the form. Visible items within a DynamicForm will be redrawn to display errors. Validation failure occurring on hidden items, or DataSource fields with no associated form items may be handled via [DynamicForm.handleHiddenValidationErrors](#method-dynamicformhandlehiddenvalidationerrors) or [ValuesManager.handleHiddenValidationErrors](ValuesManager.md#method-valuesmanagerhandlehiddenvalidationerrors).

In the case of a validation error, the callback will **not** be called by default since the form has already handled the failed save by displaying the validation errors to the user. If you need to do something additional in this case, you can set [RPCRequest.willHandleError](RPCRequest.md#attr-rpcrequestwillhandleerror) via the `requestProperties` parameter to force your callback to be invoked. However, first consider:

*   if you are trying to customize display of validation errors, there are several [built-in modes](#attr-dynamicformshowerroricons) and [DynamicForm.showErrors](#method-dynamicformshowerrors) may be a better place to put customizations.
*   for unrecoverable general errors (eg server is down), [central error handling](RPCManager.md#classmethod-rpcmanagerhandleerror) in invoked, so consider placing customizations there unless an unrecoverable error should be handled specially by this specific form.

**Note:** If a form is to be cleared after saving data, we recommend clearing the form from the callback rather than calling saveData() and then synchronously clearing the form. This gives users a chance to view and respond to any validation errors returned by the server. It is also required to ensure forms containing an [upload field](FileItem.md#class-fileitem), have a chance to upload the file to the server.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

---
## Method: DynamicForm.isNewRecord

### Description
Returns true if [DynamicForm.saveOperationType](#attr-dynamicformsaveoperationtype) is currently "add". See [DynamicForm.saveOperationType](#attr-dynamicformsaveoperationtype).

### Returns

`[Boolean](#type-boolean)` — whether this form will use an "add" operation when saving

---
## Method: DynamicForm.formSubmitFailed

### Description
Method called when an attempt to [natively submit](#method-dynamicformsubmitform) a form is unable to submit to the server. Default behavior is to display the [DynamicForm.formSubmitFailedWarning](#attr-dynamicformformsubmitfailedwarning) in a warning dialog. The most common cause for this failure is that the user has typed an invalid file-path into an upload type field.

**Note:** This is very unlikely to occur with modern versions of IE, which don't allow the path of a file to be edited by hand (only selected via file navigation). It was last seen in IE6-7 under Windows XP.

Rather than throwing an exception on the client during submit(), normally all failures in native form submission are handled by the server. For further information, see [File Uploading](../kb_topics/upload.md#kb-topic-uploading-files).

### Groups

- i18nMessages

**Deprecated**

**Flags**: A

---
## Method: DynamicForm.handleAsyncValidationReply

### Description
Notification fired when an asynchronous validation completes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| success | [boolean](../reference.md#type-boolean) | false | — | true if validation succeeded, false if it failed |
| errors | [Object](../reference.md#type-object) | false | — | Map of errors by fieldName. Will be null if validation succeeded. |

---
## Method: DynamicForm.getErrors

### Description
Returns any errors that are currently visible to the user for this form, without performing validation.

### Returns

`[Object](../reference.md#type-object)` — Errors are returned as an object of the format  
`{fieldName:errors, fieldName:errors}`  
where each `errors` object will be either an error message string or an array of error message strings.

### Groups

- errors

---
## Method: DynamicForm.setMethod

### Description
Sets the [method](#attr-dynamicformmethod) for this form.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| method | [FormMethod](../reference.md#type-formmethod) | false | — | html form submission method (get or post) |

---
## Method: DynamicForm.getItems

### Description
Method to retrieve the [items](#attr-dynamicformfields) for this DynamicForm.

### Returns

`[Array of FormItem](#type-array-of-formitem)` — —

### Groups

- elements

---
## Method: DynamicForm.submitForm

### Description
Submits the form to the URL defined by [DynamicForm.action](#attr-dynamicformaction), identically to how a plain HTML `<form>` element would submit data, as either an HTTP GET or POST as specified by [DynamicForm.method](#attr-dynamicformmethod).

**Notes:**

*   this is used only in the very rare case that a form is used to submit data directly to a URL. Normal server contact is through [DataBound Component Methods](../kb_topics/dataBoundComponentMethods.md#kb-topic-databound-component-methods).
*   For this method to reliably include values for every field in the grid, [DynamicForm.canSubmit](#attr-dynamicformcansubmit) must be set to `true`
*   To submit values for fields that do not have an editor, use [HiddenItem](HiddenItem.md#class-hiddenitem) with a [FormItem.defaultValue](FormItem.md#attr-formitemdefaultvalue) set. This is analogous to `<input type="hidden">` in HTML forms.

### Groups

- submitting

---
## Method: DynamicForm.setValuesAsCriteria

### Description
This method will display the specified criteria in this form for editing. The criteria parameter may be a simple [Criterion](../reference_2.md#object-criterion) object or an [AdvancedCriteria](../reference.md#object-advancedcriteria) object.

For simple criteria, the specified fieldName will be used to apply criteria to form items, as with a standard setValues() call.

For AdvancedCriteria, behavior is as follows:

*   If the top level operator doesn't match the [operator](#attr-dynamicformoperator) for this form, the entire criteria will be nested in an outer advanced criteria object with the appropriate operator.
*   Each criterion within AdvancedCriteria will be applied to a form item if [FormItem.shouldSaveValue](FormItem.md#attr-formitemshouldsavevalue) is true for the item and [FormItem.canEditCriterion](FormItem.md#method-formitemcaneditcriterion) returns true for the criterion in question. By default this method checks for a match with both the `fieldName` and `operator` of the criterion. The criterion is actually passed to the item for editing via [FormItem.setCriterion](FormItem.md#method-formitemsetcriterion) . Note that these methods may be overridden for custom handling. Also note that the default [CanvasItem.setCriterion](CanvasItem.md#method-canvasitemsetcriterion) implementation handles editing nested criteria via embedded dynamicForms.
*   Criteria which don't map to any form item will be stored directly on the form and recombined with the edited values from each item when [DynamicForm.getValuesAsCriteria](#method-dynamicformgetvaluesascriteria) is called.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criterion](#type-criterion) | false | — | criteria to edit. |

### Groups

- criteriaEditing

---
## Method: DynamicForm.checkForValidationErrors

### Description
Performs silent validation of the current form values, like [DynamicForm.valuesAreValid](#method-dynamicformvaluesarevalid). In contrast to [DynamicForm.valuesAreValid](#method-dynamicformvaluesarevalid), this method allows checking for server-side errors, and finding out what the errors are.

The callback must be passed unless server-side validation is being skipped, and If passed, it always fires, errors or not, firing synchronously if server validation is skipped.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [ValidationStatusCallback](#type-validationstatuscallback) | false | — | callback to invoke after validation is complete |
| validateHiddenFields | [boolean](../reference.md#type-boolean) | true | — | should validators be processed for non-visible fields such as dataSource fields with no associated item or fields with visibility set to `"hidden"` |
| skipServerValidation | [boolean](../reference.md#type-boolean) | true | — | whether to skip doing server-side validation |

### Returns

`[Map](#type-map)` — null if server-side validation is required, or no errors are present; otherwise, an object mapping field names to the associated errors, for those fields that failed validation.

### Groups

- validation

---
## Method: DynamicForm.setError

### Description
Sets error message(s) for the specified itemName to the error string or array of strings. You must call form.markForRedraw() to display the new error message(s).  
**Note:** you can call this multiple times for an individual itemName which will result in an array of errors being remembered.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| itemName | [String](#type-string) | false | — | name of the item to set |
| errorMessage | [String](#type-string)|[Array](#type-array) | false | — | error message string or array of strings |

### Groups

- errors

**Deprecated**

**Flags**: A

---
## Method: DynamicForm.clearValue

### Description
Clears the value for some field via a call to [FormItem.clearValue](FormItem.md#method-formitemclearvalue) if appropriate. If there is no item associated with the field name, the field will just be cleared within our stored set of values.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | Name of the field being cleared. A [DataPath](../reference_2.md#type-datapath) may be used for clearing details of nested data structures. |

---
## Method: DynamicForm.itemChanged

### Description
Handler fired when there is a changed() event fired on a FormItem within this form.

Fires after the change() handler on the FormItem itself, and only if the item did not cancel the change event and chooses to allow it to propagate to the form as a whole.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | the FormItem where the change event occurred |
| newValue | [Any](#type-any) | false | — | new value for the FormItem |

---
## Method: DynamicForm.viewSelectedData

### Description
Displays the currently selected record(s) of the selectionComponent widget (typically a listGrid) in this component.

For a DynamicForm the first record of the selection is shown after the form is placed into [read-only mode](#attr-dynamicformcanedit). A subsequent call to [DynamicForm.editRecord](#method-dynamicformeditrecord) or similar will return the form to editability.

Note that since field-level `canEdit:true` settings override the form-level canEdit setting the automatic change to read-only may not change every field.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| selectionComponent | [ListGrid](#type-listgrid)|[TileGrid](#type-tilegrid)|[ID](#type-id) | false | — | the ListGrid or TileGrid or ID of a [ListGrid](ListGrid_1.md#class-listgrid)/[TileGrid](TileGrid.md#class-tilegrid) whose currently selected record(s) is/are to be viewed |

### Groups

- dataBoundComponentMethods

---
## Method: DynamicForm.reset

### Description
Resets values to the state it was the last time `setValues()` or `rememberValues()` was called. If neither of those methods has been called, values will be set back to their initial values at init time.

### Groups

- formValues

---
## Method: DynamicForm.editNewRecord

### Description
Prepare to edit a new record by clearing the current set of values (or replacing them with initialValues if specified).  
This method will also call [DynamicForm.setSaveOperationType](#method-dynamicformsetsaveoperationtype) to ensure subsequent calls to `saveData()` will use an `add` rather than an `update` operation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| initialValues | [Record](#type-record)|[Object](../reference.md#type-object) | true | — | initial set of values for the editor as a map of field names to their corresponding values |

### Groups

- dataBoundComponentMethods

### See Also

- [DynamicForm.saveData](#method-dynamicformsavedata)

---
## Method: DynamicForm.itemHoverHTML

### Description
Retrieves the HTML to display in a hover canvas when the user holds the mouse pointer over some item. Return null to suppress the hover canvas altogether.  
Default implementation returns the prompt for the item if defined.  
Can be overridden via `item.itemHoverHTML()`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | Item the user is hovering over. |

### Groups

- Hovers

### See Also

- [FormItem.prompt](FormItem.md#attr-formitemprompt)
- [FormItem.itemHoverHTML](FormItem.md#method-formitemitemhoverhtml)

**Flags**: A

---
## Method: DynamicForm.hideItem

### Description
Hide a form item via [FormItem.hide](FormItem.md#method-formitemhide)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| itemName | [String](#type-string) | false | — | Name of the item to show |

### Groups

- formValues

---
## Method: DynamicForm.isFocused

### Description
Returns true if this DynamicForm has the keyboard focus.

Unlike standard canvases, for a DynamicForm this method will return true when keyboard focus is currently on one of the form's [items](#attr-dynamicformitems).

Note that in some cases the items of a form may be written directly into a different [canvas](FormItem.md#attr-formitemcontainerwidget). In this case the dynamicForm containing the items may not have been drawn on the page itself, but this method can still return true if one of the items has focus.

### Returns

`[Boolean](#type-boolean)` — whether focus is currently in one of this form's items.

---
## Method: DynamicForm.titleHoverHTML

### Description
Retrieves the HTML to display in a hover canvas when the user holds the mouse pointer over some item's title. Return null to suppress the hover canvas altogether.  
Default implementation returns the prompt for the item if defined. If no prompt is defined and the item title is clipped, the item title will be shown in a hover by default.  
Can be overridden by [FormItem.titleHoverHTML](FormItem.md#method-formitemtitlehoverhtml).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | Item the user is hovering over. |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML to be displayed in the hover

### Groups

- Hovers

### See Also

- [FormItem.prompt](FormItem.md#attr-formitemprompt)
- [FormItem.titleHoverHTML](FormItem.md#method-formitemtitlehoverhtml)

**Flags**: A

---
## Method: DynamicForm.itemChange

### Description
Handler fired when there is a change() event fired on a FormItem within this form.

Fires after the change() handler on the FormItem itself, and only if the item did not cancel the change event and chooses to allow it to propagate to the form as a whole.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | the FormItem where the change event occurred |
| newValue | [Any](#type-any) | false | — | new value for the FormItem |
| oldValue | [Any](#type-any) | false | — | value the FormItem had previous to this change() event |

### Returns

`[boolean](../reference.md#type-boolean)` — return false to cancel the change, or true to allow it

---
## Method: DynamicForm.setCanEdit

### Description
Is this form editable or read-only? Setting the form to non-editable causes all form items to render as read-only unless a form item is specifically marked as editable (the item's [canEdit](FormItem.md#attr-formitemcanedit) attribute is `true`).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canEdit | [boolean](../reference.md#type-boolean) | false | — | Can this form be edited? |

### Groups

- readOnly

### See Also

- [DynamicForm.canEdit](#attr-dynamicformcanedit)

---
## Method: DynamicForm.resetValues

### Description
Same as [DynamicForm.reset](#method-dynamicformreset).

### Groups

- formValues

---
## Method: DynamicForm.clearFieldErrors

### Description
Clear any validation errors on the field passed in.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | field to clear errors from |
| show | [boolean](../reference.md#type-boolean) | false | — | If true this method will fall through to [DynamicForm.showFieldErrors](#method-dynamicformshowfielderrors) to update the display |

### Groups

- errors

---
## Method: DynamicForm.setItems

### Description
Synonym for [DynamicForm.setFields](#method-dynamicformsetfields)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| itemList | [Array of FormItem Properties](#type-array-of-formitem-properties) | false | — | list of new items to show in the form |

### Groups

- elements

---
## Method: DynamicForm.focusInItem

### Description
Move the keyboard focus into a particular item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| itemName | [number](#type-number)|[ItemName](#type-itemname)|[FormItem](#type-formitem) | false | — | Item (or reference to) item to focus in. |

### Groups

- eventHandling
- focus

---
## Method: DynamicForm.submitValues

### Description
Triggered when a SubmitItem is included in the form is submitted and gets pressed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| values | [Object](../reference.md#type-object) | false | — | the form values |
| form | [DynamicForm](#type-dynamicform) | false | — | the form being submitted |

### Groups

- submitting

### See Also

- [DynamicForm.submit](#method-dynamicformsubmit)

---
## Method: DynamicForm.validate

### Description
Validates the form without submitting it, and redraws the form to display error messages if there are any validation errors. Returns true if validation succeeds, or false if validation fails.

For databound forms, any [DataSource](DataSource.md#class-datasource) field validators will be run even if there is no associated item in the form. Validators will also be run on hidden form items. In both these cases, validation failure can be handled via [DynamicForm.handleHiddenValidationErrors](#method-dynamicformhandlehiddenvalidationerrors).

If this form has any fields which require server-side validation (see [Validator.serverCondition](Validator.md#attr-validatorservercondition)) this will also be initialized. Such validation will occur asynchronously. Developers can use [DynamicForm.isPendingAsyncValidation](#method-dynamicformispendingasyncvalidation) and [DynamicForm.handleAsyncValidationReply](#method-dynamicformhandleasyncvalidationreply) to detect and respond to asynchronous validation.

Note that for silent validation, [DynamicForm.valuesAreValid](#method-dynamicformvaluesarevalid) (client-side) and [DynamicForm.checkForValidationErrors](#method-dynamicformcheckforvalidationerrors) (client and server-side) can be used instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| validateHiddenFields | [boolean](../reference.md#type-boolean) | true | — | Should validators be processed for non-visible fields such as dataSource fields with no associated item or fields with visibility set to `"hidden"`? |

### Returns

`[boolean](../reference.md#type-boolean)` — true if validation succeeds, or false if validation fails.

### Groups

- validation

### See Also

- [ValuesManager.validate](ValuesManager.md#method-valuesmanagervalidate)

---
## Method: DynamicForm.valuesChanged

### Description
Handler fired when the entire set of values is replaced, as by a call to [DynamicForm.setValues](#method-dynamicformsetvalues), [DynamicForm.resetValues](#method-dynamicformresetvalues) or [DynamicForm.editRecord](#method-dynamicformeditrecord).

Note that it is invalid to call such methods from this handler because doing so would result in an infinite loop.

---
