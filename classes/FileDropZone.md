# FileDropZone Documentation

[← Back to API Index](../reference.md)

---

## Class: FileDropZone

*Inherits from:* [DropZone](DropZone.md#class-dropzone)

### Description
The FileDropZone class provides a straightforward way to upload files from a user's desktop using HTML5 file drop capabilities.

A FileDropZone does not itself upload files - it provides the UI for file collection and progress indication. Upload is typically handled by a surrounding form or application code.

Users can add files by dragging them onto the drop zone, or by clicking the drop zone to open a standard file browser dialog (when [canAddFilesOnClick](#canaddfilesonclick) is true).

When used with a form, uploads include per-file progress indication and error handling.

For use within a DynamicForm, see [FileUploadItem](FileUploadItem.md#class-fileuploaditem).

FileDropZone extends [DropZone](DropZone.md#class-dropzone) (and therefore StatefulCanvas), so CSS styling uses standard state suffixes: Over (during drag), Disabled, and custom states Populated (files present) and Processing (upload in progress).

---
## ClassAttr: FileDropZone.maxSizeErrorMessage

### Description
Error message shown when [FileDropZone.maxSize](#attr-filedropzonemaxsize) is exceeded.

### Groups

- i18nMessages

**Flags**: IR

---
## ClassAttr: FileDropZone.clickToAddMessage

### Description
Message shown below [FileDropZone.emptyDropAreaMessage](#classattr-filedropzoneemptydropareamessage) when [FileDropZone.canAddFilesOnClick](#attr-filedropzonecanaddfilesonclick) is true.

### Groups

- i18nMessages

**Flags**: IR

---
## ClassAttr: FileDropZone.dragOverReplaceMessage

### Description
Message shown during dragOver when the zone is populated and [FileDropZone.replaceFilesOnDrop](#attr-filedropzonereplacefilesondrop) is true.

### Groups

- i18nMessages

**Flags**: IR

---
## ClassAttr: FileDropZone.multipleFilesErrorMessage

### Description
Error message shown when multiple files are dropped but [FileDropZone.multiple](#attr-filedropzonemultiple) is false.

### Groups

- i18nMessages

**Flags**: IR

---
## ClassAttr: FileDropZone.retryButtonTitle

### Description
Title for the retry button shown on failed uploads.

### Groups

- i18nMessages

**Flags**: IR

---
## ClassAttr: FileDropZone.maxFilesErrorMessage

### Description
Error message shown when [FileDropZone.maxFiles](#attr-filedropzonemaxfiles) is exceeded. Dynamic string supporting ${maxFiles} substitution.

### Groups

- i18nMessages

**Flags**: IR

---
## ClassAttr: FileDropZone.emptyDropAreaMessage

### Description
Default message shown when no files have been added.

### Groups

- i18nMessages

**Flags**: IR

---
## ClassAttr: FileDropZone.cancelButtonTitle

### Description
Title for the cancel button.

### Groups

- i18nMessages

**Flags**: IR

---
## ClassAttr: FileDropZone.processingMessage

### Description
Message shown during upload/processing.

### Groups

- i18nMessages

**Flags**: IR

---
## ClassAttr: FileDropZone.dragOverAddMessage

### Description
Message shown during dragOver when the zone is populated and [FileDropZone.replaceFilesOnDrop](#attr-filedropzonereplacefilesondrop) is false.

### Groups

- i18nMessages

**Flags**: IR

---
## ClassAttr: FileDropZone.maxFileSizeErrorMessage

### Description
Error message shown when [FileDropZone.maxFileSize](#attr-filedropzonemaxfilesize) is exceeded. Dynamic string supporting ${file} substitution.

### Groups

- i18nMessages

**Flags**: IR

---
## ClassAttr: FileDropZone.duplicateFileNameMessage

### Description
Error message shown when a duplicate file is detected and [FileDropZone.replaceFilesOnDrop](#attr-filedropzonereplacefilesondrop) is false. Dynamic string supporting ${file} substitution.

### Groups

- i18nMessages

**Flags**: IR

---
## ClassAttr: FileDropZone.minSizeErrorMessage

### Description
Error message shown when [FileDropZone.minSize](#attr-filedropzoneminsize) is not met.

### Groups

- i18nMessages

**Flags**: IR

---
## ClassAttr: FileDropZone.invalidFileTypeMessage

### Description
Error message shown when [FileDropZone.acceptedFileTypes](#attr-filedropzoneacceptedfiletypes) is violated. Dynamic string supporting ${file} substitution.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FileDropZone.videoFileIcon

### Description
Icon for video files.

**Flags**: IR

---
## Attr: FileDropZone.audioFileIcon

### Description
Icon for audio files.

**Flags**: IR

---
## Attr: FileDropZone.minSize

### Description
Minimum total size in bytes for all files combined.

**Flags**: IR

---
## Attr: FileDropZone.archiveFileIcon

### Description
Icon for archive files (ZIP, TAR, etc.).

**Flags**: IR

---
## Attr: FileDropZone.defaultFileIcon

### Description
Default icon for files when no specific type icon is available.

**Flags**: IR

---
## Attr: FileDropZone.spreadsheetFileIcon

### Description
Icon for spreadsheet files (Excel, CSV, etc.).

**Flags**: IR

---
## Attr: FileDropZone.codeFileIcon

### Description
Icon for code/script files.

**Flags**: IR

---
## Attr: FileDropZone.showFileThumbnails

### Description
If true, display thumbnails/icons for added files. If false, show only file names.

**Flags**: IR

---
## Attr: FileDropZone.baseStyle

### Description
Base CSS class for the drop zone. Supports state suffixes: Over, Populated, Processing, Disabled.

**Flags**: IR

---
## Attr: FileDropZone.progressText

### Description
AutoChild Label showing the percentage complete text.

**Flags**: IR

---
## Attr: FileDropZone.documentFileIcon

### Description
Icon for document files (Word, text, etc.).

**Flags**: IR

---
## Attr: FileDropZone.maxFileSize

### Description
Maximum size in bytes for any individual file.

**Flags**: IR

---
## Attr: FileDropZone.pdfFileIcon

### Description
Icon for PDF files.

**Flags**: IR

---
## Attr: FileDropZone.replaceFilesOnDrop

### Description
If true, dropping new files replaces existing files. If false, new files are added to the existing list.

**Flags**: IR

---
## Attr: FileDropZone.imageFileIcon

### Description
Icon for image files (when showImagePreviews is false).

**Flags**: IR

---
## Attr: FileDropZone.maxSize

### Description
Maximum total size in bytes for all files combined.

**Flags**: IR

---
## Attr: FileDropZone.valign

### Description
Vertical alignment for drop zone content.

**Flags**: IR

---
## Attr: FileDropZone.progressLabel

### Description
AutoChild Label showing the processing message during uploads.

**Flags**: IR

---
## Attr: FileDropZone.thumbnailWidth

### Description
Width in pixels for file thumbnails/icons.

**Flags**: IR

---
## Attr: FileDropZone.acceptedFileTypes

### Description
Array of accepted MIME types (e.g., \["image/\*", "application/pdf"\]). If null, all file types are accepted.

**Flags**: IR

---
## Attr: FileDropZone.showCancelButton

### Description
Whether to show a cancel button during processing that allows the user to abort the upload.

**Flags**: IR

---
## Attr: FileDropZone.align

### Description
Horizontal alignment for drop zone content.

**Flags**: IR

---
## Attr: FileDropZone.removeIcon

### Description
Icon for the remove button on file tiles.

**Flags**: IR

---
## Attr: FileDropZone.canAddFilesOnClick

### Description
If true, clicking the drop zone opens a file browser dialog.

**Flags**: IR

---
## Attr: FileDropZone.multiple

### Description
Does this FileDropZone support multiple files?

**Flags**: IR

---
## Attr: FileDropZone.thumbnailHeight

### Description
Height in pixels for file thumbnails/icons.

**Flags**: IR

---
## Attr: FileDropZone.progressBar

### Description
AutoChild Progressbar showing upload progress.

**Flags**: IR

---
## Attr: FileDropZone.showImagePreviews

### Description
When [FileDropZone.showFileThumbnails](#attr-filedropzoneshowfilethumbnails) is true, should actual image previews be generated for image files? If false, image files will show a generic image icon instead. Image previews are generated using the FileReader API.

**Flags**: IR

---
## Attr: FileDropZone.cancelButton

### Description
AutoChild Button allowing users to cancel an in-progress upload. Only shown if [FileDropZone.showCancelButton](#attr-filedropzoneshowcancelbutton) is true.

**Flags**: IR

---
## Attr: FileDropZone.maxFiles

### Description
Maximum number of files allowed when [FileDropZone.multiple](#attr-filedropzonemultiple) is true.

**Flags**: IR

---
## Method: FileDropZone.getProcessingPercentDone

### Description
Get current progress percentage.

### Returns

`[Integer](../reference_2.md#type-integer)` — Current percentage, or null if not processing

---
## Method: FileDropZone.showDropError

### Description
Display an error when a drop fails validation. Default implementation calls isc.warn(). Override for custom handling.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| errorMessage | [String](#type-string) | false | — | Error message to display |

---
## Method: FileDropZone.fileUploadFailed

### Description
Notification fired when an individual file upload fails (in concurrent mode).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| file | [File](#type-file) | false | — | The file that failed |
| error | [String](#type-string) | false | — | Error message describing the failure |

---
## Method: FileDropZone.fileUploadComplete

### Description
Notification fired when an individual file upload completes (in concurrent mode).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| file | [File](#type-file) | false | — | The file that completed |
| success | [Boolean](#type-boolean) | false | — | Whether the upload succeeded |
| response | [DSResponse](#type-dsresponse) | false | — | The server response for this file |

---
## Method: FileDropZone.setProcessingProgress

### Description
Update progress indication during upload/processing.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| percentDone | [Float](../reference_2.md#type-float) | false | — | Progress percentage (0-100) |
| processed | [Integer](../reference_2.md#type-integer) | false | — | Bytes processed so far |
| total | [Integer](../reference_2.md#type-integer) | false | — | Total bytes being processed |

### Returns

`[Boolean](#type-boolean)` — false if no files selected, true otherwise

---
## Method: FileDropZone.filesRemoved

### Description
Notification fired when files are removed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| files | [Array of File](#type-array-of-file) | false | — | Files that were removed |

---
## Method: FileDropZone.getSize

### Description
Get the total size in bytes of all selected files.

### Returns

`[Integer](../reference_2.md#type-integer)` — Total size in bytes, or 0 if no files

---
## Method: FileDropZone.clearFiles

### Description
Clear all files from this fileDropZone.

---
## Method: FileDropZone.removeFile

### Description
Remove a specific file from this fileDropZone.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| file | [File](#type-file)|[Integer](../reference_2.md#type-integer) | false | — | The file to remove, or its index |

---
## Method: FileDropZone.cancelProcessing

### Description
Cancel an in-progress upload/processing operation.

This will abort the active XHR request (if any), hide the processing UI, and fire the [FileDropZone.processingCancelled](#method-filedropzoneprocessingcancelled) notification.

---
## Method: FileDropZone.filesAdded

### Description
Notification fired when files are successfully added (via drag or click).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| files | [Array of File](#type-array-of-file) | false | — | Files that were added |

---
## Method: FileDropZone.getFiles

### Description
Retrieves the files that have been added to this fileDropZone.

### Returns

`[Array of File](#type-array-of-file)` — JavaScript File objects added to this fileDropZone

---
## Method: FileDropZone.setFiles

### Description
Programmatically populate a fileDropZone with files.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| files | [File](#type-file)|[Array of File](#type-array-of-file) | false | — | JavaScript File object(s) to attach |

---
## Method: FileDropZone.setFileProgress

### Description
Update progress indication for a specific file during concurrent uploads.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| file | [File](#type-file) | false | — | The file being uploaded |
| percentDone | [Float](../reference_2.md#type-float) | false | — | Progress percentage (0-100) for this file |
| processed | [Integer](../reference_2.md#type-integer) | false | — | Bytes processed so far for this file |
| total | [Integer](../reference_2.md#type-integer) | false | — | Total bytes for this file |

---
## Method: FileDropZone.processingCancelled

### Description
Notification fired when processing is cancelled via [FileDropZone.cancelProcessing](#method-filedropzonecancelprocessing).

This is a notification method intended for override. The FileDropZone itself does not perform any network abort logic - it only manages local UI state (hiding progress, preserving files). When used as the canvas of a [FileUploadItem](FileUploadItem.md#class-fileuploaditem), the item's default configuration overrides this method to propagate the cancel to the containing [DynamicForm](DynamicForm.md#class-dynamicform), which handles aborting any in-flight XHR upload request via [RPCManager.cancelQueue](RPCManager.md#classmethod-rpcmanagercancelqueue).

For standalone FileDropZone usage (outside of FileUploadItem), implement this method to abort any custom upload logic you have initiated.

---
## Method: FileDropZone.startProcessing

### Description
Show UI indicating processing has started. Masks the component and shows progressIndicator.

### Returns

`[Boolean](#type-boolean)` — false if no files selected, true otherwise

---
## Method: FileDropZone.endProcessing

### Description
Hide processing UI. Called when upload/processing completes.

---
