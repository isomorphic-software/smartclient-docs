# ViewLoader Documentation

[← Back to API Index](../reference.md)

---

## Class: ViewLoader

*Inherits from:* [Label](Label.md#class-label)

### Description
The ViewLoader component can be used to load new SmartClient-based user interfaces into a running application.

**NOTE:** before using a ViewLoader, be sure that you have read about and understood the [SmartClient Architecture](../kb_topics/smartArchitecture.md#kb-topic-smartclient-architecture). The most responsive and scalable application architecture preloads views rather than using ViewLoaders.

A ViewLoader is a Canvas, and can be provided anywhere a Canvas can be provided: as a Tab pane, and Layout member, etc. When a ViewLoader draws, it shows a [loading message](#attr-viewloaderloadingmessage), then performs an RPC to the [viewURL](#attr-viewloaderviewurl) to load components.

The response from the viewURL should be SmartClient components defined in JavaScript, with no surrounding `<SCRIPT>` tags or other HTML framing. The returned script can be dynamically generated, for example, it may be the result of a JSP containing an XML view description enclosed in [`<isomorphicXML>`](../kb_topics/xmlTag.md#kb-topic-isomorphicxml) tags.

In the returned script, the special variable "viewLoader" is available to refer to the ViewLoader instance that is loading components. The intended usage is that the returned script creates a view consisting of SmartClient components, then calls `viewLoader.setView(myView)` to place the loaded view into the ViewLoader. If the view does not call setView() explicitly, the viewLoader will find the last top-level UI component (Canvas subclass) created by the view and set that as the current view. Top-level in this case means that the UI component is not contained in another UI component as a member or child.

The ViewLoader relies on the XMLHttpRequest object which can be disabled by end-users in some supported browsers. See [platformDependencies](../kb_topics/platformDependencies.md#kb-topic-platform-dependencies) for more information.

### Groups

- viewLoading

### See Also

- [RPCRequest.evalResult](RPCRequest.md#attr-rpcrequestevalresult)
- [smartArchitecture](../kb_topics/smartArchitecture.md#kb-topic-smartclient-architecture)

---
## Attr: ViewLoader.httpMethod

### Description
Selects the HTTP method that will be used when fetching content. Valid values are "POST" and "GET".

### Groups

- contentLoading

**Flags**: IRW

---
## Attr: ViewLoader.viewRPCProperties

### Description
RPCRequest properties to be sent with every RPCRequest issued by the ViewLoader. Very advanced; could be used to, for example, set HTTP headers.

**Flags**: IRA

---
## Attr: ViewLoader.allowCaching

### Description
By default a ViewLoader will explicitly prevent browser caching.

Set to true to allow browser caching **if the browser would normally do so**, in other words, if the HTTP headers returned with the response indicate that the response can be cached.

**Flags**: IR

---
## Attr: ViewLoader.viewURLParams

### Description
Parameters to be sent to the viewURL when fetching the view.

**Flags**: IR

---
## Attr: ViewLoader.viewURL

### Description
URL to load components from.

**Flags**: IR

---
## Attr: ViewLoader.loadingMessage

### Description
Message to show while the view is loading. Use `"${loadingImage}"` to include [a loading image](Canvas.md#classattr-canvasloadingimagesrc).

### Groups

- viewLoading

**Flags**: IR

---
## Method: ViewLoader.getView

### Description
Retrieve the current view. May be null if the view has not yet been loaded, or has been explicitly set to null.

### Returns

`[Canvas](#type-canvas)` — the current view

### Groups

- contentLoading

---
## Method: ViewLoader.handleError

### Description
This method is called when a transport error occurs. Typically, this is the result of the server returning an HTTP error code such as 404 - document not found. You can inspect the RPCResponse object for the reasons for the error and take appropriate action. Typical properties to look at are rpcResponse.status, and rpcResponse.httpResponseCode.

This method is called from the response processing pipeline. If you want to provide your own HTML response as the result of the error, you can do so by setting rpcResponse.data to your HTML string. Returning false from this method suppresses any further response handling. The default implementation of this method causes an error message to be logged to the Developer Console and sets the HTML to the error string.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rpcRequest | [RPCRequest](#type-rpcrequest) | false | — | The RPCRequest that was made to the server |
| rpcResponse | [RPCResponse](#type-rpcresponse) | false | — | The RPCResponse that was received |

### Returns

`[Boolean](#type-boolean)` — false to suppress further response processing

### Groups

- contentLoading

---
## Method: ViewLoader.setViewURL

### Description
Change the URL this component loads a view from. Triggers a fetch from the new URL.

Can also be called with no arguments to reload the view from the existing [ViewLoader.viewURL](#attr-viewloaderviewurl).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| url | [URL](../reference_2.md#type-url) | true | — | URL to retrieve view from |
| params | [Object](../reference.md#type-object) | true | — | Parameters to send to the viewURL. Merged with `component.viewURLParams` if both are set. |
| rpcProperties | [RPCRequest Properties](#type-rpcrequest-properties) | true | — | Additional properties for the RPCRequest sent by the ViewLoader. Very advanced; could be used to, for example, set HTTP headers. |

### Groups

- viewLoading

---
## Method: ViewLoader.viewLoaded

### Description
StringMethod fired when the view has been loaded. Has no default implementation. May be observed or overridden to fire custom logic when loading completes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| view | [Canvas](#type-canvas) | false | — | the view that was loaded |

### Groups

- contentLoading

---
