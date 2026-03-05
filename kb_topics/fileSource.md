# FileSource Operations

[← Back to API Index](../reference.md)

---

## KB Topic: FileSource Operations

### Description
These APIs allow a [DataSource](../classes/DataSource_1.md#class-datasource) to be used as a way to store files in a DataSource that might otherwise be stored in a filesystem on the server. They are implemented by sending requests to the server with a special [operationType](../reference.md#type-dsoperationtype).

FileSource operations use standardized field names: fileName, fileType, fileFormat, fileContents, fileSize, fileLastModified and optionally fileVersion. These are translated on the server to native field names for the [DataSource](../classes/DataSource_1.md#class-datasource), determined according to the DataSource configuration for [fileNameField](../classes/DataSource_1.md#attr-datasourcefilenamefield), [fileTypeField](../classes/DataSource_1.md#attr-datasourcefiletypefield), [fileFormatField](../classes/DataSource_1.md#attr-datasourcefileformatfield), [fileContentsField](../classes/DataSource_1.md#attr-datasourcefilecontentsfield), [fileLastModifiedField](../classes/DataSource_1.md#attr-datasourcefilelastmodifiedfield), and [fileVersionField](../classes/DataSource_1.md#attr-datasourcefileversionfield).

### Related

- [DataSource.makeFileSpec](../classes/DataSource.md#classmethod-datasourcemakefilespec)
- [Callbacks.HasFileCallback](../classes/Callbacks.md#method-callbackshasfilecallback)
- [Callbacks.HasFileVersionCallback](../classes/Callbacks.md#method-callbackshasfileversioncallback)
- [Callbacks.GetFileCallback](../classes/Callbacks.md#method-callbacksgetfilecallback)
- [Callbacks.GetFileVersionCallback](../classes/Callbacks.md#method-callbacksgetfileversioncallback)
- [DataSource.getFile](../classes/DataSource_1.md#method-datasourcegetfile)
- [DataSource.hasFile](../classes/DataSource_1.md#method-datasourcehasfile)
- [DataSource.listFiles](../classes/DataSource_1.md#method-datasourcelistfiles)
- [DataSource.saveFile](../classes/DataSource_1.md#method-datasourcesavefile)
- [DataSource.renameFile](../classes/DataSource_1.md#method-datasourcerenamefile)
- [DataSource.removeFile](../classes/DataSource_1.md#method-datasourceremovefile)
- [DataSource.listFileVersions](../classes/DataSource_1.md#method-datasourcelistfileversions)
- [DataSource.getFileVersion](../classes/DataSource_1.md#method-datasourcegetfileversion)
- [DataSource.hasFileVersion](../classes/DataSource_1.md#method-datasourcehasfileversion)
- [DataSource.removeFileVersion](../classes/DataSource_1.md#method-datasourceremovefileversion)
- [FileSpec](../reference.md#object-filespec)
- [DataSource.fileNameField](../classes/DataSource_1.md#attr-datasourcefilenamefield)
- [DataSource.fileTypeField](../classes/DataSource_1.md#attr-datasourcefiletypefield)
- [DataSource.fileFormatField](../classes/DataSource_1.md#attr-datasourcefileformatfield)
- [DataSource.fileContentsField](../classes/DataSource_1.md#attr-datasourcefilecontentsfield)
- [DataSource.fileLastModifiedField](../classes/DataSource_1.md#attr-datasourcefilelastmodifiedfield)
- [DataSource.fileVersionField](../classes/DataSource_1.md#attr-datasourcefileversionfield)
- [DataSource.maxFileVersions](../classes/DataSource_1.md#attr-datasourcemaxfileversions)
- [DataSource.projectFileKey](../classes/DataSource_1.md#attr-datasourceprojectfilekey)
- [DataSource.projectFileLocations](../classes/DataSource_1.md#attr-datasourceprojectfilelocations)

### See Also

- [DataSource](../classes/DataSource_1.md#class-datasource)

---
