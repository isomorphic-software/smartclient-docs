# FileUploadItem Documentation

[← Back to API Index](../reference.md)

---

## Class: FileUploadItem

*Inherits from:* [CanvasItem](CanvasItem.md#class-canvasitem)

### Description
FormItem for uploading files using HTML5 file drop capabilities.

A FileUploadItem's [canvas](#attr-fileuploaditemcanvas) is a [FileDropZone](FileDropZone.md#class-filedropzone). The [value](#method-getvalue) of a FileUploadItem is the JavaScript File object(s) representing files the user added.

FileUploadItem is not the default for `binary` type fields. To use FileUploadItem for binary fields, set [DynamicForm.useFileUploadItem](DynamicForm.md#attr-dynamicformusefileuploaditem) to true on the form, or specify `editorType:"FileUploadItem"` on the field.

When the form is [saved](DynamicForm.md#method-dynamicformsavedata), files are uploaded automatically. Use [DynamicForm.showUploadProgress](DynamicForm.md#attr-dynamicformshowuploadprogress) to display upload progress.

**Single File Upload**

With the default setting of [multiple:false](#multiple), a FileUploadItem allows uploading a single file to a binary field on the DataSource. This is analogous to the standard [FileItem](FileItem.md#class-fileitem).

**Multiple File Upload**

To upload multiple files, set [multiple:true](#multiple) and configure a [DataSource](DataSource.md#class-datasource) property pointing to a related DataSource that will store the files. This follows the same master-detail pattern as [MultiFileItem](MultiFileItem.md#class-multifileitem):

*   The form's DataSource is the "master" record (e.g., an email message)
*   The FileUploadItem's [DataSource](DataSource.md#class-datasource) is the "detail" DataSource storing files (e.g., email attachments)
*   The detail DataSource must have a [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) linking to the master DataSource's primary key
*   Each uploaded file creates a separate record in the detail DataSource

See [MultiFileItem](MultiFileItem.md#class-multifileitem) for an example of the DataSource setup required.

**Multiple Binary Fields**

A form can contain multiple FileUploadItems for different binary fields in the same DataSource. When the form is saved, all files are uploaded in a single request, creating one record with all binary fields populated. This differs from [FileItem](FileItem.md#class-fileitem) which has a limitation preventing multiple file uploads in a single form submission.

Note: If you want immediate upload on drop (like Gmail attachments), use a [FormItem.changed](FormItem.md#method-formitemchanged) handler to call [DynamicForm.saveData](DynamicForm.md#method-dynamicformsavedata).

---
## Attr: FileUploadItem.canvasConstructor

### Description
The class to use for the [Canvas](Canvas.md#class-canvas) autoChild. Default is FileDropZone.

**Flags**: IR

---
## Attr: FileUploadItem.cancelButtonTitle

### Description
Custom [FileDropZone.cancelButtonTitle](FileDropZone.md#classattr-filedropzonecancelbuttontitle) for this fileUploadItem's canvas. If unset, the default property will be used.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FileUploadItem.multipleFilesErrorMessage

### Description
Custom [FileDropZone.multipleFilesErrorMessage](FileDropZone.md#classattr-filedropzonemultiplefileserrormessage) for this fileUploadItem's canvas. If unset, the default property will be used.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FileUploadItem.canvas

### Description
The [FileDropZone](FileDropZone.md#class-filedropzone) component that provides the drag-drop file selection UI.

The FileDropZone is automatically created using the [FileUploadItem.canvasConstructor](#attr-fileuploaditemcanvasconstructor) and [FileUploadItem.canvasDefaults](#attr-fileuploaditemcanvasdefaults) properties. To customize the FileDropZone, either set properties directly on the FileUploadItem (which are passed through to the FileDropZone) or override [FileUploadItem.canvasDefaults](#attr-fileuploaditemcanvasdefaults).

Access the FileDropZone via `fileUploadItem.canvas` after the item is created.

**Flags**: IR

---
## Attr: FileUploadItem.emptyDropAreaMessage

### Description
Custom [FileDropZone.emptyDropAreaMessage](FileDropZone.md#classattr-filedropzoneemptydropareamessage) for this fileUploadItem's canvas. If unset, the default property will be used.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FileUploadItem.processingMessage

### Description
Custom [FileDropZone.processingMessage](FileDropZone.md#classattr-filedropzoneprocessingmessage) for this fileUploadItem's canvas. If unset, the default property will be used.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FileUploadItem.duplicateFileNameMessage

### Description
Custom [FileDropZone.duplicateFileNameMessage](FileDropZone.md#classattr-filedropzoneduplicatefilenamemessage) for this fileUploadItem's canvas. If unset, the default property will be used.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FileUploadItem.showCancelButton

### Description
See [FileDropZone.showCancelButton](FileDropZone.md#attr-filedropzoneshowcancelbutton).

**Flags**: IR

---
## Attr: FileUploadItem.minSize

### Description
See [FileDropZone.minSize](FileDropZone.md#attr-filedropzoneminsize).

**Flags**: IR

---
## Attr: FileUploadItem.thumbnailWidth

### Description
See [FileDropZone.thumbnailWidth](FileDropZone.md#attr-filedropzonethumbnailwidth).

**Flags**: IR

---
## Attr: FileUploadItem.maxFileSizeErrorMessage

### Description
Custom [FileDropZone.maxFileSizeErrorMessage](FileDropZone.md#classattr-filedropzonemaxfilesizeerrormessage) for this fileUploadItem's canvas. If unset, the default property will be used.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FileUploadItem.maxSize

### Description
See [FileDropZone.maxSize](FileDropZone.md#attr-filedropzonemaxsize).

**Flags**: IR

---
## Attr: FileUploadItem.showImagePreviews

### Description
See [FileDropZone.showImagePreviews](FileDropZone.md#attr-filedropzoneshowimagepreviews).

**Flags**: IR

---
## Attr: FileUploadItem.canAddFilesOnClick

### Description
See [FileDropZone.canAddFilesOnClick](FileDropZone.md#attr-filedropzonecanaddfilesonclick).

**Flags**: IR

---
## Attr: FileUploadItem.replaceFilesOnDrop

### Description
See [FileDropZone.replaceFilesOnDrop](FileDropZone.md#attr-filedropzonereplacefilesondrop).

**Flags**: IR

---
## Attr: FileUploadItem.invalidFileTypeMessage

### Description
Custom [FileDropZone.invalidFileTypeMessage](FileDropZone.md#classattr-filedropzoneinvalidfiletypemessage) for this fileUploadItem's canvas. If unset, the default property will be used.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FileUploadItem.showFileThumbnails

### Description
See [FileDropZone.showFileThumbnails](FileDropZone.md#attr-filedropzoneshowfilethumbnails).

**Flags**: IR

---
## Attr: FileUploadItem.minSizeErrorMessage

### Description
Custom [FileDropZone.minSizeErrorMessage](FileDropZone.md#classattr-filedropzoneminsizeerrormessage) for this fileUploadItem's canvas. If unset, the default property will be used.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FileUploadItem.clickToAddMessage

### Description
Custom [FileDropZone.clickToAddMessage](FileDropZone.md#classattr-filedropzoneclicktoaddmessage) for this fileUploadItem's canvas. If unset, the default property will be used.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FileUploadItem.dataSource

### Description
DataSource where files are stored when [multiple:true](#attr-fileuploaditemmultiple).

This DataSource should contain:

*   A [primaryKey](DataSourceField.md#attr-datasourcefieldprimarykey) field
*   A field with a [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) relationship to the primary key of the form's DataSource
*   A field of type "binary" for storing the uploaded file

This follows the same pattern as [MultiFileItem.dataSource](MultiFileItem.md#attr-multifileitemdatasource). See [MultiFileItem](MultiFileItem.md#class-multifileitem) for a complete example of the required DataSource structure.

This property is required when [multiple:true](#attr-fileuploaditemmultiple) is set. If omitted, a warning will be logged and the item will behave as single-file upload.

**Flags**: IR

---
## Attr: FileUploadItem.thumbnailHeight

### Description
See [FileDropZone.thumbnailHeight](FileDropZone.md#attr-filedropzonethumbnailheight).

**Flags**: IR

---
## Attr: FileUploadItem.maxFileSize

### Description
See [FileDropZone.maxFileSize](FileDropZone.md#attr-filedropzonemaxfilesize).

**Flags**: IR

---
## Attr: FileUploadItem.canvasDefaults

### Description
Default properties for the [Canvas](Canvas.md#class-canvas) autoChild FileDropZone.

The default implementation includes handlers that forward [FileDropZone.filesAdded](FileDropZone.md#method-filedropzonefilesadded) and [FileDropZone.filesRemoved](FileDropZone.md#method-filedropzonefilesremoved) notifications to update the FormItem's value.

When overriding, use `isc.addProperties()` to merge with the defaults rather than replacing them entirely, to preserve the value synchronization behavior.

**Flags**: IR

---
## Attr: FileUploadItem.maxSizeErrorMessage

### Description
Custom [FileDropZone.maxSizeErrorMessage](FileDropZone.md#classattr-filedropzonemaxsizeerrormessage) for this fileUploadItem's canvas. If unset, the default property will be used.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FileUploadItem.maxFiles

### Description
See [FileDropZone.maxFiles](FileDropZone.md#attr-filedropzonemaxfiles).

**Flags**: IR

---
## Attr: FileUploadItem.multiple

### Description
Whether this FileUploadItem allows multiple files to be selected.

When `multiple:true`, a [DataSource](DataSource.md#class-datasource) property must also be specified pointing to a related DataSource that will store the uploaded files, following the same master-detail pattern as [MultiFileItem](MultiFileItem.md#class-multifileitem). Each file will be uploaded as a separate record in the detail DataSource after the master record is saved.

If `multiple:true` is set without a valid [DataSource](DataSource.md#class-datasource), a warning will be logged and the item will behave as if `multiple:false`.

See [FileDropZone.multiple](FileDropZone.md#attr-filedropzonemultiple) for the underlying FileDropZone property.

**Flags**: IR

---
## Attr: FileUploadItem.maxFilesErrorMessage

### Description
Custom [FileDropZone.maxFilesErrorMessage](FileDropZone.md#classattr-filedropzonemaxfileserrormessage) for this fileUploadItem's canvas. If unset, the default property will be used.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FileUploadItem.acceptedFileTypes

### Description
See [FileDropZone.acceptedFileTypes](FileDropZone.md#attr-filedropzoneacceptedfiletypes).

**Flags**: IR

---
## Method: FileUploadItem.endProcessing

### Description
See [FileDropZone.endProcessing](FileDropZone.md#method-filedropzoneendprocessing).

---
## Method: FileUploadItem.getSize

### Description
See [FileDropZone.getSize](FileDropZone.md#method-filedropzonegetsize).

---
## Method: FileUploadItem.getFiles

### Description
See [FileDropZone.getFiles](FileDropZone.md#method-filedropzonegetfiles).

---
## Method: FileUploadItem.getDataSource

### Description
Returns the DataSource configured for storing uploaded files when [multiple:true](#attr-fileuploaditemmultiple).

### Returns

`[DataSource](#type-datasource)` — the detail DataSource, or null if not configured

---
## Method: FileUploadItem.startProcessing

### Description
See [FileDropZone.startProcessing](FileDropZone.md#method-filedropzonestartprocessing).

---
## Method: FileUploadItem.setFileProgress

### Description
See [FileDropZone.setFileProgress](FileDropZone.md#method-filedropzonesetfileprogress).

---
## Method: FileUploadItem.setProcessingProgress

### Description
See [FileDropZone.setProcessingProgress](FileDropZone.md#method-filedropzonesetprocessingprogress).

---
## Method: FileUploadItem.cancelProcessing

### Description
See [FileDropZone.cancelProcessing](FileDropZone.md#method-filedropzonecancelprocessing).

---
