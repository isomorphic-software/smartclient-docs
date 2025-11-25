# Uploading Files

[← Back to API Index](../main.md)

---

## KB Topic: Uploading Files

### Description
SmartClient provides special client and server-side support for file upload that allows uploaded files to be treated like ordinary DataSource fields. This includes:

*   the [FileItem](../classes/FileItem.md#class-fileitem) and [MultiFileItem](../classes/MultiFileItem.md#class-multifileitem) FormItems that enable users to upload one or more files as a background operation, without leaving the current page
*   server-side support that allows binary uploads to be treated as a normal DataSource field values, with all other aspects of server-side integration unchanged
*   built-in SQL & Hibernate DataSource support that can store and retrieve uploaded files from SQL databases

The following documentation assumes you are using the SmartClient Java Server. If you are not, skip to the sections near the end of this document.  
_Note: This documentation topic is concerned specifically with file upload. Developers looking for a general discussion of how Binary fields are handled with the SmartClient server may also be interested in the [Binary Fields](binaryFields.md#kb-topic-binary-fields) overview._

**Single file upload: "binary" field type**

To use SmartClient's client-server upload system, you use a DataSource field of [type](../classes/DataSourceField.md#attr-datasourcefieldtype) "binary". By default, a DynamicForm bound to a DataSource with a field of type "binary" will use the [FileItem](../classes/FileItem.md#class-fileitem), which displays a standard HTML `<input type="upload">` form control.

When you call [DynamicForm.saveData](../classes/DynamicForm.md#method-dynamicformsavedata) on a DynamicForm containing a FileItem, SmartClient processes the save identically to a saveData() call that did not include a file upload:

*   if you are using the built-in SQL connectors via serverType:"sql", the file will be saved to SQL as described under [field type "binary"](../main_2.md#type-fieldtype).
*   if you have server-side business logic, the inbound request may be routed to your business logic via RPCManager dispatch or DMI declarations as normal, your business logic will receive a normal DSRequest, and you are expected to provide a normal DSResponse.

Client-side callbacks, such as the callback passed to saveData(), fire normally.

Note that FileItems cannot be programmatically populated - this is a browser security restriction over which we have no control. This restriction means that we are unable to populate a FileItem with the correct filename when a form is editing an existing record. Also, when you call saveData() on a form that is editing a new record, the FileItem will be cleared on successful completion of the saveData() call; this is a side-effect of the form being placed into "edit" mode. In both of these cases, the fact that the FileItem has been cleared will not cause the persisted binary data to be removed by SmartClient Server on subsequent calls to setData(). If the user selects another file, it will overwrite the existing one; if the FileItem is left blank, the server simply ignores it. If you actually wish to wipe out the value of a binary field, call [updateData()](../classes/DataSource.md#method-datasourceupdatedata) on the underlying dataSource, passing an explicit null value for the binary field.

DataSources can have multiple binary fields, but developers should be aware that you can not submit more than one FileItem in a single form. Developers needing to upload multiple files can either use the [MultiFileItem](../classes/MultiFileItem.md#class-multifileitem), or use multiple DynamicForms (nested in a [VStack](../main.md#class-vstack), or similar), and submit them separately. For an add operation, the pattern would be to perform the initial submission of values for the record and then use the [callback](../classes/DSRequest.md#attr-dsrequestcallback) to apply the primary key value for the new record to the forms with binary fields and save them to the server separately. This approach has the advantage that if an error or timeout occurs, users will not be caught waiting for files to complete uploading before being notified of the failure and having to repeat the entire transaction.  
Note when adding a new record using this pattern, if you have a binary field marked as `required="true"` it should be submitted as part of the initial submission.

**Restricting upload sizes**

The server framework includes mechanisms for setting maximum allowable file sizes. The first, applied using [global configuration properties](server_properties.md#kb-topic-serverproperties-file), is meant to prevent an end user from uploading a file large enough to cause memory issues on the server.

To configure the maximum allowed size of a single uploaded file (disabled by default), set the **fileUpload.maxFileSize** property's value (in bytes):

fileUpload.maxFileSize: 104857600

To configure the maximum combined size of all files in a single request (disabled by default), set the **fileUpload.maxSize** property's value (also in bytes):

fileUpload.maxSize: 209715200

Another configuration property controls the default value of a "binary" DataSourceField's [maxFileSize](../classes/DataSourceField.md#attr-datasourcefieldmaxfilesize) attribute, suitable for managing storage requirements for a given DataSource over time (e.g., limiting images to 100MB).

DSRequest.maxUploadFileSize: 104857600

To configure the maximum number of files in a single request (set to 10 by default), set the **fileUpload.maxFileCount** property's value:

fileUpload.maxFileCount: 10

When a [FileItem](../classes/FileItem.md#class-fileitem) or [UploadItem](../classes/UploadItem.md#class-uploaditem) is bound to a "binary" `DataSourceField` with a `maxFileSize` setting, a [`maxFileSize`\-type](../main.md#type-validatortype) validator is automatically added to the item's [validators](../classes/FormItem.md#attr-formitemvalidators). In supported browsers, a `maxFileSize` validator is a client-side check that the size of a file selected for upload does not exceed the field's `maxFileSize`. Note, however, that server-side enforcement of the `maxFileSize` is always required because the user's browser might not support client-side file size checks. Also, any client-side check can be bypassed by a malicious user.

**Processing File Uploads with server-side business logic**

Server-side business logic that processes file uploads may retrieve upload files via the server side API dsRequest.getUploadedFile(_fieldName_). The uploaded file is returned as an instance of ISCFileItem, which provides access to a Java InputStream as well as metadata about the file (size, name). See the server-side JavaDoc (com.isomorphic.\*) for details.

Server-side validation errors may be provided, including validation errors for the uploaded file (such as too large or invalid content), and will be displayed in the form that attempted an upload.

Be aware of the following special concerns when processing file uploads:

*   if you provide your own Java Servlet or JSP that creates an instance of RPCManager in order process SmartClient requests, many APIs of the HttpServletRequest are not safe to call before you have created the RPCManager, passing in the HttpServletRequest. These include getReader(), getParameter() and other commonly called methods. This is a limitation of Java Servlets, not specific to SmartClient
*   unlike other DataSource "add" and "update" operations, you are not expected to return the file as part of the data returned in the DSResponse

**Multi file upload: MultiFileItem**

The MultiFileItem provides an interface for a user to save one or more files that are related to a DataSource record, where each file is represented by a record in a related DataSource.

See the [MultiFileItem](../classes/MultiFileItem.md#class-multifileitem) docs for details.

**Upload without the SmartClient Server**

If it is acceptable that the application will do a full-page reload after the upload completes, you can simply:

*   set [DynamicForm.encoding](../classes/DynamicForm.md#attr-dynamicformencoding) to "multipart"
*   include an [UploadItem](../classes/UploadItem.md#class-uploaditem) to get a basic HTML upload control
*   set [DynamicForm.action](../classes/DynamicForm.md#attr-dynamicformaction) to a URL where you have deployed server-side code to handle the upload
*   call [DynamicForm.submitForm](../classes/DynamicForm.md#method-dynamicformsubmitform) to cause the form to be submitted

This cause the DynamicForm component to submit to the form.action URL like an ordinary HTML `<form>` element. Many [online tutorials](http://www.google.com/search?q=html+file+upload+example) are available which explain how to handle HTML form file upload in various server-side technologies.

Note that when you submitForm(), the only values that will be sent to your actionURL are values for which actual FormItems exist. This differs from saveData(), in which the entire set of [form values](../classes/DynamicForm.md#attr-dynamicformvalues) are always sent. To handle submitting extra values, use [HiddenItem](../classes/HiddenItem.md#class-hiddenitem)s.

For further details, see the [UploadItem](../classes/UploadItem.md#class-uploaditem) docs.

**Background upload without the SmartClient Server**

Achieving background file upload without using the SmartClient server is also possible although considerably more advanced. In addition to the steps above, create a hidden `<iframe>` element in the page, and use [DynamicForm.target](../classes/DynamicForm.md#attr-dynamicformtarget) to target the form submission at this IFRAME. In order receive a callback notification when the upload completes, after processing the file upload, your server should output HTML content for the IFRAME that includes a `<SCRIPT>` block which will navigate out of the IFRAME (generally via the JavaScript global "top") and call a global method you have declared as a callback.

### Related

- [UploadItem](../classes/UploadItem.md#class-uploaditem)
- [FileItem](../classes/FileItem.md#class-fileitem)
- [MultiFileItem](../classes/MultiFileItem.md#class-multifileitem)
- [MultiFilePicker](../main.md#class-multifilepicker)
- [ViewFileItem](../main.md#class-viewfileitem)
- [FileItem.editForm](../classes/FileItem.md#attr-fileitemeditform)
- [FileItem.uploadItem](../classes/FileItem.md#attr-fileitemuploaditem)
- [FileItem.displayForm](../classes/FileItem.md#attr-fileitemdisplayform)
- [FileItem.displayItem](../classes/FileItem.md#attr-fileitemdisplayitem)
- [FileItem.displayCanvas](../classes/FileItem.md#attr-fileitemdisplaycanvas)

---
