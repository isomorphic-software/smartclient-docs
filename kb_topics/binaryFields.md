# Binary Fields

[← Back to API Index](../reference.md)

---

## KB Topic: Binary Fields

### Description
_Note: This overview discusses the handling of Binary fields with the SmartClient server. If you're looking for general information about file upload in SmartClient you may also be interested in the [Uploading Files](upload.md#kb-topic-uploading-files) documentation topic._

When using the SmartClient Server framework (included in Pro Edition or better) you can declare a field of type "binary", or certain specific binary types such as "imageFile".

UI components such as [ListGrid](../classes/ListGrid_1.md#class-listgrid) and [FileItem](../classes/FileItem.md#class-fileitem) will offer UIs to download, view and upload files stored in a binary field, as well as some other custom handling such as [sorting by fileName](../classes/ListGrid_1.md#attr-listgridsortbinarybyfilename). [DataSource.downloadFile](../classes/DataSource.md#method-datasourcedownloadfile) and [DataSource.viewFile](../classes/DataSource.md#method-datasourceviewfile) can be used to programmatically trigger download/viewing as well. Note that these automatic features, and components like [TileGrid](../classes/TileGrid.md#class-tilegrid) that make use of them, only work correctly for DataSources that declare a valid [primaryKey](../classes/DataSourceField.md#attr-datasourcefieldprimarykey) field.

If you would like to obtain a URL to the binary data (for example to use as [Img.src](../classes/Img.md#attr-imgsrc)), you can use the [DataSource.getFileURL](../classes/DataSource.md#method-datasourcegetfileurl) API.

As covered under the ["binary" field type description](../reference_2.md#type-fieldtype), binary fields imply 3 other related metadata fields named after the binary field, which store the file size, file name and date of creation. Typically you do not need to add these fields to the dataSource yourself, because the SmartClient Server will implicitly create them if they do not exist. You only need to declare one or more of these fields yourself if you need non-default settings - for example, if you have a need to support filenames longer than 255 characters. If you do need non-default settings, simply declare the metadata field(s) in the normal way. If you do this, note that you become responsible for ensuring that the fields are correctly declared: in particular, you must ensure that you declare the correct type for each field (`text`, `integer` and `datetime` for `_filename`, `_filesize` and `_date_created`, respectively)

When using one of the built-in server DataSource types (SQL, JPA, Hibernate), these metadata fields, UI controls and APIs will work with no special effort - just declare a binary field. For JPA or Hibernate the Java getter/setter for the binary field must be of type byte\[\] or Byte\[\] (this is imposed by the ORM system); if you are using the SQL DataSource, no additional declarations are required unless you are using [DataSource.beanClassName](../classes/DataSource.md#attr-datasourcebeanclassname), in which case you must add getters/setters of type InputStream, or one of the types listed for JPA/Hibernate.

For metadata fields like the file size, providing storage for the metadata fields (SQL columns or JPA/Hibernate getter/setters) is optional but highly recommended. If you don't want a particular metadata field, you can declare a `<field>` for it explicitly and set ignore="true". **Note:** If you decide not to store the "\_filename" metadata element, the built-in binary UI controls in components like ListGrid, mentioned above, do not work properly. In the absence of a filename metadata field, it is necessary to set [mime-type](../classes/DataSourceField.md#attr-datasourcefieldmimetype) on the binary field - otherwise, we can't make a reasonable guess at a MIME type, so the browser tends not to know what to do with the downloaded content. Omiting the file size metadata will simply cause the browser not to show a progress dialog during download, or not to show an accurate one.

**Downloading from binary fields**

If writing a custom DataSource or writing a [DMI](../classes/DMI.md#class-dmi), implement the "downloadFile" and "viewFile" operationTypes, and return data for a single Record which has binary data as the field value for the binary field - accepted types are InputStream, byte\[\], java.sql.Blob or String.

For example, you could return a Java bean with a getter method which returns a byte\[\], and which is named after the binaryField using Java Beans conventions: `get_FieldName_()`. Or, return a Java Map where a byte\[\] is stored under a key named the same as the binary field's name.

As discussed under [FieldType](../reference_2.md#type-fieldtype), additional metadata fields are implied when you declare a binary field. Returning a value for the "\_filesize" field will allow the browser to show progress of the download. Returning a value for the "\_filename" field will cause the downloaded file to be named after the "\_filename" value.

Refer to *this example* to see how this case works.

**Uploading to binary fields**

Again with the built-in server DataSource types, no special effort is required.

For a custom DataSource, an upload from a [FileItem](../classes/FileItem.md#class-fileitem) control (the default upload control) is treated just like an ordinary "add" or "update" DataSource operation. The uploaded file(s), if any, are available from the server-side API `dsRequest.getUploadedFile()`. Metadata fields such as "\_filename" can be populated from the data in the returned ISCFileItem.

Refer to *this example* to see how this case works.

**Binary fields and normal "fetch"**

For an ordinary "fetch" operation, it's generally useless to return data for a binary field, because in most cases code running in the browser would not be able to do anything with a binary value (such as invoke a PDF viewing plugin). For this reason the SmartClient Server will automatically omit values of type InputStream, byte\[\] or Blob during a normal "fetch".

However you can deliver the binary data to the browser by transforming it to a Base64-encoded String by setting [DataSourceField.encodeInResponse](../classes/DataSourceField.md#attr-datasourcefieldencodeinresponse) on your `<field>` declaration. This can be used with certain browser features such as [image data URIs](https://www.google.com/search?q=image+data+uri), but note that some older browsers (notably IE7 and earlier) do not support data URIs.

Refer to *this example* to see how this case works.

**Downloads unrelated to binary fields**

If you want to download or view a file that is not stored in a DataSource record, for example, you want to dynamically generate a report of some kind on the fly, any [DMI](../classes/DMI.md#class-dmi) can return a binary response by calling the server-side API `RPCManager.doCustomResponse()` and writing binary data directly to the ServletResponse outputStream.

It's typical to represent an operation that returns a binary stream as a DataSource request with operationType "fetch", especially if it takes Criteria that identify DataSource Records that will be used to create the binary stream.

When initiating such a download, set [RPCRequest.downloadResult](../classes/RPCRequest.md#attr-rpcrequestdownloadresult) via the `requestProperties` argument of [DataSource.fetchData](../classes/DataSource.md#method-datasourcefetchdata) so that the client-side framework knows that a download will occur instead of a normal response. In this case, callbacks will not be fired because code in the browser does not receive notification that the download has initiated or has completed.

Refer to *this example* to see how this case works.

**Binary handling without the SmartClient Server**

To download or view files with the SmartClient Server, you can write a servlet that streams back binary data. For a download, you can then redirect the main page to the servlet by setting window.location - be sure the download can never fail if you this, because any error message returned by the server in lieu of a file will replace the application instead of triggering a "Save As.." dialog.

To view a file, you can open a new browser window to the URL of the servlet.

Refer to *this example* to see how this case works.

**The Capture property in FileItem and UploadItem components**

The [capture](../classes/FileItem.md#attr-fileitemcapture) property provides a straightforward way to leverage the functionality of a mobile device's camera for capturing media. When it is set on a file upload field, it triggers the media capture interface only when the application is used on a mobile device. This means, the use of this property has no effect on desktop browsers.

It is crucial to consider the additional properties [FileItem.accept](../classes/FileItem.md#attr-fileitemaccept) and [DataSourceField.mimeType](../classes/DataSourceField.md#attr-datasourcefieldmimetype) when using the "capture" property. These properties enable the specification of the file types that can be captured and loaded into the corresponding components. By defining appropriate values for these properties, the selection of allowed media formats can be limited, which is useful for ensuring compatibility and security within the application.

---
