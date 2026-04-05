# Reify Documentation

[← Back to API Index](../reference.md)

---

## Class: Reify

*Inherits from:* [VLayout](../reference.md#class-vlayout)

### Description
An application available within [Reify OnSite](../kb_topics/reifyOnSite.md#kb-topic-reify-onsite) that allows developers to create and manage SmartClient screens and datasources. Only **internal framework code** can create an instance of the Reify tool - do not try it directly in your applications. If you want to create visual tools similar to Reify, see [the Dashboards & Tools framework overview](../kb_topics/devTools.md#kb-topic-dashboards--tools-framework-overview).

Note that in the SmartClient SDK, this class present only to provide [Reify](../kb_topics/reifyForDevelopers.md#kb-topic-reify-for-developers) utility class method APIs, and is not an instantiable widget. For example, you can call [Reify.getMockDS](#classmethod-reifygetmockds) to export a [DataSource](DataSource.md#class-datasource) as XML-formatted values and metadata for importing into Reify to create a [MockDataSource](MockDataSource.md#class-mockdatasource).

### Groups

- reify

---
## ClassAttr: Reify.serverURL

### Description
URL of Reify server to use when calling [Reify.loadProject](#method-reifyloadproject). This URL is assumed to only specify the server root, so [Reify.projectLoaderPath](#classattr-reifyprojectloaderpath) will be appended to it when sending the actual request. Can be overridden by [LoadProjectSettings.serverURL](LoadProjectSettings.md#attr-loadprojectsettingsserverurl).

Note that, unless this URL is on your local VPN, it is recommended to use `https` to protect your login credentials.

**Flags**: IRW

---
## ClassAttr: Reify.projectLoaderPath

### Description
Sets the path to reach the [ProjectLoaderServlet](../kb_topics/servletDetails.md#kb-topic-the-core-and-optional-smartclient-servlets) relative to the base [Reify.serverURL](#classattr-reifyserverurl). Can be overridden by [LoadProjectSettings.projectLoaderPath](LoadProjectSettings.md#attr-loadprojectsettingsprojectloaderpath).

**Flags**: IRW

---
## ClassAttr: Reify.userName

### Description
Account name to use for authenticating with the Reify server when calling [Reify.loadProject](#method-reifyloadproject). If proper credentials are not provided the project will not be loaded. Can be overridden by [LoadProjectSettings.userName](LoadProjectSettings.md#attr-loadprojectsettingsusername).

Note that you can set your email address into this property instead of your user name, and the server should still be able to authenticate you for project loading.

### See Also

- [Reify.password](#classattr-reifypassword)

**Flags**: IRW

---
## ClassAttr: Reify.password

### Description
Account password to use for authenticating with the Reify server when calling [Reify.loadProject](#method-reifyloadproject). If proper credentials are not provided the project will not be loaded. Can be overridden by [LoadProjectSettings.userName](LoadProjectSettings.md#attr-loadprojectsettingsusername).

### See Also

- [Reify.userName](#classattr-reifyusername)

**Flags**: IRW

---
## ClassAttr: Reify.verifyDataSources

### Description
Controls whether [DataSource verification](LoadProjectSettings.md#attr-loadprojectsettingsverifydatasources) is enabled by default for all [loadProject](RPCManager.md#classmethod-rpcmanagerloadproject) operations.

**Flags**: IR

---
## Attr: Reify.projectDataSource

### Description
The [DataSource](DataSource.md#class-datasource) to use for saving the project, using fileSource operations. If not set, the property defaults to "vbProjects" except in hostedMode where "isc\_hostedProjects" is the default.

### Groups

- reify

**Flags**: IR

---
## ClassMethod: Reify.showMockDS

### Description
Shows the result of running [Reify.getMockDS](#classmethod-reifygetmockds) in a [modal window](ModalWindow.md#class-modalwindow) so it can be copied and pasted as needed into [Reify](../kb_topics/reifyForDevelopers.md#kb-topic-reify-for-developers) or elsewhere.

Note that the callback is fired when the window is closed, not when it's populated.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsNames | [Array of String](#type-array-of-string)|[String](#type-string) | false | — | [ID](DataSource.md#attr-datasourceid)s of the desired DataSources |
| callback | [MockDSExportCallback](#type-mockdsexportcallback) | false | — | called with the complete export or serialization |
| settings | [MockDSExportSettings](#type-mockdsexportsettings) | false | — | controls format and what records and metadata to include |

---
## ClassMethod: Reify.setUserName

### Description
Setter for [Reify.userName](#classattr-reifyusername).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| userName | [String](#type-string) | false | — | — |

---
## ClassMethod: Reify.getMockDS

### Description
Exports or serializes the specified [DataSources](DataSource.md#class-datasource) using the provided settings.

The "reifyCSV" [format](MockDSExportSettings.md#attr-mockdsexportsettingsformat) generates comma-separated values to paste into the DataSource creation wizard in [Reify](../kb_topics/reifyForDevelopers.md#kb-topic-reify-for-developers). The use case for the other two formats is, if you have a SmartClient application, and you plan to load [MockDataSources](MockDataSource.md#class-mockdatasource) to enable people to add screens to your application using Reify, you may want to test your application with the MockDataSources to ensure they have the right data to allow your application to function (for example, that records in one MockDataSource that are related to another MockDataSource match up). Similarly, you may want to test any custom classes that you upload to Reify in a standalone file using [MockDataSources](MockDataSource.md#class-mockdatasource).

You can customize the `settings`, such as [numRows](MockDSExportSettings.md#attr-mockdsexportsettingsnumrows) (or [numLevels](MockDSExportSettings.md#attr-mockdsexportsettingsnumlevels) for tree-DataSources) to keep the data volume returned by the export low. When related DataSources are present, all related records will be included in the export, even if `numRows` is exceeded. If this is too much data, [criteria](MockDSExportSettings.md#attr-mockdsexportsettingscriteria) can be used to further restrict exported records. Note that `settings` supports an array of [requestProperties](MockDSExportSettings.md#attr-mockdsexportsettingsrequestproperties), so that you can provide unique configuration for each DataSource being exported, rather than only global configuration.

Unless you need programmatic or expert control over the settings, you will likely find it easier to use the "Reify Export" button in the [DataSources tab](../kb_topics/dataSourcesTab.md#kb-topic-datasources-tab). as when using that route, useful global and per-DataSources settings can be configured in an intuitively-arranged popup dialog.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsNames | [Array of String](#type-array-of-string)|[String](#type-string) | false | — | [ID](DataSource.md#attr-datasourceid)s of the desired DataSources |
| callback | [MockDSExportCallback](#type-mockdsexportcallback) | false | — | called with the complete export or serialization |
| settings | [MockDSExportSettings](#type-mockdsexportsettings) | false | — | controls format and what records and metadata to include |

### See Also

- [reifyForDevelopers](../kb_topics/reifyForDevelopers.md#kb-topic-reify-for-developers)
- [Reify.showMockDS](#classmethod-reifyshowmockds)

---
## ClassMethod: Reify.saveProject

### Description
Saves a loaded [Project](Project.md#class-project) to a file on the server, using the `saveFile` built-in RPC. The file can later be loaded via [Reify.loadSavedProject](#classmethod-reifyloadsavedproject) to recreate the project without contacting a Reify server.

By default, the saved format is determined by how the project was loaded. If the project was loaded with [includeXML:true](#loadprojectsettingsincludexml), only the original XML definitions are saved — these are the verbatim strings from the Reify server, with no re-serialization or round-tripping. Otherwise, the JavaScript component code is saved.

The optional `format` parameter overrides this default:

*   **"json"** – saves only the JavaScript `code` representation
*   **"xml"** – saves only the `xml` representation. Requires [includeXML:true](#loadprojectsettingsincludexml) to have been set when the project was loaded.
*   **"both"** – saves both `code` and `xml` (when present)

Note: [Project.createScreen](Project.md#method-projectcreatescreen) requires the `code` property. Files saved with only `xml` (the default when `includeXML` was used, or format "xml") cannot be loaded via [Reify.loadSavedProject](#classmethod-reifyloadsavedproject) for screen creation. Use format "both" or "json" to produce a file suitable for [Reify.loadSavedProject](#classmethod-reifyloadsavedproject).

The `saveFile` built-in method must be enabled in `server.properties`:

```
 RPCManager.enabledBuiltinMethods: saveFile
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| project | [Project](#type-project) | false | — | a loaded project |
| path | [String](#type-string) | false | — | server path relative to the webRoot (e.g. "shared/myApp.proj.json") |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | called on completion |
| format | [String](#type-string) | true | — | "json", "xml", "both", or null for auto-detect |

### See Also

- [Reify.loadSavedProject](#classmethod-reifyloadsavedproject)

---
## ClassMethod: Reify.setServerURL

### Description
Setter for [Reify.serverURL](#classattr-reifyserverurl).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| serverURL | [URL](../reference_2.md#type-url) | false | — | — |

---
## ClassMethod: Reify.setProjectLoaderPath

### Description
Setter for [Reify.projectLoaderPath](#classattr-reifyprojectloaderpath).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| path | [String](#type-string) | false | — | — |

---
## ClassMethod: Reify.setPassword

### Description
Setter for [Reify.password](#classattr-reifypassword).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| password | [String](#type-string) | false | — | — |

---
## ClassMethod: Reify.loadProject

### Description
Loads projects from the [reify](../kb_topics/reify.md#kb-topic-reify-overview) server specified by [Reify.serverURL](#classattr-reifyserverurl) (or [LoadProjectSettings.serverURL](LoadProjectSettings.md#attr-loadprojectsettingsserverurl)) using the [ProjectLoaderServlet](../kb_topics/servletDetails.md#kb-topic-the-core-and-optional-smartclient-servlets), reachable at the relative path [Reify.projectLoaderPath](#classattr-reifyprojectloaderpath) (or [LoadProjectSettings.projectLoaderPath](LoadProjectSettings.md#attr-loadprojectsettingsprojectloaderpath)) underneath the server URL, and fires the given callback after the project has been cached. When a project is loaded, all of its DataSources and screens (except where explicitly overridden by settings) are also cached in the project.

See [RPCManager.loadProject](RPCManager.md#classmethod-rpcmanagerloadproject) for further details.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| projectNames | [String](#type-string) | false | — | Comma-separated string containing the names of project(s) to load. |
| callback | [LoadProjectCallback](#type-loadprojectcallback) | false | — | Callback for notification of completion of project(s) loaded and screens cached. |
| settings | [LoadProjectSettings](#type-loadprojectsettings) | false | — | Settings applicable to the loadProject operation. |

### See Also

- [Reify](#class-reify)

---
## ClassMethod: Reify.loadSavedProject

### Description
Loads a [Project](Project.md#class-project) from a file on the server previously saved by [Reify.saveProject](#method-reifysaveproject), without contacting a Reify server.

A saved project file is a JSON envelope containing each screen and DataSource definition. Each definition includes the JavaScript component code (the `code` property) and, when the project was originally loaded with [includeXML:true](#loadprojectsettingsincludexml), the original XML source as well (the `xml` property). Both representations are preserved through save/load round-trips.

The resulting [Project](Project.md#class-project) is cached the same way as one loaded via [Reify.loadProject](#method-reifyloadproject), and screens can be created via [Project.createScreen](Project.md#method-projectcreatescreen).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| path | [String](#type-string) | false | — | server path relative to the webRoot (e.g. "shared/myApp.proj.json") |
| callback | [LoadProjectCallback](#type-loadprojectcallback) | false | — | called with the loaded [Project](Project.md#class-project) |
| settings | [LoadProjectSettings](#type-loadprojectsettings) | true | — | optional settings for project loading |

### See Also

- [Reify.saveProject](#method-reifysaveproject)

---
## Method: Reify.loadProject

### Description
Loads an existing project from [Reify.projectDataSource](#attr-reifyprojectdatasource) within Reify making it the current project. If project cannot be found a new project will be created and loaded.

The last accessed screen within the project is restored to the current screen.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| projectName | [String](#type-string) | false | — | the name of the project to load |
| ownerId | [String](#type-string) | true | — | optional ID of the project owner |
| callback | [Function](#type-function) | true | — | optional callback to fire when the project has been loaded |

---
