# MultiFileItem Documentation

[← Back to API Index](../main.md)

---

## Class: MultiFileItem

*Inherits from:* [CanvasItem](CanvasItem.md#class-canvasitem)

### Description
The MultiFileItem provides an interface for a user to save one or more files that are related to a DataSource record, where each file is represented by a record in a related DataSource.

Use MultiFileItem when a record may have one or more files associated with it (such as attachments to an email message) where no information about the files needs to be stored other than the files themselves. If you have several fields associated with each file (such as an uploaded document with a version, comments and processes associated with it), consider instead an ordinary DataSource with on field of type "binary", and using the [FileItem](FileItem.md#class-fileitem) for upload.

See the [Uploading Files](../kb_topics/upload.md#kb-topic-uploading-files) overview for more information on upload.

**DataSource Setup**

In a relationship sometimes called a "master-detail" relationship, the MultiFileItem stores files in a "detail" DataSource which are related to a "master" DataSource record being edited by the form which contains the MultiFileItem.

To use a MultiFileItem:

*   declare a "detail" DataSource to store the related files. At a minimum, this DataSource must have:
    *   a [primaryKey](DataSourceField.md#attr-datasourcefieldprimarykey) field
    *   a field declaring a [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) relationship to the primaryKey of the "master" DataSource
    *   a field of type "binary"
*   [bind](DataBoundComponent.md#attr-databoundcomponentdatasource) a DynamicForm to the "master" DataSource
*   in the DynamicForm bound to the "master" DataSource, declare a field with [editorType](FormItem.md#attr-formitemeditortype):"MultiFileItem" and a `dataSource` property set to the ID of the "detail" DataSource

An example "detail" DataSource for storing files is shown below. This "detail" DataSource assumes a "master" DataSource with [DataSource.ID](DataSource.md#attr-datasourceid) "masterRecord" and with a primaryKey field "id".
```
 
   <DataSource ID="uploadedFiles" serverType="sql">
     <fields>
        <field name="fileId" type="sequence" primaryKey="true" hidden="true"/>
        <field name="masterRecordId" type="number" foreignKey="masterRecord.id" hidden="true"/>
        <field name="file" type="binary" title="File"/>
     </fields>
   </DataSource>
 
 
```

Aside from a single "binary" field, the "detail" DataSource should generally have only hidden fields, as shown above. Additional internal fields (such as a "lastUpdated" field) may be added, but will not be editable via MultiFileItem.

**Display**

The MultiFileItem appears as a list of files related to the current record. An optional button, the [removeButton](#attr-multifileitemremovebutton) allows removing files. A second optional button, the [editButton](#attr-multifileitemeditbutton), launches a picker for uploading further files.

**Saving**

In all cases, uploading a new file is an "add" DSRequest against the [MultiFileItem.dataSource](#attr-multifileitemdatasource).

The MultiFileItem has two modes, according to whether the "master" record is being newly created via an "add" operation or whether the master record is pre-existing ("update" operation).

If the master record is pre-existing, each file added by the user is uploaded as soon as the user exits the picker launched from the edit button, and the list of files shown in the main form reflects the actual list of stored files.

If the master record is being newly created, files are not actually uploaded until **after** the master record is confirmed saved, and the list of fields shown in the main form reflects files which will be uploaded after the master record is saved.

In both cases, if there are multiple files to upload, they are uploaded one at a time, as a series of separate "add" DSRequests against the [MultiFileItem.dataSource](#attr-multifileitemdatasource).

Also in both cases, deletion of any file is immediate. In the case of a pre-existing master record, all files shown actually exist as DataSource records, and deletion is performed as a "remove" DSRequest against the [MultiFileItem.dataSource](#attr-multifileitemdatasource).

### Groups

- upload

---
## Attr: MultiFileItem.editButton

### Description
Button for launching a picker to add new files for upload. Supports the properties of a [FormItemIcon](../main.md#object-formitemicon).

**Flags**: IR

---
## Attr: MultiFileItem.pickerAddAnotherFileButtonTitle

### Description
The contents of the "Add another" file button in the picker launched by the [edit button](#attr-multifileitemeditbutton).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiFileItem.removeButtonPrompt

### Description
The [prompt](FormItemIcon.md#attr-formitemiconprompt) of the [remove button](#attr-multifileitemremovebutton).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiFileItem.emptyMessage

### Description
Empty message to display when there are no files listed.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiFileItem.dataSource

### Description
DataSource where files are stored.

This DataSource is expected to have a field of type "binary" as well as a primaryKey and foreignKey declaration to some other DataSource; see the [MultiFileItem](#class-multifileitem) for an overview.

This DataSource need only be capable of "fetch", "add" and "remove" - "update" is unused.

**Flags**: IR

---
## Attr: MultiFileItem.pickerUploadButtonInitialTitle

### Description
The initial title of the upload button in the picker lauched by the [edit button](#attr-multifileitemeditbutton) that is used before the form is saved.

### Groups

- i18nMessages

### See Also

- [MultiFileItem.pickerUploadButtonTitle](#attr-multifileitempickeruploadbuttontitle)

**Flags**: IR

---
## Attr: MultiFileItem.removeButton

### Description
Button for removing files. Supports the properties of a [FormItemIcon](../main.md#object-formitemicon).

**Flags**: IR

---
## Attr: MultiFileItem.pickerCancelButtonTitle

### Description
The title of the cancel button in the picker lauched by the [edit button](#attr-multifileitemeditbutton).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiFileItem.pickerUploadButtonTitle

### Description
The title of the upload button in the picker lauched by the [edit button](#attr-multifileitemeditbutton) that is used after the form is saved.

### Groups

- i18nMessages

### See Also

- [MultiFileItem.pickerUploadButtonInitialTitle](#attr-multifileitempickeruploadbuttoninitialtitle)

**Flags**: IR

---
## Attr: MultiFileItem.pickerConstructor

### Description
MultiFileItems use a [MultiFilePicker](../main.md#class-multifilepicker) instance as their picker. The generated `picker` autoChild may be customized via the standard [AutoChild](../main.md#type-autochild) pattern.

**Flags**: IR

---
## Attr: MultiFileItem.pickerUploadProgressLabel

### Description
Specifies the label of the progress meter in the picker lauched by the [edit button](#attr-multifileitemeditbutton). This property is a dynamic string, similar to the [Canvas.dynamicContents](Canvas.md#attr-canvasdynamiccontents) feature, with the variables `fileName` and `formattedFileSize`.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: MultiFileItem.editButtonPrompt

### Description
The [prompt](FormItemIcon.md#attr-formitemiconprompt) of the [edit button](#attr-multifileitemeditbutton).

### Groups

- i18nMessages

**Flags**: IR

---
