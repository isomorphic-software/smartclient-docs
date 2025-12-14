# Grid Editing

[← Back to API Index](../reference.md)

---

## KB Topic: Grid Editing

### Description
Data being displayed by a grid may be edited within the grid, by showing editing interfaces embedded inside the cells of the grid.

**Enabling editing**

Editing is enabled when [canEdit](../classes/ListGrid_1.md#attr-listgridcanedit) is `true`. When enabled, the user can begin editing via the [editEvent](../classes/ListGrid_1.md#attr-listgrideditevent), typically click or double-click. Editing can also be triggered programmatically by a call to [startEditing()](../classes/ListGrid_2.md#method-listgridstartediting) or [startEditingNew()](../classes/ListGrid_2.md#method-listgridstarteditingnew).

**New record creation**

By default, editing is restricted to existing records. Setting [ListGrid.listEndEditAction](../classes/ListGrid_1.md#attr-listgridlistendeditaction) to "next" allows the user to create new records by simply navigating off the end of the dataset with the keyboard. Editing of new records can also be initiated with [ListGrid.startEditingNew](../classes/ListGrid_2.md#method-listgridstarteditingnew), for example, from a button outside the grid. See the [Unsaved Records Overview](unsavedRecords.md#kb-topic-handling-unsaved-records) for special concerns when dealing with unsaved records.

**Saving changes**

Saving of changes is triggered automatically when the user navigates out of the row or cell being edited (based on [ListGrid.saveByCell](../classes/ListGrid_1.md#attr-listgridsavebycell)) or when the user ends editing. For a "mass update" interface, automatic saving of changes can be disabled entirely via [autoSaveEdits:false](../classes/ListGrid_1.md#attr-listgridautosaveedits), in which case a manual call to [saveEdits()](../classes/ListGrid_2.md#method-listgridsaveedits) or [saveAllEdits()](../classes/ListGrid_1.md#method-listgridsavealledits) is required to trigger saving.

If a grid has no DataSource, saving means that the properties of the [ListGridRecord](../reference_2.md#object-listgridrecord)s in [grid.data](../classes/ListGrid_1.md#attr-listgriddata) are directly changed.

For a grid with a DataSource, saving will be accomplished by using DataSource "update" operations for existing records, and DataSource "add" operations for new records. If multiple records have been edited and [saveAllEdits()](../classes/ListGrid_1.md#method-listgridsavealledits) is called, [request queuing](../classes/RPCManager.md#classmethod-rpcmanagerstartqueue) will be automatically used to enable all edits to be saved in one HTTP turnaround (if using the SmartClient Server).

By default, a grid will send only updated fields and primaryKey fields as part of [DSRequest.data](../classes/DSRequest.md#attr-dsrequestdata) so that the server can discern which fields the user actually changed. However, the grid always includes the original field values in the dsRequest as [DSRequest.oldValues](../classes/DSRequest.md#attr-dsrequestoldvalues).

Note that although it is possible to load DataSource data without actually declaring a [primaryKey field](../classes/DataSourceField.md#attr-datasourcefieldprimarykey), a primaryKey must be declared for editing and saving. The values of primaryKey fields is how SmartClient identifies the changed record to the server.

**Saving edits in a sorted data set:** When a user updates or adds a record in a sorted listGrid, the data set may be automatically [unsorted](../classes/ListGrid_1.md#method-listgridunsort). When this happens, the sort indicator will be removed from sort field headers, and all rows will stay in their current positions, including edited records where the sort field value has been changed.  
Note that for a databound grid with a partial data set, a "true unsort" isn't possible without droppping the cache, as both client and server need to agree on the positions of rows. In this case the grid is marked as unsorted, and all visible rows stay in place until the next fetch occurs, at which point the cache is dropped and a truly unsorted data set retrieved from the server. Typically the next fetch would be caused by the user scrolling to a new position in the grid. Once that fetch occurs the positions of rows within the grid will be updated to match the positions of rows in the unsorted server-side data set, meaning if the user scrolled back to their previous position they may see a different set of records. (See also [ResultSet.updatePartialCache](../classes/ResultSet.md#attr-resultsetupdatepartialcache)).

**Validation**

Any time saving is attempted, validation is automatically triggered. Values entered by the user will be checked against the [ListGridField.validators](../classes/ListGridField.md#attr-listgridfieldvalidators) and the [DataSourceField.validators](../classes/DataSourceField.md#attr-datasourcefieldvalidators). Any invalid values abort an attempted save.

Similar to editing and saving, validation can be done on row transitions or on cell transitions by setting [validateByCell](../classes/ListGrid_1.md#attr-listgridvalidatebycell), or can be disabled entirely via [neverValidate:true](../classes/ListGrid_1.md#attr-listgridnevervalidate).

**Editability of cells**

Editors will either be shown for the complete row or for a single cell based on [editByCell,editByCell](../classes/ListGrid_1.md#class-listgrid). Whether a cell can be edited can be controlled on a per field basis by setting [field.canEdit](../classes/ListGridField.md#attr-listgridfieldcanedit), or on a per-record basis by setting [recordEditProperty](../classes/ListGrid_1.md#attr-listgridrecordeditproperty) on a [record](../reference_2.md#object-listgridrecord), or can be controlled on an arbitrary, programmatic basis via an override of [ListGrid.canEditCell](../classes/ListGrid_2.md#method-listgridcaneditcell).

Cells which are not editable just display the cell's current value.

**Keyboard Navigation**

Full keyboard navigation is supported by default, including Tab and Shift-Tab to navigate between cells in a row, and Up Arrow and Down Arrow to traverse rows. Several properties on both grids and fields, all named \*EditAction, control navigation behavior of certain keys (eg Enter).

You can use [startEditing(_rowNum_, _colNum_)](../classes/ListGrid_2.md#method-listgridstartediting) to programmatically move editing to a particular cell, for example, during a [field.changed()](../classes/ListGridField.md#method-listgridfieldchanged) event.

**editValues (unsaved changes)**

The term "editValues" means changes that the user has made to the dataset which have not been saved. The grid manages and stores editValues separately from the data itself in order to allow the user to revert to original values, and in order to enable to grid to send only updated fields to the server.

Because editValues are stored separately, if you directly access the dataset (eg via `grid.getData().get()`) you will see the records without the user's unsaved changes. Many APIs exist for retrieving and managing editValues (search for editValue). For the common case of needing to access the record-as-edited, you can call [grid.getEditedRecord(rowNum)](../classes/ListGrid_1.md#method-listgridgeteditedrecord).

When accessing and manipulating edited data, you should think carefully about whether you want to be working with the original data or with the edited version. Values entered by the user may not have been validated yet, or may have failed validation, hence you may find a String value in a field of type "date" or "int", which could cause naive formatters or totaling functions to crash.

Setting editValues via APIs such as [ListGrid.setEditValue](../classes/ListGrid_2.md#method-listgridseteditvalue) is fully equivalent to the user making changes to data via the editing UI. If you _also_ allow editing external to the grid, setting editValues is one way to combine changes from external editors into the grid's edits, so that you can do a single save.

**Customizing Cell Editors**

When a cell is being edited, the editor displayed in the cell will be a [FormItem](../classes/FormItem.md#class-formitem). The editor type for the cell will be determined by [ListGrid.getEditorType](../classes/ListGrid_2.md#method-listgridgeteditortype) based on the specified [ListGridField.editorType](../classes/ListGridField.md#attr-listgridfieldeditortype) or [data type](../classes/ListGridField.md#attr-listgridfieldtype) for the field in question.

You can customize the editor by setting [ListGridField.editorProperties](../classes/ListGridField.md#attr-listgridfieldeditorproperties) to a set of properties that is valid for that FormItem type. Custom FormItem classes are also allowed, for example, you may use [FormItem.icons](../classes/FormItem.md#attr-formitemicons) to create an icon that launches a separate [Dialog](../classes/Dialog.md#class-dialog) in order to provide an arbitrary interface that allows the user to select the value for a field.

**Events**

Editing triggers several events which you can provide handlers for in order to customize editing behavior. Some of the most popular are [field.change()](../classes/ListGridField.md#method-listgridfieldchange), [field.changed()](../classes/ListGridField.md#method-listgridfieldchanged) for detecting changes made by the user, [ListGrid.cellChanged](../classes/ListGrid_2.md#method-listgridcellchanged) for detecting changes that have been successfully saved, and [editorEnter](../classes/ListGrid_2.md#method-listgrideditorenter) and [editorExit()](../classes/ListGrid_2.md#method-listgrideditorexit) for detecting user navigation during editing.

You can also install event handlers directly on the FormItem-based editors used in the grid via [editorProperties](../classes/ListGridField.md#attr-listgridfieldeditorproperties) as mentioned above. When handling events on items, or which involve items, be aware that in addition to standard [FormItem](../classes/FormItem.md#class-formitem) APIs, editors have the following properties:

\- `rowNum`: The rowNum of the record being edited.  
\- `colNum`: The colNum of the cell being edited.  
\- `grid`: A pointer back to the listGrid containing the record.

**Binary Fields**

The ListGrid will automatically show "view" and "download" icon buttons for binary field types (see [ListGridFieldType](../reference.md#type-listgridfieldtype)). However, you cannot use an upload control embedded within a ListGrid row to upload files (regardless of whether you use FileItem or UploadItem). This is because, in the browser's security model, native HTML upload controls cannot be re-created and populated with a chosen file, and the ListGrid needs to be able to re-create editors at any time in order to handle loading data on scroll, scrolling editors in and out of view, adding new rows, changing sort direction, and other use cases.

However you _can_ create an editor with a [FormItem icon](../classes/FormItem.md#attr-formitemicons) that pops up a separate Window containing a FileItem in a DynamicForm, so long as the form in the Window saves the uploaded file immediately rather than trying to have the grid perform the save.

### Related

- [InlineEditEvent](../reference.md#type-inlineeditevent)
- [SearchEditorMode](../reference.md#type-searcheditormode)
- [RowEndEditAction](../reference.md#type-rowendeditaction)
- [EnterKeyEditAction](../reference.md#type-enterkeyeditaction)
- [EscapeKeyEditAction](../reference.md#type-escapekeyeditaction)
- [ArrowKeyEditAction](../reference.md#type-arrowkeyeditaction)
- [EditCompletionEvent](../reference.md#type-editcompletionevent)
- [ListGridEditEvent](../reference.md#type-listgrideditevent)
- [CubeGrid.setEditValue](../classes/CubeGrid.md#method-cubegridseteditvalue)
- [CubeGrid.getEditValue](../classes/CubeGrid.md#method-cubegridgeteditvalue)
- [CubeGrid.getEditedRecord](../classes/CubeGrid.md#method-cubegridgeteditedrecord)
- [CubeGrid.getEditedCell](../classes/CubeGrid.md#method-cubegridgeteditedcell)
- [CubeGrid.getEditValues](../classes/CubeGrid.md#method-cubegridgeteditvalues)
- [CubeGrid.clearEditValue](../classes/CubeGrid.md#method-cubegridcleareditvalue)
- [CubeGrid.saveEdits](../classes/CubeGrid.md#method-cubegridsaveedits)
- [CubeGrid.getAllEditCells](../classes/CubeGrid.md#method-cubegridgetalleditcells)
- [CubeGrid.discardAllEdits](../classes/CubeGrid.md#method-cubegriddiscardalledits)
- [CubeGrid.recordHasChanges](../classes/CubeGrid.md#method-cubegridrecordhaschanges)
- [CubeGrid.hasChanges](../classes/CubeGrid.md#method-cubegridhaschanges)
- [CubeGrid.saveAllEdits](../classes/CubeGrid.md#method-cubegridsavealledits)
- [DataBoundComponent.fieldIsEditable](../classes/DataBoundComponent.md#method-databoundcomponentfieldiseditable)
- [DynamicForm.getEditorType](../classes/DynamicForm.md#method-dynamicformgeteditortype)
- [DynamicForm.fieldIsEditable](../classes/DynamicForm.md#method-dynamicformfieldiseditable)
- [ListGridField.defaultDynamicValue](../classes/ListGridField.md#method-listgridfielddefaultdynamicvalue)
- [ListGridField.editorEnter](../classes/ListGridField.md#method-listgridfieldeditorenter)
- [ListGridField.editorExit](../classes/ListGridField.md#method-listgridfieldeditorexit)
- [ListGridField.cellChanged](../classes/ListGridField.md#method-listgridfieldcellchanged)
- [ListGridField.formatEditorValue](../classes/ListGridField.md#method-listgridfieldformateditorvalue)
- [ListGridField.parseEditorValue](../classes/ListGridField.md#method-listgridfieldparseeditorvalue)
- [ListGridField.change](../classes/ListGridField.md#method-listgridfieldchange)
- [ListGridField.changed](../classes/ListGridField.md#method-listgridfieldchanged)
- [ListGrid.markRecordRemoved](../classes/ListGrid_2.md#method-listgridmarkrecordremoved)
- [ListGrid.markRecordsRemoved](../classes/ListGrid_2.md#method-listgridmarkrecordsremoved)
- [ListGrid.recordMarkedAsRemoved](../classes/ListGrid_2.md#method-listgridrecordmarkedasremoved)
- [ListGrid.unmarkRecordRemoved](../classes/ListGrid_2.md#method-listgridunmarkrecordremoved)
- [ListGrid.markSelectionRemoved](../classes/ListGrid_2.md#method-listgridmarkselectionremoved)
- [ListGrid.canEditCell](../classes/ListGrid_2.md#method-listgridcaneditcell)
- [ListGrid.fieldIsEditable](../classes/ListGrid_2.md#method-listgridfieldiseditable)
- [ListGrid.startEditing](../classes/ListGrid_2.md#method-listgridstartediting)
- [ListGrid.editExistingRecord](../classes/ListGrid_2.md#method-listgrideditexistingrecord)
- [ListGrid.getEditorValueMap](../classes/ListGrid_2.md#method-listgridgeteditorvaluemap)
- [ListGrid.setEditorValueMap](../classes/ListGrid_2.md#method-listgridseteditorvaluemap)
- [ListGrid.getEditorType](../classes/ListGrid_2.md#method-listgridgeteditortype)
- [ListGrid.startEditingNew](../classes/ListGrid_2.md#method-listgridstarteditingnew)
- [ListGrid.getAllEditRows](../classes/ListGrid_2.md#method-listgridgetalleditrows)
- [ListGrid.getEditValues](../classes/ListGrid_2.md#method-listgridgeteditvalues)
- [ListGrid.getEditedRecord](../classes/ListGrid_1.md#method-listgridgeteditedrecord)
- [ListGrid.getEditedCell](../classes/ListGrid_2.md#method-listgridgeteditedcell)
- [ListGrid.setEditValue](../classes/ListGrid_2.md#method-listgridseteditvalue)
- [ListGrid.getEditValue](../classes/ListGrid_2.md#method-listgridgeteditvalue)
- [ListGrid.clearEditValue](../classes/ListGrid_2.md#method-listgridcleareditvalue)
- [ListGrid.getEditRow](../classes/ListGrid_2.md#method-listgridgeteditrow)
- [ListGrid.getEditCol](../classes/ListGrid_2.md#method-listgridgeteditcol)
- [ListGrid.getEditField](../classes/ListGrid_2.md#method-listgridgeteditfield)
- [ListGrid.cancelEditing](../classes/ListGrid_2.md#method-listgridcancelediting)
- [ListGrid.endEditing](../classes/ListGrid_2.md#method-listgridendediting)
- [ListGrid.findNextEditCell](../classes/ListGrid_2.md#method-listgridfindnexteditcell)
- [ListGrid.discardAllEdits](../classes/ListGrid_2.md#method-listgriddiscardalledits)
- [ListGrid.discardEdits](../classes/ListGrid_2.md#method-listgriddiscardedits)
- [ListGrid.saveEdits](../classes/ListGrid_2.md#method-listgridsaveedits)
- [ListGrid.rowHasChanges](../classes/ListGrid_2.md#method-listgridrowhaschanges)
- [ListGrid.hasChanges](../classes/ListGrid_1.md#method-listgridhaschanges)
- [ListGrid.cellHasChanges](../classes/ListGrid_2.md#method-listgridcellhaschanges)
- [ListGrid.saveAllEdits](../classes/ListGrid_1.md#method-listgridsavealledits)
- [ListGrid.cellChanged](../classes/ListGrid_2.md#method-listgridcellchanged)
- [ListGrid.editComplete](../classes/ListGrid_2.md#method-listgrideditcomplete)
- [ListGrid.editFailed](../classes/ListGrid_1.md#method-listgrideditfailed)
- [ListGrid.editorEnter](../classes/ListGrid_2.md#method-listgrideditorenter)
- [ListGrid.rowEditorEnter](../classes/ListGrid_2.md#method-listgridroweditorenter)
- [ListGrid.editorExit](../classes/ListGrid_2.md#method-listgrideditorexit)
- [ListGrid.rowEditorExit](../classes/ListGrid_2.md#method-listgridroweditorexit)
- [ListGrid.formatEditorValue](../classes/ListGrid_2.md#method-listgridformateditorvalue)
- [ListGrid.parseEditorValue](../classes/ListGrid_2.md#method-listgridparseeditorvalue)
- [TreeGrid.startEditingNew](../classes/TreeGrid.md#method-treegridstarteditingnew)
- [Calendar.eventSnapGap](../classes/Calendar.md#attr-calendareventsnapgap)
- [Calendar.showQuickEventDialog](../classes/Calendar.md#attr-calendarshowquickeventdialog)
- [Calendar.eventEditorFields](../classes/Calendar.md#attr-calendareventeditorfields)
- [Calendar.eventEditorDateFieldTitle](../classes/Calendar.md#attr-calendareventeditordatefieldtitle)
- [Calendar.eventDialogFields](../classes/Calendar.md#attr-calendareventdialogfields)
- [ListGrid.recordCanRemoveProperty](../classes/ListGrid_1.md#attr-listgridrecordcanremoveproperty)
- [ListGridRecord._canRemove](../classes/ListGridRecord.md#attr-listgridrecord_canremove)
- [ListGrid.saveRequestProperties](../classes/ListGrid_1.md#attr-listgridsaverequestproperties)
- [ListGridField.editorImageURLPrefix](../classes/ListGridField.md#attr-listgridfieldeditorimageurlprefix)
- [ListGridField.editorImageURLSuffix](../classes/ListGridField.md#attr-listgridfieldeditorimageurlsuffix)
- [ListGridField.icons](../classes/ListGridField.md#attr-listgridfieldicons)
- [ListGridField.editorIconWidth](../classes/ListGridField.md#attr-listgridfieldeditoriconwidth)
- [ListGridField.editorIconHeight](../classes/ListGridField.md#attr-listgridfieldeditoriconheight)
- [ListGridField.defaultIconSrc](../classes/ListGridField.md#attr-listgridfielddefaulticonsrc)
- [ListGridField.iconVAlign](../classes/ListGridField.md#attr-listgridfieldiconvalign)
- [ListGridField.canEdit](../classes/ListGridField.md#attr-listgridfieldcanedit)
- [ListGridField.defaultValue](../classes/ListGridField.md#attr-listgridfielddefaultvalue)
- [ListGridField.enterKeyEditAction](../classes/ListGridField.md#attr-listgridfieldenterkeyeditaction)
- [ListGridField.escapeKeyEditAction](../classes/ListGridField.md#attr-listgridfieldescapekeyeditaction)
- [ListGridField.arrowKeyEditAction](../classes/ListGridField.md#attr-listgridfieldarrowkeyeditaction)
- [ListGridField.editorType](../classes/ListGridField.md#attr-listgridfieldeditortype)
- [ListGridField.editorProperties](../classes/ListGridField.md#attr-listgridfieldeditorproperties)
- [ListGridField.initialValue](../classes/ListGridField.md#attr-listgridfieldinitialvalue)
- [ListGrid.modalEditing](../classes/ListGrid_1.md#attr-listgridmodalediting)
- [ListGridField.multiple](../classes/ListGridField.md#attr-listgridfieldmultiple)
- [ListGridField.editorValueMap](../classes/ListGridField.md#attr-listgridfieldeditorvaluemap)
- [ListGrid.canEdit](../classes/ListGrid_1.md#attr-listgridcanedit)
- [ListGrid.recordEditProperty](../classes/ListGrid_1.md#attr-listgridrecordeditproperty)
- [ListGridRecord._canEdit](../classes/ListGridRecord.md#attr-listgridrecord_canedit)
- [ListGrid.alwaysShowEditors](../classes/ListGrid_1.md#attr-listgridalwaysshoweditors)
- [ListGrid.editByCell](../classes/ListGrid_1.md#attr-listgrideditbycell)
- [ListGrid.saveByCell](../classes/ListGrid_1.md#attr-listgridsavebycell)
- [ListGrid.canRemoveRecords](../classes/ListGrid_1.md#attr-listgridcanremoverecords)
- [ListGrid.deferRemoval](../classes/ListGrid_1.md#attr-listgriddeferremoval)
- [ListGrid.waitForSave](../classes/ListGrid_1.md#attr-listgridwaitforsave)
- [ListGrid.stopOnErrors](../classes/ListGrid_1.md#attr-listgridstoponerrors)
- [ListGrid.autoSaveEdits](../classes/ListGrid_1.md#attr-listgridautosaveedits)
- [ListGrid.confirmCancelEditing](../classes/ListGrid_1.md#attr-listgridconfirmcancelediting)
- [ListGrid.cancelEditingConfirmationMessage](../classes/ListGrid_1.md#attr-listgridcanceleditingconfirmationmessage)
- [ListGrid.confirmDiscardEdits](../classes/ListGrid_1.md#attr-listgridconfirmdiscardedits)
- [ListGrid.autoConfirmSaveEdits](../classes/ListGrid_1.md#attr-listgridautoconfirmsaveedits)
- [ListGrid.confirmDiscardEditsMessage](../classes/ListGrid_1.md#attr-listgridconfirmdiscardeditsmessage)
- [ListGrid.discardEditsSaveButtonTitle](../classes/ListGrid_1.md#attr-listgriddiscardeditssavebuttontitle)
- [ListGrid.rowEndEditAction](../classes/ListGrid_1.md#attr-listgridrowendeditaction)
- [ListGrid.listEndEditAction](../classes/ListGrid_1.md#attr-listgridlistendeditaction)
- [ListGrid.newRecordRowMessage](../classes/ListGrid_1.md#attr-listgridnewrecordrowmessage)
- [ListGrid.enterKeyEditAction](../classes/ListGrid_1.md#attr-listgridenterkeyeditaction)
- [ListGrid.escapeKeyEditAction](../classes/ListGrid_1.md#attr-listgridescapekeyeditaction)
- [ListGrid.arrowKeyEditAction](../classes/ListGrid_1.md#attr-listgridarrowkeyeditaction)
- [ListGrid.editEvent](../classes/ListGrid_1.md#attr-listgrideditevent)
- [ListGrid.editOnFocus](../classes/ListGrid_1.md#attr-listgrideditonfocus)
- [ListGrid.editOnF2Keypress](../classes/ListGrid_1.md#attr-listgrideditonf2keypress)
- [ListGrid.selectOnEdit](../classes/ListGrid_1.md#attr-listgridselectonedit)
- [ListGridField.canToggle](../classes/ListGridField.md#attr-listgridfieldcantoggle)
- [ListGrid.enumCriteriaAsInitialValues](../classes/ListGrid_1.md#attr-listgridenumcriteriaasinitialvalues)
- [ListGrid.longTextEditorThreshold](../classes/ListGrid_1.md#attr-listgridlongtexteditorthreshold)
- [ListGrid.longTextEditorType](../classes/ListGrid_1.md#attr-listgridlongtexteditortype)

---
