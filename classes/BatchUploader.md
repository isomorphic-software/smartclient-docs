# BatchUploader Documentation

[← Back to API Index](../reference.md)

---

## Class: BatchUploader

*Inherits from:* [VStack](../reference.md#class-vstack)

### Description
The BatchUploader handles the upload, validation, review and saving of a dataset expressed in CSV or other upload formats.

**NOTE:** BatchUploader is only available with SmartClient Power or better.

By default, a BatchUploader consists of a single [FileItem](FileItem.md#class-fileitem) form field. This form field will upload a file using the special "batchUpload" built-in DataSource. The uploaded file data will be parsed and validated using the [uploadDataSource](#attr-batchuploaderuploaddatasource), then streamed back to the browser, along with any errors, for display in a ListGrid.

The [BatchUploader.previewShown](#method-batchuploaderpreviewshown) notification method will be fired when the uploaded records are being displayed in this grid.

The user can then correct any errors and submit the final dataset, which will be added to the DataSource via a series of "add" DSRequests, all submitted as a single HTTP request via [request queuing](RPCManager.md#classmethod-rpcmanagerstartqueue).  
Developers may specify a custom "add" operation to use on the target [BatchUploader.uploadDataSource](#attr-batchuploaderuploaddatasource) via the [BatchUploader.uploadOperation](#attr-batchuploaderuploadoperation) property.

Additional form fields can be added to the form that uploads the data file via [uploadFormFields](#attr-batchuploaderuploadformfields). Values entered into these fields are not included in the "add" DSRequests used to store the uploaded records. Instead, they are stored as HttpSession attributes with the names corresponding to the names of the specified `uploadFormFields` (optionally with a [prefix](#attr-batchuploaderuploadfieldprefix) applied, in case this is necessary to avoid name collisions in the session). This allows any custom logic for the "add" operation to access these additional fields via httpSession.getAttribute(). If [uploadFormFields](#attr-batchuploaderuploadformfields) are not provided method httpSession.getAttribute() will not be called.

Because all records are saved in a single HTTP request, a similar strategy of storing data as servletRequest or session attributes allows reuse of objects required to perform the "add" operations (such as field values common to all added records, or a SQL connection or transaction manager).

If you already have upload data available as a csv-formatted string or similar, the BatchUploader can be used without showing an upload interface. This can be valuable if you are picking up sample data from some custom UI (a separate upload component, or TextArea for copy/pasting content, for example).  
To suppress the upload interface, set [BatchUploader.showUploadForm](#attr-batchuploadershowuploadform) to `false` and invoke [BatchUploader.uploadData](#method-batchuploaderuploaddata) directly. The `uploadData()` method passes sample data to the server as `values.pasteData`. The server side `batchUpload` dataSource has logic to extract and work with this data, exactly as if it had been directly uploaded as the content of a file.

If [uploadFieldName](DataSourceField.md#attr-datasourcefielduploadfieldname) is set on any of the [uploadDataSource](#attr-batchuploaderuploaddatasource)'s fields, the BatchUploader will use that name to map the uploaded file's content.

Note, that for [CSV data format](#attr-batchuploaderdataformat) header line is optional. If first non-empty line in the uploaded file has no matching field names, it is assumed that there's no header row, and all rows (including the first one) are treated as data rows.

Imported data can be transformed during import, see [DataSourceField.importStrategy](DataSourceField.md#attr-datasourcefieldimportstrategy) for details.

A couple of server-side techniques are interesting in conjunction with the BatchUploader. One is to set the [DataSource.serverConstructor](DataSource.md#attr-datasourceserverconstructor) property to point at your own class that inherits from `com.isomorphic.datasource.BasicDataSource`. The most interesting reason for doing this is to override the `validate` method and provide complete custom validation - for example, checking relations to other tables.

Another technique is to handle the initial SmartClient call in your own servlet, by setting the [dataURL](#attr-batchuploaderdataurl) property. You then handle the add requests with a combination of your own code and SmartClient server API calls. This is a good way to add special pre- and post-processing to the normal server-side flow.

**Note:** The special "batchUpload" DataSource, which should reside in the shared/ds folder of your application's webroot (see [Installation Instructions](../kb_topics/iscInstall.md#kb-topic-installing-the-smartclient-runtime)) . is not part of your application's data flow, and it has nothing to do with the [uploadDataSource](#attr-batchuploaderuploaddatasource) you use to actually persist the validated and error-corrected data: it is simply a means to uploading the raw data in the first place. Normally, you should simply ignore its presence and treat it as an internal detail of the SmartClient framework.

However, there are circumstances in which you may wish to change it to achieve specific aims. For example, you may wish to override the Java class it invokes, in order to insert your own security or other validation logic into the initial upload flow. This is entirely in keeping with the design, but we regard it as an out-of-the-ordinary use-case: normal usage is simply to ignore the presence of the batchUpload DataSource.

BatchUploader is a [VStack](../reference.md#class-vstack), that simply stacks members on the vertical axis without trying to manage their height. If you need to control heights, you can set [vPolicy](Layout.md#attr-layoutvpolicy) to "fill"

---
## Attr: BatchUploader.uploadDelimiter

### Description
The delimiter to use when importing character-delimited files. The default is comma (CSV).

**Flags**: IRW

---
## Attr: BatchUploader.previousButton

### Description
Button that scrolls grid to the previous error.

**Flags**: IR

---
## Attr: BatchUploader.uploadFileItem

### Description
FileItem for selecting the file to upload.

**Flags**: IR

---
## Attr: BatchUploader.uploadFileLabel

### Description
Title to display next to the [FileItem](FileItem.md#class-fileitem) field where the user enters a filename to upload

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: BatchUploader.commitButtonTitle

### Description
Title for the [commit button](#attr-batchuploadercommitbutton).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: BatchUploader.uploadStatusMessages

### Description
Container for informational messages that are shown when a user attempts an upload. Appears above the [BatchUploader.grid](#attr-batchuploadergrid).

**Flags**: IR

---
## Attr: BatchUploader.defaultQuoteString

### Description
The default character used to quote strings.

**Deprecated**

**Flags**: IRW

---
## Attr: BatchUploader.uploadOperation

### Description
Optional [DSRequest.operationId](DSRequest.md#attr-dsrequestoperationid) for the "add" operation used to add new records to the [BatchUploader.uploadDataSource](#attr-batchuploaderuploaddatasource).

**Flags**: IR

---
## Attr: BatchUploader.cancelConfirmMessage

### Description
Confirmation message to show if the user clicks the "Cancel" button and [BatchUploader.warnOnCancel](#attr-batchuploaderwarnoncancel) is true. Defaults to "You will lose any work you have done on this data. Proceed anyway?"

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: BatchUploader.previousButtonTitle

### Description
Title for the [previous error button](#attr-batchuploaderpreviousbutton).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: BatchUploader.uploadForm

### Description
Form used to specify file to upload, and any additional fields required.

**Flags**: IR

---
## Attr: BatchUploader.uploadEncoding

### Description
On server-side, BatchUploader uses `DataImport` to import uploaded files, specifically APIs taking `java.io.Reader` parameter. `BatchUploader.uploadEncoding` setting defines the encoding, which will be used to create a `java.io.Reader` instance to read data from uploaded files. The default is "UTF-8".

**Flags**: IRW

---
## Attr: BatchUploader.partialCommitError

### Description
If [BatchUploader.partialCommit](#attr-batchuploaderpartialcommit) is set to "prevent", the text to display to the user if they try to commit a dataset containing errors. By default, this text is "There are errors in your data. Please correct all errors before clicking Commit"

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: BatchUploader.errorMessageFileIsBlank

### Description
Error message to show when the uploading process detects a file with no data.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: BatchUploader.errorMessageExcelFileDetected

### Description
Error message to show when the uploading process detects an Excel File, which is not supported.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: BatchUploader.autoInterpretBooleans

### Description
Controls if server-side API _BatchUpload.parseUploadData(...)_ will convert imported boolean fields values to actual _Booleans_ or will leave them as _Strings_. The default is true.

Default behavior would interpret boolean values by following rules:

*   Accept all caps permutations of "true"/"false", "yes"/"no", and "null"
*   "T" == true, "F" == false
*   "Y" == true, "N" == false
*   "0" is false
*   empty string is null
*   everything else is true

**Flags**: IRW

---
## Attr: BatchUploader.dataURL

### Description
If set, the batchUploader will copy this value to the queue of "add" requests it sends to the server to actually populate the data. You can use this facility to route the queue to your own server-side logic, for example to add pre- or post-processing.

**Flags**: IRW

---
## Attr: BatchUploader.cancelButton

### Description
Button that cancels the uncommitted upload.

**Flags**: IR

---
## Attr: BatchUploader.showUploadForm

### Description
Should the [BatchUploader.uploadForm](#attr-batchuploaderuploadform) be displayed.

Setting this value to false will suppress the default upload interface for the BatchUploader. In this case sample data may be uploaded directly via the [BatchUploader.uploadData](#method-batchuploaderuploaddata) method.

**Flags**: IRA

---
## Attr: BatchUploader.uploadButtonTitle

### Description
Title for the [upload button](#attr-batchuploaderuploadbutton).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: BatchUploader.uploadFieldPrefix

### Description
String to prepend to the names of the additional fields specified in [BatchUploader.uploadFormFields](#attr-batchuploaderuploadformfields) before they are stored in the HttpSession on the server. This property provides a basic namespace facility, allowing you to avoid name collisions with existing session attributes.

Example usage: if you have an additional field called "someDate" and you set uploadFieldPrefix to "myFields\_", your additionalFormField will be available as an HttpSession attribute called "myFields\_someDate"

**Flags**: IRW

---
## Attr: BatchUploader.uploadDataSource

### Description
DataSource used to save uploaded records. Should have an operation of type "add".

Be careful to note that this is the DataSource representing your data as it will be persisted to your server. It is completely different from the special "batchUpload" DataSource which is used purely as a medium to upload the raw data to the server in the first place.

**Flags**: IR

---
## Attr: BatchUploader.nextButtonTitle

### Description
Title for the [next error button](#attr-batchuploadernextbutton).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: BatchUploader.uploadFormFields

### Description
Optional fields for the uploadForm.

**Flags**: IR

---
## Attr: BatchUploader.errorMessageDelimiterOrEndOfLine

### Description
Error message to show when the uploading process detects a missing delimiter or end of line after quoted value in the first line.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: BatchUploader.dataFormat

### Description
Format to assume for user-provided data. Use [ImportFormat](../reference_2.md#type-importformat) "auto" for auto-detection.

**Flags**: IR

---
## Attr: BatchUploader.errorMessageInputType

### Description
Error message to show when the uploading process detects an invalid inputType.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: BatchUploader.grid

### Description
Grid which will show a preview of data to be uploaded, with errors flagged

**Flags**: IR

---
## Attr: BatchUploader.warnOnCancel

### Description
If set, indicates that a warning dialog should be shown when Cancel is clicked, asking the user to confirm that this is really what they want to do. The actual warning message is specified with [BatchUploader.cancelConfirmMessage](#attr-batchuploadercancelconfirmmessage)

**Flags**: IRW

---
## Attr: BatchUploader.requestProperties

### Description
Object containing properties to send with every "add" request this batchUploader sends.

**Flags**: IRW

---
## Attr: BatchUploader.errorMessageUnterminatedQuote

### Description
Error message to show when the uploading process detects an unterminated quote string in the first line.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: BatchUploader.defaultDelimiter

### Description
The delimiter to use when importing character-delimited files. The default is comma (CSV).

**Deprecated**

**Flags**: IRW

---
## Attr: BatchUploader.showCommitConfirmation

### Description
Whether to show the [commit message](#attr-batchuploadercommitconfirmationmessage) after data is successfully committed.

**Flags**: IR

---
## Attr: BatchUploader.gridFields

### Description
Fields to apply to [BatchUploader.grid](#attr-batchuploadergrid). These will override the field definitions in the [BatchUploader.uploadDataSource](#attr-batchuploaderuploaddatasource) on a field by field basis, as described under [DataBoundComponent.fields](DataBoundComponent.md#attr-databoundcomponentfields).

**Flags**: IRW

---
## Attr: BatchUploader.commitConfirmationMessage

### Description
Message to display after data has been committed, when [showCommitConfirmation](#attr-batchuploadershowcommitconfirmation) is true.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: BatchUploader.partialCommitPrompt

### Description
If [BatchUploader.partialCommit](#attr-batchuploaderpartialcommit) is set to "prompt", the text to display to the user in the confirmation dialog. By default, this text is "There are errors in your data so it cannot all be saved. If you proceed, you will lose the records with errors. Click 'OK' to proceed anyway, or 'Cancel' to return to your data"

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: BatchUploader.allRecordsInErrorMessage

### Description
Message to display when the user clicks "Commit" but there is nothing we can commit because every row in the grid has errors

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: BatchUploader.uploadQuoteString

### Description
The character used to quote strings. The default is double quotes.

**Flags**: IRW

---
## Attr: BatchUploader.commitButton

### Description
Button that commits changes once the user is happy with the data.

**Flags**: IR

---
## Attr: BatchUploader.nextButton

### Description
Button that scrolls grid to the next error.

**Flags**: IR

---
## Attr: BatchUploader.uploadButton

### Description
Button that triggers the upload.

**Flags**: IR

---
## Attr: BatchUploader.partialCommit

### Description
Specifies what action to take if the user attempts to commit a partially validated set of data (ie, one that still contains some errors).

**Flags**: IRW

---
## Attr: BatchUploader.discardedColumnsMessage

### Description
Message displayed when columns in the imported file were discarded and [BatchUploader.displayDiscardedColumns](#attr-batchuploaderdisplaydiscardedcolumns) is true. Within this message, ${discardedColumns} can be used to show a comma separated list of the column names that were discarded (example: "price, saleDate, total").

Default message is: "The following columns in your uploaded file were ignored because they did not match any of the expected column names: ${discardedColumns}"

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: BatchUploader.errorMessageUndeterminedDelimiter

### Description
Error message to show when the uploading process is unable to detect the delimiter.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: BatchUploader.updatesRolledBackMessage

### Description
Message to display if at least one update was rolled back due to errors in another row. See the [transactions overview](DataSource.md#attr-datasourceautojointransactions) for details of SmartClient's automatic transactional updates feature

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: BatchUploader.errorMessageRowsNotParsed

### Description
Error message to show when the uploaded file has rows other than the first row that could not be parsed.

This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed.

The following variables are available to be used in this message:

*   goodRowCount: Total rows that were parsed correctly.
*   totalRows: Total rows to be parsed in the uploaded file.
*   firstBadRow: First row that could not be parsed.
*   badRowCount: Total rows that could not be parsed.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: BatchUploader.cancelButtonTitle

### Description
Title for the [cancel button](#attr-batchuploadercancelbutton).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: BatchUploader.displayDiscardedColumns

### Description
If columns were present in the imported data that were discarded because they could not be matched to any DataSource fields, whether these should be displayed to the user, using the [BatchUploader.discardedColumnsMessage](#attr-batchuploaderdiscardedcolumnsmessage) shown within the [BatchUploader.uploadStatusMessages](#attr-batchuploaderuploadstatusmessages) component.

**Flags**: IR

---
## Attr: BatchUploader.partialCommitConfirmationMessage

### Description
Message to display after data has been committed, when [showCommitConfirmation](#attr-batchuploadershowcommitconfirmation) is true.

### Groups

- i18nMessages

**Flags**: IR

---
## Method: BatchUploader.previewShown

### Description
Notification method fired when the [BatchUploader.grid](#attr-batchuploadergrid) is populated with a new set of data for the user to preview before commit.

This notification occurs after the user has uploaded a new data file, the data has been processed on the server, and the preview grid populated with the data ready for committing. Developers may use this notification to examine or modify the data set to be uploaded. The [ListGrid.data](ListGrid_1.md#attr-listgriddata) object will be populated with the array of uploaded records, and standard grid APIs such as [ListGrid.getRowErrors](ListGrid_2.md#method-listgridgetrowerrors), [ListGrid.setEditValue](ListGrid_2.md#method-listgridseteditvalue), etc may be used to interact with this data.

Note that developers wishing to manipulate the uploaded data can also do this on the server side when user hits the commit button to submit the data to the [BatchUploader.uploadDataSource](#attr-batchuploaderuploaddatasource). This can be achieved by setting the [BatchUploader.uploadOperation](#attr-batchuploaderuploadoperation) to call a custom ["add" type operation](DataSource.md#attr-datasourceoperationbindings) on the target dataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| grid | [ListGrid](#type-listgrid) | false | — | The [BatchUploader.grid](#attr-batchuploadergrid) autoChild. |

### See Also

- [BatchUploader.beforeCommit](#method-batchuploaderbeforecommit)

---
## Method: BatchUploader.beforeCommit

### Description
Notification method fired when the [BatchUploader.commitButton](#attr-batchuploadercommitbutton) is clicked.

This notification occurs before actually committing data to the server. It allows to make changes to the data after user edits, but before it will be sent to server.

Read also [BatchUploader.previewShown](#method-batchuploaderpreviewshown) docs for details how to change data in grid and for possibility to interrupt upload process on the server as well.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| grid | [ListGrid](#type-listgrid) | false | — | The [BatchUploader.grid](#attr-batchuploadergrid) autoChild. |

### See Also

- [BatchUploader.previewShown](#method-batchuploaderpreviewshown)

---
## Method: BatchUploader.uploadData

### Description
This method assumes a developer has sample data in memory (for example a csv-formatted string), and invokes the dataSource upload operation directly, bypassing the uploadForm.

The sample data will be available on the server via `values.pasteData`. This usage is expected and understood by the server side batchUpload dataSource.

This method is most commonly used in conjunction with [showUploadForm:false](#attr-batchuploadershowuploadform).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [String](#type-string) | false | — | formatted data to upload |

**Flags**: A

---
