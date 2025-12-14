# HTMLFlow Documentation

[← Back to API Index](../reference.md)

---

## Class: HTMLFlow

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
Use the HTMLFlow component to display HTML content that should expand to its natural size without scrolling.

HTML content can be loaded and reloaded from a URL via the property `contentsURL`. This method of loading is for simple HTML content only; SmartClient components should be loaded via the [ViewLoader](ViewLoader.md#class-viewloader) class.

NOTE: Since the size of an HTMLFlow component is determined by its HTML contents, this component will draw at varying sizes if given content of varying size. When using HTMLFlow components within a Layout, consider what will happen if the HTMLFlow renders at various sizes. An HTMLFlow which can expand should be placed in a container where other components can render smaller, where the container is allowed to scroll, or where there is padding to expand into.

HTMLFlow is a [DataBoundComponent](../reference.md#interface-databoundcomponent) but only supports one method at this time, [fetchRelatedData](#method-htmlflowfetchrelateddata).

### Groups

- contentLoading

---
## Attr: HTMLFlow.contentsURLParams

### Description
Parameters to be sent to the contentsURL when fetching content.

### Groups

- contentLoading

**Flags**: IRW

---
## Attr: HTMLFlow.autoChangeProtocol

### Description
If this component is passed a URL with a protocol that differs from the current page, should it be automatically changed to match the page?

**Flags**: IRW

---
## Attr: HTMLFlow.captureSCComponents

### Description
If true, SmartClient components created while executing the loaded HTML are captured for rendering inside the HTMLFlow.

Only applies when contentsType is **not** "page".

### Groups

- contentLoading

**Flags**: IR

---
## Attr: HTMLFlow.dynamicContents

### Description
Dynamic contents allows the contents string to be treated as a simple but powerful template. When this attribute is set to true, JavaScript expressions may be embedded within the contents string, using the format: `${_[JavaScript to evaluate]_}`.

For example, to include the current date in a templated message, `canvas.contents` could be set to:  
`"Today's date is `<b>`${new Date().toUSShortDate()}`</b>`"`

Embedded expressions will be evaluated when the canvas is drawn or redrawn, and the result of the evaluated expression will be displayed to the user. If the expression does not evaluate to a String, the `toString()` representation of the returned object will be displayed automatically

Dynamic expressions are evaluated in the scope of the canvas displaying the content, so the `this` keyword may be used within your expression to refer to the canvas. Developers may also explicitly supply values for variables to be used within the evaluation via the [Canvas.dynamicContentsVars](Canvas.md#attr-canvasdynamiccontentsvars) property.

Notes:

*   Calling markForRedraw() on the canvas will evaluate any embedded expressions.
*   Multiple such expressions may be embedded within the contents string for a component.
*   If an error occurs during evaluation, a warning is logged to the [Developer Console](../kb_topics/debugging.md#kb-topic-debugging) and the error string will be embedded in place of the expected value in the Canvas.

### Groups

- contents
- dynamicStrings

### See Also

- [HTMLFlow.contents](#attr-htmlflowcontents)
- [Canvas.dynamicContentsVars](Canvas.md#attr-canvasdynamiccontentsvars)

**Flags**: IRWA

---
## Attr: HTMLFlow.contentsType

### Description
The default setting of `null` or 'fragment' indicates that HTML loaded from [HTMLFlow.contentsURL](#attr-htmlflowcontentsurl) is assumed to be an HTML fragment rather than a complete page. Set to "page" to load HTML as a standalone page, via an IFRAME.

`contentsType:"page"` should only be used for controlled HTML content, and only when such content cannot be delivered as an HTML fragment instead (the default). To dynamically load SmartClient components, use [ViewLoader](ViewLoader.md#class-viewloader), **never** this mechanism (click [here](../kb_topics/noFrames.md#kb-topic-dont-misuse-frames) for why).

Loading HTML content as a fragment is less resource intensive and avoids visual artifacts such as translucent media becoming opaque or disappearing when placed over an IFRAME.

Loading third-party, uncontrolled content could lead to the surrounding page disappearing if a user clicks on an HTML link with `target=_top`.

With `contentsType:"page"`, [HTMLFlow.loadingMessage](#attr-htmlflowloadingmessage) is not supported, and only "GET" is supported for [httpMethod](#attr-htmlflowhttpmethod).

Note that a native bug has been observed in Internet Explorer version 10 whereby if an HTMLFlow with `contentsType` set to `"page"` loads a page containing an HTML ``<frameset>``, when the HTMLFlow is [hidden](Canvas.md#method-canvashide), it can interfere with the rendering of other elements on the page. Setting [Canvas.shrinkElementOnHide](Canvas.md#attr-canvasshrinkelementonhide) to `true` will work around this behavior.

### Groups

- contentLoading

**Flags**: IR

---
## Attr: HTMLFlow.canSelectText

### Description
Text selection for copy and paste is enabled by default in the HTMLFlow class. Note that this setting has no impact if [ContentsType](../reference.md#type-contentstype) is set to "page". In this case contents is loaded from a target URL via an IFRAME element, and text selection behavior will be dictated by the loaded HTML.

**Flags**: IR

---
## Attr: HTMLFlow.httpMethod

### Description
Selects the HTTP method that will be used when fetching content. Valid values are "POST" and "GET".

### Groups

- contentLoading

**Flags**: IRW

---
## Attr: HTMLFlow.selectContentOnSelectAll

### Description
When this `HTMLFlow` is focused, causes Ctrl-A / Command-A keypresses to select just the content, as opposed to all content on the screen becoming selected. This `HTMLFlow` must be [focusable](Canvas.md#attr-canvascanfocus) in order for this setting to have an effect.

Not valid with [contentsType](#attr-htmlflowcontentstype) "page".

**Flags**: IRW

---
## Attr: HTMLFlow.contents

### Description
The contents of a canvas or label widget. Any HTML string is acceptable.

### Groups

- contents

### See Also

- [HTMLFlow.dynamicContents](#attr-htmlflowdynamiccontents)

**Flags**: IRW

---
## Attr: HTMLFlow.iframeSandbox

### Description
When using [contentsType](#attr-htmlflowcontentstype) "page", sets the `<iframe>` `sandbox` attribute to the provided value.

Use the value "\*ALL\*" to cause the "sandbox" attribute to be output with no value (which causes full sandboxing).

See any HTML reference for other legal values of the "sandbox" attribute, which allow you to remove individual restrictions on the loaded content.

Note that SmartClient simply applies the provided value to the generated `<iframe>` element and cannot fix bugs or differences in sandbox behavior across different browsers.

**Flags**: IR

---
## Attr: HTMLFlow.loadingMessage

### Description
HTML to show while content is being fetched, active only if the `contentsURL` property has been set. Use `"${loadingImage}"` to include [a loading image](Canvas.md#classattr-canvasloadingimagesrc).

The loading message will show both during the initial load of content, and during reload if the contents are reloaded or the contentsURL changed. For a first-time only loading message, initialize the `contents` property instead.  
Note: the `loadingMessage` is never displayed when loading complete web pages rather than HTML fragments (see [HTMLFlow.contentsType](#attr-htmlflowcontentstype)).

### Groups

- contentLoading

**Flags**: IRW

---
## Attr: HTMLFlow.evalScriptBlocks

### Description
If `evalScriptBlocks` is true, HTMLFlow will pre-process the loaded HTML in order to mimic how the HTML would execute if it were loaded as an independent page or loaded via an IFRAME.

This feature is intended to assist with migrating existing applications to SmartClient.

`evalScriptBlocks` is enabled by default when loading remote content (via [HTMLFlow.contentsURL](#attr-htmlflowcontentsurl)) and disabled by default for content supplied via [HTMLFlow.setContents](#method-htmlflowsetcontents).

Note that, if evalScriptBlocks is false, `<SCRIPT>` blocks will still be detected and disabled to avoid the inconsistent results across different browsers.

Only applies when contentsType is **not** "page".

### Groups

- contentLoading

**Flags**: IR

---
## Attr: HTMLFlow.allowCaching

### Description
By default an HTMLFlow will explicitly prevent browser caching.

Set to true to allow browser caching **if the browser would normally do so**, in other words, if the HTTP headers returned with the response indicate that the response can be cached.

**Flags**: IR

---
## Attr: HTMLFlow.contentsURL

### Description
URL to load content from.

If specified, this component will load HTML content from the specified URL when it is first drawn.

This feature relies on the XMLHttpRequest object which can be disabled by end-users in some supported browsers. See [platformDependencies](../kb_topics/platformDependencies.md#kb-topic-platform-dependencies) for more information.

### Groups

- contentLoading

**Flags**: IRW

---
## Method: HTMLFlow.fetchRelatedData

### Description
Based on the relationship between the DataSource this component is bound to and the DataSource specified as the "schema" argument, call fetchData() to retrieve records in this data set that are related to the passed-in record.

Relationships between DataSources are declared via [DataSourceField.foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey).

For example, given two related DataSources "orders" and "orderItems", where we want to fetch the "orderItems" that belong to a given "order". "orderItems" should declare a field that is a [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) to the "orders" table (for example, it might be named "orderId" with foreignKey="orders.id"). Then, to load the records related to a given "order", call fetchRelatedData() on the component bound to "orderItems", pass the "orders" DataSource as the "schema" and pass a record from the "orders" DataSource as the "record" argument.

**Note:** When you expect a large number of records to be returned it is not recommended to display these in the DetailViewer as it doesn't have the same level of support for large datasets as the [ListGrid](ListGrid_1.md#class-listgrid).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | DataSource record |
| schema | [Canvas](#type-canvas)|[DataSource](#type-datasource)|[ID](#type-id) | false | — | schema of the DataSource record, or DataBoundComponent already bound to that schema |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

---
## Method: HTMLFlow.loadingContent

### Description
Returns true if this htmlFlow is currently loading content from the server.  
Note: Does not apply to htmlFlows with [contentsType](#attr-htmlflowcontentstype) set to `"page"`

### Returns

`[Boolean](#type-boolean)` — whether content is currently being loaded

### Groups

- contentLoading

### See Also

- [HTMLFlow.contentLoaded](#method-htmlflowcontentloaded)

**Flags**: A

---
## Method: HTMLFlow.setContentsURL

### Description
Change the URL this component loads content from. Triggers a fetch for content from the new URL.

Can also be called with no arguments to reload content from the existing [HTMLFlow.contentsURL](#attr-htmlflowcontentsurl).

This feature relies on the XMLHttpRequest object which can be disabled by end-users in some supported browsers. See [platformDependencies](../kb_topics/platformDependencies.md#kb-topic-platform-dependencies) for more information.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| url | [URL](../reference_2.md#type-url) | true | — | URL to retrieve contents from |
| params | [Object](../reference.md#type-object) | true | — | Parameters to send to the contentsURL. Merged with `component.contentsURLParams` if both are set. |

### Groups

- contentLoading

### See Also

- [HTMLFlow.evalScriptBlocks](#attr-htmlflowevalscriptblocks)

---
## Method: HTMLFlow.contentLoaded

### Description
StringMethod fired when content is completely loaded in this htmlFlow. Has no default implementation. May be observed or overridden as a notification type method to fire custom logic when loading completes.

Notes:

*   A call to [this.setContents()](Canvas.md#method-canvassetcontents) will cause this notification to be fired when the contents have been set. If [HTMLFlow.evalScriptBlocks](#attr-htmlflowevalscriptblocks) is true, and the HTML passed into `setContents()` contains any ``<script src=... >`` tags, this callback will be fired asynchronously once the scripts have been loaded from the server and executed, as well as having the widget content updated
*   When using [HTMLFlow.contentsURL](#attr-htmlflowcontentsurl), this does not apply to htmlFlows with [contentsType](#attr-htmlflowcontentstype) set to `"page"`

### Groups

- contentLoading

---
## Method: HTMLFlow.setContents

### Description
Changes the contents of a widget to newContents, an HTML string.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newContents | [HTMLString](../reference.md#type-htmlstring) | true | — | an HTML string to be set as the contents of this widget |

### See Also

- [HTMLFlow.evalScriptBlocks](#attr-htmlflowevalscriptblocks)

---
## Method: HTMLFlow.transformHTML

### Description
Override to modify the loaded HTML before it is rendered.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| html | [HTMLString](../reference.md#type-htmlstring) | false | — | the html as loaded from the server return (HTML) html to be rendered |

### Groups

- contentLoading

---
## Method: HTMLFlow.handleError

### Description
This method is called when a transport error occurs. Typically, this is the result of the server returning an HTTP error code such as 404 - document not found. You can inspect the RPCResponse object for the reasons for the error and take appropriate action. Typical properties to look at are rpcResponse.status, and rpcResponse.httpResponseCode.

This method is called from the response processing pipeline. If you want to provide your own HTML response that should be rendered into this component as the result of the error, you can do so by setting rpcResponse.data to your HTML string. Returning false from this method suppresses any further response handling. The default implementation of this method causes an error message to be logged to the Developer Console and sets the HTML to the error string.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rpcRequest | [RPCRequest](#type-rpcrequest) | false | — | The RPCRequest that was made to the server |
| rpcResponse | [RPCResponse](#type-rpcresponse) | false | — | The RPCResponse that was received |

### Returns

`[boolean](../reference.md#type-boolean)` — false to suppress further response processing

### Groups

- contentLoading

---
