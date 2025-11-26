# ScreenLoader Documentation

[← Back to API Index](../reference.md)

---

## Class: ScreenLoader

*Inherits from:* [VLayout](../reference.md#class-vlayout)

### Description
The ScreenLoader component can be used to load [ComponentXML Screens](../kb_topics/componentXML.md#kb-topic-component-xml) into a running application.

A ScreenLoader is a VLayout, and can be provided anywhere a Canvas can be used: as a Tab pane, and Layout member, etc. When a ScreenLoader draws, it shows a [loading message](#attr-screenloaderloadingmessage) if [enabled](#attr-screenloadershowloadingmessage), performs an RPC to the [screenLoaderURL](RPCManager.md#classattr-rpcmanagerscreenloaderurl) to load the screen, if necessary, and finally embeds the [screen](#attr-screenloaderscreenname) within the layout.

The last top-level UI component (Canvas subclass) defined by the screen is set as the layout contents. Top-level in this case means that the UI component is not contained in another UI component as a member or child.

The ScreenLoader relies on the XMLHttpRequest object which can be disabled by end-users in some supported browsers. See [platformDependencies](../kb_topics/platformDependencies.md#kb-topic-platform-dependencies) for more information.

---
## Attr: ScreenLoader.dataContextBinding

### Description
A [DataContextBinding](../reference.md#object-datacontextbinding) to be applied to the loaded screen via [Canvas.setDataContext](Canvas.md#method-canvassetdatacontext).

### Groups

- dataContext

**Flags**: IWR

---
## Attr: ScreenLoader.loadingMessage

### Description
Message to show while the screen is loading if [enabled](#attr-screenloadershowloadingmessage). Use `"${loadingImage}"` to include [a loading image](Canvas.md#classattr-canvasloadingimagesrc).

**Flags**: IR

---
## Attr: ScreenLoader.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: ScreenLoader.showLoadingMessage

### Description
Should a [loading message](#attr-screenloaderloadingmessage) be displayed while screen is loading?

**Flags**: IR

---
## Attr: ScreenLoader.screenLoaderURL

### Description
Specifies the URL where ScreenLoaderServlet is installed. If not set, [RPCManager.screenLoaderURL](RPCManager.md#classattr-rpcmanagerscreenloaderurl) is used.

**Flags**: IR

---
## Attr: ScreenLoader.screenName

### Description
Name of screen to be loaded.

**Flags**: IR

---
## Method: ScreenLoader.setDataContextBinding

### Description
Set the dataContextBinding property.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| binding | [DataContext](#type-datacontext) | false | — | the new DataContext binding |

### Groups

- dataContext

---
## Method: ScreenLoader.dataContextChanged

### Description
Notification method fired when [DataContext](../reference.md#object-datacontext) is bound on the embedded screen. This can occur on the initial draw or by an explicit call to [setDataContext()](Canvas.md#method-canvassetdatacontext) either via this ScreenLoader or from other components including the screen itself.

### Groups

- dataContext

---
