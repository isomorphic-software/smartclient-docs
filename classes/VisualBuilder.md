# VisualBuilder Documentation

[← Back to API Index](../reference.md)

---

## Class: VisualBuilder

### Description
An application that allows developers to create and manage SmartClient screens and datasources. This is an **internal only** class - do not try to use it directly in your applications. If you want to create visual tools similar to VisualBuilder, see [the Dashboards & Tools framework overview](../kb_topics/devTools.md#kb-topic-dashboards--tools-framework-overview)

### Groups

- visualBuilder

---
## Attr: VisualBuilder.defaultApplicationMode

### Description
The default application mode. Note, this can be changed through the UI - see [showModeSwitcher](#attr-visualbuildershowmodeswitcher)

**Flags**: IR

---
## Attr: VisualBuilder.saveFileBuiltinIsEnabled

### Description
If set to true the built-in save file mechanism is enabled, allowing you to save files to offline storage or the server filesystem (if enabled)

### See Also

- [VisualBuilder.filesystemDataSourceEnabled](#attr-visualbuilderfilesystemdatasourceenabled)

**Flags**: IR

---
## Attr: VisualBuilder.customComponentsURL

### Description
Relative URL to Visual Builder's customComponents.xml configuration file. The default value makes the framework look wherever Visual Builder itself was loaded from

**Flags**: IR

---
## Attr: VisualBuilder.skin

### Description
The name of a skin to use. Note that Visual Builder may use two skins - the skin specified here, for the elements of the application you are building, and a high-contrast, white-on-black "ToolSkin" for the elements of Visual Builder itself. When in "Toolskin" mode (which is switchable at runtime through the UI), the `skin` property only affects the skin used by the visual elements of the application you are building.

**Flags**: IR

---
## Attr: VisualBuilder.initialComponent

### Description
A PaletteNode describing a component to add to an empty screen as an initial container.

**Flags**: IR

---
## Attr: VisualBuilder.globalDependenciesURL

### Description
Relative URL to Visual Builder's globalDependencies.xml configuration file. The default value makes the framework look wherever Visual Builder itself was loaded from

**Flags**: IR

---
## Attr: VisualBuilder.defaultMockupComponentsURL

### Description
Relative URL to Visual Builder's defaultMockupComponents.xml configuration file. The default value makes the framework look wherever Visual Builder itself was loaded from

**Flags**: IR

---
## Attr: VisualBuilder.showModeSwitcher

### Description
If this property is not explicitly set to false, Visual Builder shows a UI to allow the [application mode](../reference.md#type-applicationmode) to be toggled at runtime.

**Flags**: IR

---
## Attr: VisualBuilder.openFullBuilderSeparately

### Description
Whether to use the existing browser window or a new one when opening a Mockup Mode screen converted to standard Component XML via "Go to Visual Builder".

**Flags**: IR

---
## Attr: VisualBuilder.mockupMode

### Description
If true, starts Visual Builder in mockup mode

**Flags**: IR

---
## Attr: VisualBuilder.loadFileBuiltinIsEnabled

### Description
If set to true the built-in load file mechanism is enabled, allowing you to load files from offline storage or the server filesystem (if enabled)

### See Also

- [VisualBuilder.filesystemDataSourceEnabled](#attr-visualbuilderfilesystemdatasourceenabled)

**Flags**: IR

---
## Attr: VisualBuilder.filesystemDataSourceEnabled

### Description
If set to true, allows the built-in save file and load file operations to access the server filesystem. Note, this also requires appropriate server-side permission - your `server.properties` file must specify `FilesystemDataSource.enabled: true`.

If this property is false, saving and loading (if enabled) will be to and from local [offline storage](Offline.md#class-offline).

### See Also

- [VisualBuilder.saveFileBuiltinIsEnabled](#attr-visualbuildersavefilebuiltinisenabled)
- [VisualBuilder.loadFileBuiltinIsEnabled](#attr-visualbuilderloadfilebuiltinisenabled)

**Flags**: IR

---
## Attr: VisualBuilder.defaultComponentsURL

### Description
Relative URL to Visual Builder's defaultComponents.xml configuration file. The default value makes the framework look wherever Visual Builder itself was loaded from

**Flags**: IR

---
