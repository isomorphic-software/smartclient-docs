# Reify Documentation

[← Back to API Index](../reference.md)

---

## Class: Reify

*Inherits from:* [VLayout](../reference.md#class-vlayout)

### Description
An application available within [Reify OnSite](../kb_topics/reifyOnSite.md#kb-topic-reify-onsite) that allows developers to create and manage SmartClient screens and datasources. Only **internal framework code** can create an instance of the Reify tool - do not try it directly in your applications. If you want to create visual tools similar to Reify, see [the Dashboards & Tools framework overview](../kb_topics/devTools.md#kb-topic-dashboards--tools-framework-overview).

Note that in the SmartClient SDK, this class present only to provide [Reify](../kb_topics/reifyForDevelopers.md#kb-topic-reify-for-developers) utility class method APIs, and is not an instantiable widget. For example, you can call [Reify.getMockDS](#classmethod-reifygetmockds) to export a [DataSource](DataSource_1.md#class-datasource) as XML-formatted values and metadata for importing into Reify to create a [MockDataSource](MockDataSource.md#class-mockdatasource).

### Groups

- reify

---
## ClassAttr: Reify.overlaySourceHues

### Description
Hue angles (0-360) keyed by record source, used by the overlay view to differentiate screens from different Reify origins. The actual border/label colors are derived at show-time by combining these hues with the skin's light/dark mode so overlays always contrast with the page background. Recognized keys: local, remote, remoteDefault, remoteOverride, localStorage.

**Flags**: IRWA

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
## ClassAttr: Reify.overlayActive

### Description
Read-only flag: true while the [overlay\\n view](#classmethod-reifyenableoverlay) is showing.

**Flags**: RA

---
## ClassAttr: Reify.password

### Description
Account password to use for authenticating with the Reify server when calling [Reify.loadProject](#method-reifyloadproject). If proper credentials are not provided the project will not be loaded. Can be overridden by [LoadProjectSettings.userName](LoadProjectSettings.md#attr-loadprojectsettingsusername).

### See Also

- [Reify.userName](#classattr-reifyusername)

**Flags**: IRW

---
## ClassAttr: Reify.SOURCE_LOCAL

### Description
Value of the `source` field in records returned by [Reify.getLoadedProjects](#classmethod-reifygetloadedprojects), [Reify.getLoadedScreens](#classmethod-reifygetloadedscreens), and [Reify.getLoadedDataSources](#classmethod-reifygetloadeddatasources) when the resource was loaded from the local server.

**Flags**: RA

---
## ClassAttr: Reify.SOURCE_REMOTE

### Description
Value of the `source` field in records returned by the `getLoadedXxx()` methods when the resource was loaded from a remote Reify server.

**Flags**: RA

---
## ClassAttr: Reify.defaultReifyURL

### Description
Default URL prefix used by [Reify.getProjectsDS](#classmethod-reifygetprojectsds), [Reify.getScreensDS](#classmethod-reifygetscreensds), and [Reify.getDataSourcesDS](#classmethod-reifygetdatasourcesds) when accessing a remote Reify server. Should point at the remote server's `isomorphic` dir, e.g. `"https://reify.example.com/isomorphic/"`.

When null (the default), the local server's Reify storage is used. Per-call overrides via the `reifyURL` field of the [ReifyDSSettings](../reference.md#object-reifydssettings) object always take precedence.

Cross-origin access requires that the remote server's `IDACall` servlet be configured with appropriate `Access-Control-Allow-Origin` headers.

**Flags**: IRWA

---
## ClassAttr: Reify.overlayMaskOpacity

### Description
Opacity of the page-greying mask shown by the [overlay view](#classmethod-reifyenableoverlay). Range 0.0 (invisible) to 1.0 (opaque).

**Flags**: IRWA

---
## ClassAttr: Reify.overlayMaskColor

### Description
Background color of the page-greying mask shown by the [overlay view](#classmethod-reifyenableoverlay).

**Flags**: IRWA

---
## ClassAttr: Reify.verifyDataSources

### Description
Controls whether [DataSource verification](LoadProjectSettings.md#attr-loadprojectsettingsverifydatasources) is enabled by default for all [loadProject](RPCManager.md#classmethod-rpcmanagerloadproject) operations.

**Flags**: IR

---
## ClassAttr: Reify.overlayKey

### Description
Key combination that activates the [overlay view](#classmethod-reifyenableoverlay).

When the config contains a `keyName` the binding behaves as a press-to-toggle shortcut (registered via [Page.registerKey](Page.md#classmethod-pageregisterkey)). When `keyName` is omitted only modifier flags are present and the overlay uses **hold-to-show** mode — it appears while the modifiers are held and dismisses automatically on release, leaving one hand free for the mouse.

The default is hold-to-show with `Ctrl+Shift` on Windows/Linux and `Cmd+Shift` on Mac. Neither combo conflicts with any browser shortcut because browsers only act on modifier pairs when a third character key is added.

Reassign with [Reify.setOverlayKey](#classmethod-reifysetoverlaykey).

**Flags**: IRWA

---
## Attr: Reify.projectDataSource

### Description
The [DataSource](DataSource_1.md#class-datasource) to use for saving the project, using fileSource operations. If not set, the property defaults to "vbProjects" except in hostedMode where "isc\_hostedProjects" is the default.

### Groups

- reify

**Flags**: IR

---
## ClassMethod: Reify.publishScreen

### Description
Publishes a screen to a viewable URL via the Reify project infrastructure, without requiring a live Reify builder instance. The screen is saved to `vbScreens`, added to a Reify project in `vbProjects`, and a `projectRunner.jsp` URL is constructed that renders the screen on the fly. The callback receives the viewable URL.

This reuses the same project storage and rendering pipeline that [Reify.editInReify](#classmethod-reifyeditinreify) and Reify's own Run button use.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| config | [PublishScreenConfig](#type-publishscreenconfig) | false | — | publish configuration |
| callback | [PublishScreenCallback](#type-publishscreencallback) | true | — | called with the URL |

---
## ClassMethod: Reify.toggleOverlay

### Description
Show the [overlay view](#classmethod-reifyenableoverlay) if it is hidden, or hide it if it is showing.

---
## ClassMethod: Reify.getReifyDataSources

### Description
Get a list of DataSources stored in Reify's DS storage.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [Function](#type-function) | false | — | called with (Array of String dsIds) |

---
## ClassMethod: Reify.registerLoadedScreen

### Description
Add a screen Canvas instance to the loaded-resource registry. Called automatically by [RPCManager.loadScreen](RPCManager.md#classmethod-rpcmanagerloadscreen) (when no project is involved) and by [Project.createScreen](Project.md#method-projectcreatescreen) (which both replaces the project's screen-definition record with one that points at the live Canvas, and arranges for cleanup when the Canvas is destroyed).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canvas | [Canvas](#type-canvas) | false | — | the screen's top-level Canvas instance |
| info | [Object](../reference.md#type-object) | true | — | optional fields: `screenName`, `projectName`, `source`, `reifyURL`, `sourceLabel` |

---
## ClassMethod: Reify.showMockDS

### Description
Shows the result of running [Reify.getMockDS](#classmethod-reifygetmockds) in a [modal window](ModalWindow.md#class-modalwindow) so it can be copied and pasted as needed into [Reify](../kb_topics/reifyForDevelopers.md#kb-topic-reify-for-developers) or elsewhere.

Note that the callback is fired when the window is closed, not when it's populated.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsNames | [Array of String](#type-array-of-string)|[String](#type-string) | false | — | [ID](DataSource_1.md#attr-datasourceid)s of the desired DataSources |
| callback | [MockDSExportCallback](#type-mockdsexportcallback) | false | — | called with the complete export or serialization |
| settings | [MockDSExportSettings](#type-mockdsexportsettings) | false | — | controls format and what records and metadata to include |

---
## ClassMethod: Reify.getDataSourcesDS

### Description
Return a [DataSource](DataSource_1.md#class-datasource) for browsing the list of DataSources in a Reify installation. See [Reify.getProjectsDS](#classmethod-reifygetprojectsds) for behavior, settings, and remote-access details.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [Callback](../reference.md#type-callback) | false | — | called with `(DataSource ds)` |
| settings | [ReifyDSSettings](#type-reifydssettings) | false | — | optional override settings |

---
## ClassMethod: Reify.loadReify

### Description
Load the Reify editor, either inline in the current page or in a new browser window. Returns a [ReifyRemote](ReifyRemote.md#class-reifyremote) via callback that provides a uniform API for controlling and receiving notifications from the Reify instance regardless of how it was loaded.

In **inline mode**, all required Reify modules are dynamically loaded into the current page via [FileLoader.loadModules](FileLoader.md#classmethod-fileloaderloadmodules) and a Reify instance is created.

In **window mode**, Reify is opened in a new browser tab. Communication uses `window.postMessage` by default (same-origin) or RealTime Messaging if `useRTM: true` (cross-origin).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| config | [ReifyLoadConfig](#type-reifyloadconfig) | false | — | configuration |
| callback | [Function](#type-function) | false | — | called with a [ReifyRemote](ReifyRemote.md#class-reifyremote) instance |

---
## ClassMethod: Reify.getScreensDS

### Description
Return a [DataSource](DataSource_1.md#class-datasource) for browsing the list of screens in a Reify installation. See [Reify.getProjectsDS](#classmethod-reifygetprojectsds) for behavior, settings, and remote-access details.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [Callback](../reference.md#type-callback) | false | — | called with `(DataSource ds)` |
| settings | [ReifyDSSettings](#type-reifydssettings) | false | — | optional override settings |

---
## ClassMethod: Reify.getScreenProject

### Description
Determine which Reify project a screen belongs to, if any. A screen belongs to a project if it is listed in the project's screen list. This checks locally cached projects (loaded via [RPCManager.loadProject](RPCManager.md#classmethod-rpcmanagerloadproject)).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| screenName | [String](#type-string) | false | — | name of the screen |

### Returns

`[Project](#type-project)` — the project containing the screen, or null

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
Exports or serializes the specified [DataSources](DataSource_1.md#class-datasource) using the provided settings.

The "reifyCSV" [format](MockDSExportSettings.md#attr-mockdsexportsettingsformat) generates comma-separated values to paste into the DataSource creation wizard in [Reify](../kb_topics/reifyForDevelopers.md#kb-topic-reify-for-developers). The use case for the other two formats is, if you have a SmartClient application, and you plan to load [MockDataSources](MockDataSource.md#class-mockdatasource) to enable people to add screens to your application using Reify, you may want to test your application with the MockDataSources to ensure they have the right data to allow your application to function (for example, that records in one MockDataSource that are related to another MockDataSource match up). Similarly, you may want to test any custom classes that you upload to Reify in a standalone file using [MockDataSources](MockDataSource.md#class-mockdatasource).

You can customize the `settings`, such as [numRows](MockDSExportSettings.md#attr-mockdsexportsettingsnumrows) (or [numLevels](MockDSExportSettings.md#attr-mockdsexportsettingsnumlevels) for tree DataSources) to keep the data volume returned by the export low. When related DataSources are present, all related records will be included in the export, even if `numRows` is exceeded. If this is too much data, [criteria](MockDSExportSettings.md#attr-mockdsexportsettingscriteria) or [perDSCriteria](MockDSExportSettings.md#attr-mockdsexportsettingsperdscriteria) can be used to further restrict exported records. Note that `settings` supports an array of [requestProperties](MockDSExportSettings.md#attr-mockdsexportsettingsrequestproperties), so that you can provide unique configuration for each DataSource being exported, rather than only global configuration.

When exporting interlinked DataSources, set [MockDSExportSettings.followFKDepth](MockDSExportSettings.md#attr-mockdsexportsettingsfollowfkdepth) to automatically discover additional DataSources reachable via foreignKey relationships, so you don't have to manually enumerate every related DataSource.

#### Tree DataSource Handling

When a DataSource has a self-referential [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) (a field that references the same DataSource), it is automatically detected as a [tree DataSource](../kb_topics/treeDataBinding.md#kb-topic-tree-databinding). Tree DataSources are fetched level-by-level: root nodes first, then their children, up to [numLevels](MockDSExportSettings.md#attr-mockdsexportsettingsnumlevels) deep. The [treeRoots](MockDSExportSettings.md#attr-mockdsexportsettingstreeroots) setting can restrict which root nodes are included.

Not every self-referential FK represents a tree hierarchy — for example, a sales order might reference the quotation (also an order) it was created from. The automatic [maxTreeRoots](MockDSExportSettings.md#attr-mockdsexportsettingsmaxtreeroots) check detects these cases by counting root nodes before committing to tree-style fetching. For explicit control, list such DataSources in [MockDSExportSettings.nonTreeDataSources](MockDSExportSettings.md#attr-mockdsexportsettingsnontreedatasources).

#### Large Database Export

When exporting from large production databases, the default behavior of batching all DataSource fetches into a single queued request can exhaust database connection pools. For these scenarios:

*   Set [MockDSExportSettings.sequentialFetching](MockDSExportSettings.md#attr-mockdsexportsettingssequentialfetching) to fetch one DataSource at a time instead of all at once.
*   Use [MockDSExportSettings.perDSCriteria](MockDSExportSettings.md#attr-mockdsexportsettingsperdscriteria) to narrow large tables to relevant subsets (e.g. active records, recent dates).
*   The [MockDSExportSettings.maxTreeRoots](MockDSExportSettings.md#attr-mockdsexportsettingsmaxtreeroots) default of 500 automatically prevents unbounded root-node queries on DataSources where a self-FK is not a real hierarchy.
*   For DataSources you know are not trees, list them in [MockDSExportSettings.nonTreeDataSources](MockDSExportSettings.md#attr-mockdsexportsettingsnontreedatasources) to skip the exploratory root-count query entirely.

Unless you need programmatic or expert control over the settings, you will likely find it easier to use the "Reify Export" button in the [DataSources tab](../kb_topics/dataSourcesTab.md#kb-topic-datasources-tab), as when using that route, useful global and per-DataSource settings can be configured in an intuitively-arranged popup dialog.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsNames | [Array of String](#type-array-of-string)|[String](#type-string) | false | — | [ID](DataSource_1.md#attr-datasourceid)s of the desired DataSources |
| callback | [MockDSExportCallback](#type-mockdsexportcallback) | false | — | called with the complete export or serialization |
| settings | [MockDSExportSettings](#type-mockdsexportsettings) | false | — | controls format and what records and metadata to include |

### See Also

- [reifyForDevelopers](../kb_topics/reifyForDevelopers.md#kb-topic-reify-for-developers)
- [Reify.showMockDS](#classmethod-reifyshowmockds)

---
## ClassMethod: Reify.editInReify

### Description
Save an [EditContext](EditContext.md#class-editcontext)'s component tree (or raw screen XML) to Reify storage and open it in the Reify editor. This is the primary convenience method for the "Dashboards & Tools to Reify" workflow.

The method handles the complete flow:

1.  Serializes the EditContext to screen XML (if `editContext` is provided instead of raw `screenContents`)
2.  Saves the screen to vbScreens via [Reify.saveScreen](#method-reifysavescreen)
3.  Creates a new project or adds the screen to an existing project
4.  Opens Reify via [Reify.loadReify](#classmethod-reifyloadreify) with the project and screen pre-selected

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| config | [EditInReifyConfig](#type-editinreifyconfig) | false | — | configuration |
| callback | [Function](#type-function) | true | — | called with a [ReifyRemote](ReifyRemote.md#class-reifyremote) instance |

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
## ClassMethod: Reify.getLoadedScreens

### Description
Return an Array of records describing every screen currently registered in the loaded-resource registry. See [Reify.getLoadedProjects](#classmethod-reifygetloadedprojects) for the registry overview.

### Returns

`[Array of Object](#type-array-of-object)` — loaded screen records

---
## ClassMethod: Reify.saveScreen

### Description
Save screen content (XML or JSON) to Reify's screen storage (vbScreens). This makes the screen available for use in Reify projects via [Reify.loadReify](#classmethod-reifyloadreify) or [Reify.loadScreenInReify](#classmethod-reifyloadscreeninreify).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| screenName | [String](#type-string) | false | — | name for the screen |
| screenContents | [String](#type-string) | false | — | screen XML or JSON content, as produced by [EditContext.serializeAllEditNodes](EditContext.md#method-editcontextserializealleditnodes) |
| callback | [Function](#type-function) | true | — | called with (DSResponse dsResponse, Object data) |

---
## ClassMethod: Reify.unregisterLoadedDataSource

### Description
Remove a DataSource entry from the loaded-resource registry.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsName | [String](#type-string) | false | — | the DataSource's ID |

---
## ClassMethod: Reify.disableOverlay

### Description
Hide the overlay view, destroying all overlay frames. The loaded screen canvases are untouched. Idempotent.

---
## ClassMethod: Reify.setServerURL

### Description
Setter for [Reify.serverURL](#classattr-reifyserverurl).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| serverURL | [URL](../reference_2.md#type-url) | false | — | — |

---
## ClassMethod: Reify.isDataSourceInReify

### Description
Check whether a DataSource is stored in Reify's DS storage (vbDataSources).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataSourceId | [String](#type-string) | false | — | DataSource ID |
| callback | [Function](#type-function) | false | — | called with (Boolean isStored) |

---
## ClassMethod: Reify.getDataSourceProject

### Description
Determine which cached Reify project a DataSource belongs to, if any.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataSourceId | [String](#type-string) | false | — | DataSource ID |

### Returns

`[Project](#type-project)` — the project containing the DS, or null

---
## ClassMethod: Reify.addScreensToProject

### Description
Add one or more screens to an existing Reify project. The screens must already be saved via [Reify.saveScreen](#method-reifysavescreen). The project is loaded from vbProjects, the screen references are appended, and the project is saved back.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| projectName | [String](#type-string) | false | — | project name |
| screenNames | [Array of String](#type-array-of-string) | false | — | screen names to add |
| callback | [Function](#type-function) | true | — | called with (DSResponse dsResponse, Object data) |

---
## ClassMethod: Reify.registerLoadedDataSource

### Description
Add a [DataSource](DataSource_1.md#class-datasource) reference to the loaded-resource registry. Normally called from [Reify.registerLoadedProject](#classmethod-reifyregisterloadedproject) for project-bundled DSes, but available for application code that loads DSes outside the project flow.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsName | [String](#type-string) | false | — | the DataSource's ID |
| info | [Object](../reference.md#type-object) | true | — | optional fields: `projectName`, `source`, `reifyURL`, `sourceLabel` |

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
## ClassMethod: Reify.unregisterLoadedProject

### Description
Remove a [Project](Project.md#class-project) from the loaded-resource registry, along with all of its screens and DataSources. Called automatically by [Project.destroy](Project.md#method-projectdestroy).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| project | [Project](#type-project) | false | — | the Project to remove |

---
## ClassMethod: Reify.loadScreenInReify

### Description
Open a named screen in Reify for editing. The screen must be stored in Reify's screen storage (vbScreens); if not, a warning is logged and the call fails.

This is the screen equivalent of [Project.loadInReify](Project.md#method-projectloadinreify) and [DataSource.loadInReify](DataSource_1.md#method-datasourceloadinreify). Since screens are not first-class objects in SmartClient (they are Canvas hierarchies returned by [RPCManager.loadScreen](RPCManager.md#classmethod-rpcmanagerloadscreen)), this method is on the Reify class rather than on a Screen instance.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| screenName | [String](#type-string) | false | — | screen to edit |
| config | [ReifyLoadConfig](#type-reifyloadconfig) | false | — | optional config for [Reify.loadReify](#classmethod-reifyloadreify) |
| callback | [Function](#type-function) | false | — | called with [ReifyRemote](ReifyRemote.md#class-reifyremote) |

---
## ClassMethod: Reify.showOverlay

### Description
Show the overlay view with optional dismiss behaviour. Greys out the page and draws a colored frame plus action icons around every loaded Reify screen. Idempotent.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [OverlaySettings](#type-overlaysettings) | true | — | optional dismiss and behaviour configuration |

### See Also

- [Reify.enableOverlay](#classmethod-reifyenableoverlay)

---
## ClassMethod: Reify.getReifyProjects

### Description
Get a list of projects stored in Reify's project storage.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [Function](#type-function) | false | — | called with (Array of String projectNames) |

---
## ClassMethod: Reify.unregisterLoadedScreen

### Description
Remove a screen from the loaded-resource registry. Called automatically when a registered screen Canvas is destroyed (via an observation of [Canvas.destroy](Canvas.md#method-canvasdestroy)).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canvas | [Canvas](#type-canvas) | false | — | the screen's top-level Canvas instance |

---
## ClassMethod: Reify.isScreenInReify

### Description
Check whether a screen is stored in Reify's screen storage (vbScreens).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| screenName | [String](#type-string) | false | — | name of the screen |
| callback | [Function](#type-function) | false | — | called with (Boolean isStored) |

---
## ClassMethod: Reify.createProjectWithScreens

### Description
Create a minimal Reify project that references one or more screens already stored in [vbScreens](#method-reifysavescreen). The project is saved to vbProjects.

If a project with this name already exists, it is overwritten. To add screens to an existing project, use [Reify.addScreensToProject](#classmethod-reifyaddscreenstoproject) instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| projectName | [String](#type-string) | false | — | project name |
| screenNames | [Array of String](#type-array-of-string) | false | — | screen names to include |
| callback | [Function](#type-function) | true | — | called with (DSResponse dsResponse, Object data) |

---
## ClassMethod: Reify.isProjectInReify

### Description
Check whether a project loaded via [RPCManager.loadProject](RPCManager.md#classmethod-rpcmanagerloadproject) is stored in Reify's project storage (vbProjects).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| projectName | [String](#type-string) | false | — | name of the project |
| callback | [Function](#type-function) | false | — | called with (Boolean isStored) |

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
## ClassMethod: Reify.getReifyAssetsInPage

### Description
Find all assets (projects, screens, DataSources) in the current page that are also stored in Reify. This is an async operation since it queries the Reify file storage.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [Function](#type-function) | false | — | called with (Object results) where results has properties: projects (Array), screens (Array), dataSources (Array) |

---
## ClassMethod: Reify.getLoadedScreensDS

### Description
Return a live clientOnly [DataSource](DataSource_1.md#class-datasource) of loaded screen records. See [Reify.getLoadedProjectsDS](#classmethod-reifygetloadedprojectsds).

### Returns

`[DataSource](#type-datasource)` — live discovery DS for screens

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
## ClassMethod: Reify.getLoadedProjects

### Description
Return an Array of records describing every Reify [Project](Project.md#class-project) currently registered in the loaded-resource registry. Each record has fields `projectName`, `screenCount`, `dsCount`, `source`, `reifyURL`, `sourceLabel`, `loadedAt`, and `instance` (the live Project object).

### Returns

`[Array of Object](#type-array-of-object)` — loaded project records

---
## ClassMethod: Reify.setOverlayKey

### Description
Reassign the key combination that activates the [overlay view](#classmethod-reifyenableoverlay).

Pass a [KeyIdentifier](../reference.md#object-keyidentifier) object. When `keyName` is present the binding is a press-to-toggle shortcut; when absent only modifiers are checked and the overlay uses **hold-to-show** mode (appears while held, auto-dismisses on release).

A plain [KeyName](../reference_2.md#type-keyname) string (e.g. `"F2"`) is also accepted and treated as a toggle shortcut.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| key | [KeyName](../reference_2.md#type-keyname)|[KeyIdentifier](#type-keyidentifier) | false | — | new key binding |

---
## ClassMethod: Reify.addDataSourcesToProject

### Description
Register one or more DataSources in an existing Reify project's ``<datasources>`` section. The DataSource definitions must already be saved in `vbDataSources` storage; this method only updates the project's membership list so Reify-AI and the DataSources panel see them. Deduplicates by `dsName`.

Mirrors [Reify.addScreensToProject](#classmethod-reifyaddscreenstoproject) for screens.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| projectName | [String](#type-string) | false | — | project name |
| dsNames | [Array of String](#type-array-of-string) | false | — | DataSource IDs to register |
| callback | [Function](#type-function) | true | — | called with (DSResponse dsResponse, Object data) |

---
## ClassMethod: Reify.getProjectsDS

### Description
Return a [DataSource](DataSource_1.md#class-datasource) for browsing the list of projects in a Reify installation, suitable for binding to a [ListGrid](ListGrid_1.md#class-listgrid), [TreeGrid](TreeGrid.md#class-treegrid), [SelectItem](SelectItem.md#class-selectitem), etc.

By default, the local server's Reify storage is used. Pass a [ReifyDSSettings](../reference.md#object-reifydssettings) object with `reifyURL` set to access a remote Reify server (see [Reify.defaultReifyURL](#classattr-reifydefaultreifyurl)).

The DataSource is delivered asynchronously via callback because the underlying DataSource definition may need to be loaded from the server first. Subsequent calls for the same target return the same DataSource instance.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [Callback](../reference.md#type-callback) | false | — | called with `(DataSource ds)` — the DataSource is null on failure |
| settings | [ReifyDSSettings](#type-reifydssettings) | false | — | optional override settings |

---
## ClassMethod: Reify.getLoadedProjectsDS

### Description
Return a [DataSource](DataSource_1.md#class-datasource) bound to the live set of records returned by [Reify.getLoadedProjects](#classmethod-reifygetloadedprojects). The DS is `clientOnly` with `cacheAllData:true`, so bound [ListGrids](ListGrid_1.md#class-listgrid) update automatically as projects are loaded and destroyed, and the DS supports synchronous [fetchDataSynchronous()](#method-datasourcefetchdatasynchronous).

Returns the same DS instance on every call.

### Returns

`[DataSource](#type-datasource)` — live discovery DS for projects

---
## ClassMethod: Reify.getLoadedDataSourcesDS

### Description
Return a live clientOnly [DataSource](DataSource_1.md#class-datasource) of loaded DataSource records. See [Reify.getLoadedProjectsDS](#classmethod-reifygetloadedprojectsds).

### Returns

`[DataSource](#type-datasource)` — live discovery DS for DataSources

---
## ClassMethod: Reify.enableOverlay

### Description
Show the overlay view. Equivalent to `showOverlay()` with default dismiss settings (Escape key dismisses, click-outside dismisses). Idempotent.

---
## ClassMethod: Reify.saveProjectFile

### Description
Save a project definition to Reify's project storage (vbProjects). `projectXml` must be valid Reify project XML as produced by `ReifyProject.xmlSerialize()`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| projectName | [String](#type-string) | false | — | project name |
| projectXml | [String](#type-string) | false | — | project XML content |
| callback | [Function](#type-function) | true | — | called with (DSResponse dsResponse, Object data) |

---
## ClassMethod: Reify.getReifyScreens

### Description
Get a list of screens stored in Reify's screen storage.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [Function](#type-function) | false | — | called with (Array of String screenNames) |

---
## ClassMethod: Reify.registerLoadedProject

### Description
Add a [Project](Project.md#class-project) to the loaded-resource registry. Called automatically by [RPCManager.loadProject](RPCManager.md#classmethod-rpcmanagerloadproject) as projects come back from the server, and may also be called by application code for projects assembled outside the normal load path (e.g. from local storage).

Registration is idempotent: re-registering an already-known project just refreshes its record. An automatic destroy hook ensures the record is removed when the Project is destroyed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| project | [Project](#type-project) | false | — | the Project instance to register |
| sourceInfo | [Object](../reference.md#type-object) | true | — | optional override for source provenance fields (`source`, `reifyURL`, `sourceLabel`); defaults derived from [Reify.defaultReifyURL](#classattr-reifydefaultreifyurl) |

---
## ClassMethod: Reify.getLoadedDataSources

### Description
Return an Array of records describing every Reify-loaded [DataSource](DataSource_1.md#class-datasource) currently registered.

### Returns

`[Array of Object](#type-array-of-object)` — loaded DataSource records

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
