# FileSource Operations

[← Back to API Index](../main.md)

---

## KB Topic: FileSource Operations

### Description
These APIs allow a [DataSource](../classes/DataSource.md#class-datasource) to be used as a way to store files in a DataSource that might otherwise be stored in a filesystem on the server. They are implemented by sending requests to the server with a special [operationType](../main.md#type-dsoperationtype).

FileSource operations use standardized field names: fileName, fileType, fileFormat, fileContents, fileSize, fileLastModified and optionally fileVersion. These are translated on the server to native field names for the [DataSource](../classes/DataSource.md#class-datasource), determined according to the DataSource configuration for [fileNameField](../classes/DataSource.md#attr-datasourcefilenamefield), [fileTypeField](../classes/DataSource.md#attr-datasourcefiletypefield), [fileFormatField](../classes/DataSource.md#attr-datasourcefileformatfield), [fileContentsField](../classes/DataSource.md#attr-datasourcefilecontentsfield), [fileLastModifiedField](../classes/DataSource.md#attr-datasourcefilelastmodifiedfield), and [fileVersionField](../classes/DataSource.md#attr-datasourcefileversionfield).

### Related

- [DataSource.makeFileSpec](../classes/DataSource.md#classmethod-datasourcemakefilespec)
- [Callbacks.HasFileCallback](../classes/Callbacks.md#method-callbackshasfilecallback)
- [Callbacks.HasFileVersionCallback](../classes/Callbacks.md#method-callbackshasfileversioncallback)
- [Callbacks.GetFileCallback](../classes/Callbacks.md#method-callbacksgetfilecallback)
- [Callbacks.GetFileVersionCallback](../classes/Callbacks.md#method-callbacksgetfileversioncallback)
- [DataSource.getFile](../classes/DataSource.md#method-datasourcegetfile)
- [DataSource.hasFile](../classes/DataSource.md#method-datasourcehasfile)
- [DataSource.listFiles](../classes/DataSource.md#method-datasourcelistfiles)
- [DataSource.saveFile](../classes/DataSource.md#method-datasourcesavefile)
- [DataSource.renameFile](../classes/DataSource.md#method-datasourcerenamefile)
- [DataSource.removeFile](../classes/DataSource.md#method-datasourceremovefile)
- [DataSource.listFileVersions](../classes/DataSource.md#method-datasourcelistfileversions)
- [DataSource.getFileVersion](../classes/DataSource.md#method-datasourcegetfileversion)
- [DataSource.hasFileVersion](../classes/DataSource.md#method-datasourcehasfileversion)
- [DataSource.removeFileVersion](../classes/DataSource.md#method-datasourceremovefileversion)
- [FileSpec](../main.md#object-filespec)
- [DataSource.fileNameField](../classes/DataSource.md#attr-datasourcefilenamefield)
- [DataSource.fileTypeField](../classes/DataSource.md#attr-datasourcefiletypefield)
- [DataSource.fileFormatField](../classes/DataSource.md#attr-datasourcefileformatfield)
- [DataSource.fileContentsField](../classes/DataSource.md#attr-datasourcefilecontentsfield)
- [DataSource.fileLastModifiedField](../classes/DataSource.md#attr-datasourcefilelastmodifiedfield)
- [DataSource.fileVersionField](../classes/DataSource.md#attr-datasourcefileversionfield)
- [DataSource.maxFileVersions](../classes/DataSource.md#attr-datasourcemaxfileversions)
- [DataSource.projectFileKey](../classes/DataSource.md#attr-datasourceprojectfilekey)
- [DataSource.projectFileLocations](../classes/DataSource.md#attr-datasourceprojectfilelocations)

### See Also

- [DataSource](../classes/DataSource.md#class-datasource)

---
