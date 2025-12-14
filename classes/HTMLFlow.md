# HTMLFlow Documentation

[← Back to API Index](../reference.md)

---

## Class: HTMLFlow

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
Use the HTMLFlow component to display HTML content that should expand to its natural size without scrolling.

HTML content can be specified directly via [HTMLFlow.contents](#attr-htmlflowcontents), or loaded from a URL via the property [HTMLFlow.contentsURL](#attr-htmlflowcontentsurl). This method of loading is for simple HTML content only; SmartClient components should be loaded via the [ViewLoader](ViewLoader.md#class-viewloader) class.

HTMLFlows are typically used to render snippets of HTML directly in the document rather than holding a complete HTML page, as the component can only size to fit HTML content it renders directly into the DOM. If you are looking to display a complete HTML page, you will need to modify the default [Overflow](../reference.md#type-overflow) and [defaultHeight](#defaultheight), or use the [HTMLPane](HTMLPane.md#class-htmlpane) class

NOTE: Since the size of an HTMLFlow component is determined by its HTML contents, this component will draw at varying sizes if given content of varying size. When using HTMLFlow components within a Layout, consider what will happen if the HTMLFlow renders at various sizes. An HTMLFlow which can expand should be placed in a container where other components can render smaller, where the container is allowed to scroll, or where there is padding to expand into.

HTMLFlow is a [DataBoundComponent](../reference.md#interface-databoundcomponent) but only supports one method at this time, [fetchRelatedData](#method-htmlflowfetchrelateddata).

### Groups

- contentLoading

---
## Attr: HTMLFlow.supportsContentsAsPage

### Description
Can this component have its [HTMLFlow.contents](#attr-htmlflowcontents) specified as a complete standalone HTML page to be rendered into an embedded IFRAME?

If true, if [ContentsType](../reference_2.md#type-contentstype) is specified as, or [derived to be](#attr-htmlflowautoderivecontentstype) "page", the contents will be rendered into an embedded IFRAME using the `srcdoc` attribute rather than written directly into the component handle.

If false, contentsType has no effect unless contents are being loaded from an explicitly specified [HTMLFlow.contentsURL](#attr-htmlflowcontentsurl)

**Flags**: IRW

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
## Attr: HTMLFlow.defaultWidth

### Description
For custom components, establishes a default width for the component.

For a component that should potentially be sized automatically by a Layout, set this property rather than [width](Canvas.md#attr-canvaswidth) directly, because Layouts regard a width setting as an explicit size that shouldn't be changed.

### Groups

- sizing

**Flags**: IRW

---
## Attr: HTMLFlow.structuralHTMLTags

### Description
List of tags used to determine whether the HTML contents of an HTMLFlow should be rendered with [contentsType:"page"](#attr-htmlflowautoderivecontentstype).

If an HTML string contains any of these tags not enclosed in either ``<pre>` ... `</pre>`` tags or comments (`<!-- ... -->`), [HTMLFlow.isPageHTML](#method-htmlflowispagehtml) will return true.

The default list of tags are as follows:

*   "!doctype"
*   "html"
*   "head"
*   "body"
*   "style"
*   "link"
*   "script"

**Flags**: IRWA

---
## Attr: HTMLFlow.dynamicContents

### Description
Dynamic string of HTML contents for this component. As with [HTMLFlow.contents](#attr-htmlflowcontents), this may be a fragment of HTML to display or a complete HTML page. See [HTMLFlow.contentsType](#attr-htmlflowcontentstype) and [HTMLFlow.supportsContentsAsPage](#attr-htmlflowsupportscontentsaspage).

See [Canvas.dynamicContents](Canvas.md#attr-canvasdynamiccontents) for details on how dynamicContents are resolved to a final string value.

**Flags**: IRWA

---
## Attr: HTMLFlow.autoDeriveContentsType

### Description
If [ContentsType](../reference_2.md#type-contentstype) is not explicitly specified, should it be automatically derived?

If set to true, this component will use [HTMLFlow.isPageHTML](#method-htmlflowispagehtml) to determine whether the contents are a standalone HTML page which should be rendered into an embedded IFRAME rather than written directly into the component's handle in the DOM.

Note that this property will auto derive the appropriate contents type for both explicitly specified [HTMLFlow.contents](#attr-htmlflowcontents) and for HTML loaded from the [HTMLFlow.contentsURL](#attr-htmlflowcontentsurl)

See [ContentsType](../reference_2.md#type-contentstype) for further information on displaying complete HTML pages in an IFRAME.

**Flags**: IRW

---
## Attr: HTMLFlow.contentsType

### Description
The `contentsType` attribute governs whether the contents of this htmlFlow are a fragment of HTML to inserted directly into the DOM, or a complete HTML page to be displayed in an IFRAME. If not explicitly specified, [HTMLFlow.autoDeriveContentsType](#attr-htmlflowautoderivecontentstype) may be set to automatically determine the appropriate contents type by analyzing the contents of the component. If `autoDeriveContentsType` is false and `contentsType` is not explicitly specified, contents will always be assumed to be `"fragment"`.

HTMLFlow contents may be [directly specified](#attr-htmlflowcontents) or loaded from a [specified URL](#attr-htmlflowcontentsurl). Note that if [HTMLFlow.supportsContentsAsPage](#attr-htmlflowsupportscontentsaspage) is false and no [HTMLFlow.contentsURL](#attr-htmlflowcontentsurl) is specified, the contents string will always be assumed to be a fragment, even if [ContentsType](../reference_2.md#type-contentstype) is explicitly set to `"page"`.

Note that an HTMLFlow with contentsType:"page" should not be used to load and display a page containing a set of SmartClient components into the application. To dynamically load SmartClient components, use [ViewLoader](ViewLoader.md#class-viewloader), **never** this mechanism (click [here](../kb_topics/noFrames.md#kb-topic-dont-misuse-frames) for why).

**Scripting, CSS and scoping considerations for HTMLFlow contents**  
The following considerations apply to HTMLFlow contents, whether directly specified or loaded from a contentsURL.

When contentsType is `"page"`, the HTML content will be rendered as a standalone document using an IFRAME. Use [HTMLFlow.iframeSandbox](#attr-htmlflowiframesandbox) to specify IFRAME restrictions using the native [sandbox attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe#sandbox). Note that any script (if allowed) will be executed in the scope of the embedded IFRAME window, not the main application window. Similarly, other features like css stylesheets loaded by the HTMLFlow will apply to the IFRAME window only, and the IFRAME will not pick up css style from the main application by default.

When contentsType is `"fragment"`, if script is encountered within the HTML fragment it will be evaluated in the scope of the main application if [HTMLFlow.evalScriptBlocks](#attr-htmlflowevalscriptblocks) is enabled. Developers should be aware that this evaluation occurs as part of the draw/redraw process, but unlike script embedded directly in a static HTML page, it is not processed by the browser while the elements are being written into the DOM and `document.write(...)` can not be used to modify the HTML as it is being rendered. In this mode, since the contents is written directly into the DOM, standard css styling for the page will be applied.

Note that if [HTMLFlow.autoDeriveContentsType](#attr-htmlflowautoderivecontentstype) is enabled, the default set of recognized [HTMLFlow.structuralHTMLTags](#attr-htmlflowstructuralhtmltags) include ``<script>``, so HTML contents including script will display as `contentsType:"page"`. The list of `structuralHTMLTags` can be modified to exclude script tags if desired.

### Groups

- contentLoading

**Flags**: IR

---
## Attr: HTMLFlow.canSelectText

### Description
Text selection for copy and paste is enabled by default in the HTMLFlow class. Note that this setting has no impact if [ContentsType](../reference_2.md#type-contentstype) is set to "page". In this case contents is loaded from a target URL via an IFRAME element, and text selection behavior will be dictated by the loaded HTML.

**Flags**: IR

---
## Attr: HTMLFlow.httpMethod

### Description
Selects the HTTP method that will be used when fetching content. Valid values are "POST" and "GET".

### Groups

- contentLoading

**Flags**: IRW

---
## Attr: HTMLFlow.defaultHeight

### Description
HTMLFlow defaultHeight is set to `1` which, together with [overflow:"visible"](../reference.md#type-overflow) causes the HTMLFlow to size to its content HTML.

Note that if [ContentsType](../reference_2.md#type-contentstype) is `"page"`, `overflow:"visible"` is not supported - for this usage an explicit larger height should be specified. You may want to use the preconfigured [HTMLPane](HTMLPane.md#class-htmlpane) class instead of HTMLFlow for this usage.

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
String of HTML contents for this component - may be a fragment of HTML to display or a complete HTML page. See [HTMLFlow.contentsType](#attr-htmlflowcontentstype) and [HTMLFlow.supportsContentsAsPage](#attr-htmlflowsupportscontentsaspage).

To load HTML contents from a URL, use [HTMLFlow.contentsURL](#attr-htmlflowcontentsurl) instead of this property. If `contentsURL` is non-null, `contents` will be ignored.

### See Also

- [HTMLFlow.contentsURL](#attr-htmlflowcontentsurl)
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
## Attr: HTMLFlow.overflow

### Description
HTMLFlows are `overflow:"visible"` by default, allowing them to fit their HTML content.

Note that if [ContentsType](../reference_2.md#type-contentstype) is `"page"`, `overflow:"visible"` is not supported and the overflow will default to `"auto"` instead

**Flags**: IRW

---
## Attr: HTMLFlow.loadingMessage

### Description
HTML to show while content is being fetched, active only if the `contentsURL` property has been set. Use `"${loadingImage}"` to include [a loading image](Canvas.md#classattr-canvasloadingimagesrc).

The loading message will show both during the initial load of content, and during reload if the contents are reloaded or the contentsURL changed. For a first-time only loading message, initialize the `contents` property instead.

Note: the `loadingMessage` is never displayed when [HTMLFlow.contentsType](#attr-htmlflowcontentstype) was explicitly specified as `"page"`.

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
If specified the HTMLFlow will load its contents from this URL instead of displaying [this.contents](#attr-htmlflowcontents). May be combined with parameters if [HTMLFlow.contentsURLParams](#attr-htmlflowcontentsurlparams) were specified.

The HTML retrieved from the target URL may be a complete standalone page to be rendered into its own scope using an IFRAME, or a fragment of HTML to display within this component's handle. See [ContentsType](../reference_2.md#type-contentstype) and [HTMLFlow.autoDeriveContentsType](#attr-htmlflowautoderivecontentstype) for more information.

Note that the link{loadingMessage} and [HTMLFlow.httpMethod](#attr-htmlflowhttpmethod) features only apply if contentsURL was set and contentsType was not explicitly set to `"page"`

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
## Method: HTMLFlow.isPageHTML

### Description
Determines whether the html string passed in is source for a standalone HTML page as opposed to an HTML fragment to be added to the DOM.

Returns true if any [HTMLFlow.structuralHTMLTags](#attr-htmlflowstructuralhtmltags) are found in the HTML string, outside of HTML comment or ``<pre>` ... `</pre>`` blocks.

This method is used by [HTMLFlow.autoDeriveContentsType](#attr-htmlflowautoderivecontentstype) to determine whether the widget contents should be rendered inside an embedded IFRAME.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| html | [String](#type-string) | false | — | HTML string to test |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the HTML string contains any structural HTML page elements.

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
