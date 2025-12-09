# HTMLPane Documentation

[← Back to API Index](../reference.md)

---

## Class: HTMLPane

*Inherits from:* [HTMLFlow](HTMLFlow.md#class-htmlflow)

### Description
Subclass of [HTMLFlow](HTMLFlow.md#class-htmlflow) configured to display HTML content in a pane of specified size. If the HTML content is larger than the size of the pane, the pane will provide scrollbars for viewing clipped content.

HTML content can be specified directly via [HTMLPane.contents](#attr-htmlpanecontents), or loaded from a URL via the property [HTMLPane.contentsURL](#attr-htmlpanecontentsurl). This method of loading is for simple HTML content only; SmartClient components should be loaded via the [ViewLoader](ViewLoader.md#class-viewloader) class.

HTMLPanes have the ability to render snippets of HTML directly in the document, or use an IFRAME to render a complete HTML page. See [HTMLPane.contentsType](#attr-htmlpanecontentstype) for more information

You can set the size of an HTMLPane directly via the width and height properties, or indirectly by placing the HTMLPane in a container component ([Layout](Layout.md#class-layout), [Window](Window.md#class-window), [SectionStack](SectionStack.md#class-sectionstack), etc) that manages the sizes of its members.

---
## Attr: HTMLPane.contentsURL

### Description
If specified the HTMLFlow will load its contents from this URL instead of displaying [this.contents](#attr-htmlpanecontents). May be combined with parameters if [HTMLPane.contentsURLParams](#attr-htmlpanecontentsurlparams) were specified.

The HTML retrieved from the target URL may be a complete standalone page to be rendered into its own scope using an IFRAME, or a fragment of HTML to display within this component's handle. See [ContentsType](../reference_2.md#type-contentstype) and [HTMLPane.autoDeriveContentsType](#attr-htmlpaneautoderivecontentstype) for more information.

Note that the link{loadingMessage} and [httpMethod](HTMLFlow.md#attr-htmlflowhttpmethod) features only apply if contentsURL was set and contentsType was not explicitly set to `"page"`

### Groups

- contentLoading

**Flags**: IRW

---
## Attr: HTMLPane.contentsType

### Description
The `contentsType` attribute governs whether the contents of this htmlFlow are a fragment of HTML to inserted directly into the DOM, or a complete HTML page to be displayed in an IFRAME. If not explicitly specified, [HTMLPane.autoDeriveContentsType](#attr-htmlpaneautoderivecontentstype) may be set to automatically determine the appropriate contents type by analyzing the contents of the component. If `autoDeriveContentsType` is false and `contentsType` is not explicitly specified, contents will always be assumed to be `"fragment"`.

HTMLFlow contents may be [directly specified](#attr-htmlpanecontents) or loaded from a [specified URL](#attr-htmlpanecontentsurl). Note that if [HTMLPane.supportsContentsAsPage](#attr-htmlpanesupportscontentsaspage) is false and no [HTMLPane.contentsURL](#attr-htmlpanecontentsurl) is specified, the contents string will always be assumed to be a fragment, even if [ContentsType](../reference_2.md#type-contentstype) is explicitly set to `"page"`.

Note that an HTMLFlow with contentsType:"page" should not be used to load and display a page containing a set of SmartClient components into the application. To dynamically load SmartClient components, use [ViewLoader](ViewLoader.md#class-viewloader), **never** this mechanism (click [here](../kb_topics/noFrames.md#kb-topic-dont-misuse-frames) for why).

**Scripting, CSS and scoping considerations for HTMLFlow contents**  
The following considerations apply to HTMLFlow contents, whether directly specified or loaded from a contentsURL.

When contentsType is `"page"`, the HTML content will be rendered as a standalone document using an IFRAME. Use [iframeSandbox](HTMLFlow.md#attr-htmlflowiframesandbox) to specify IFRAME restrictions using the native [sandbox attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe#sandbox). Note that any script (if allowed) will be executed in the scope of the embedded IFRAME window, not the main application window. Similarly, other features like css stylesheets loaded by the HTMLFlow will apply to the IFRAME window only, and the IFRAME will not pick up css style from the main application by default.

When contentsType is `"fragment"`, if script is encountered within the HTML fragment it will be evaluated in the scope of the main application if [evalScriptBlocks](HTMLFlow.md#attr-htmlflowevalscriptblocks) is enabled. Developers should be aware that this evaluation occurs as part of the draw/redraw process, but unlike script embedded directly in a static HTML page, it is not processed by the browser while the elements are being written into the DOM and `document.write(...)` can not be used to modify the HTML as it is being rendered. In this mode, since the contents is written directly into the DOM, standard css styling for the page will be applied.

Note that if [HTMLPane.autoDeriveContentsType](#attr-htmlpaneautoderivecontentstype) is enabled, the default set of recognized [structuralHTMLTags](HTMLFlow.md#attr-htmlflowstructuralhtmltags) include ``<script>``, so HTML contents including script will display as `contentsType:"page"`. The list of `structuralHTMLTags` can be modified to exclude script tags if desired.

### Groups

- contentLoading

**Flags**: IRW

---
## Attr: HTMLPane.autoDeriveContentsType

### Description
If [ContentsType](../reference_2.md#type-contentstype) is not explicitly specified, should it be automatically derived?

If set to true, this component will use [isPageHTML()](HTMLFlow.md#method-htmlflowispagehtml) to determine whether the contents are a standalone HTML page which should be rendered into an embedded IFRAME rather than written directly into the component's handle in the DOM.

Note that this property will auto derive the appropriate contents type for both explicitly specified [HTMLPane.contents](#attr-htmlpanecontents) and for HTML loaded from the [HTMLPane.contentsURL](#attr-htmlpanecontentsurl)

See [ContentsType](../reference_2.md#type-contentstype) for further information on displaying complete HTML pages in an IFRAME.

**Flags**: IRW

---
## Attr: HTMLPane.contentsURLParams

### Description
Parameters to be sent to the contentsURL when fetching content.

### Groups

- contentLoading

**Flags**: IRW

---
## Attr: HTMLPane.contents

### Description
String of HTML contents for this component - may be a fragment of HTML to display or a complete HTML page. See [HTMLFlow.contentsType](HTMLFlow.md#attr-htmlflowcontentstype) and [HTMLFlow.supportsContentsAsPage](HTMLFlow.md#attr-htmlflowsupportscontentsaspage).

To load HTML contents from a URL, use [HTMLFlow.contentsURL](HTMLFlow.md#attr-htmlflowcontentsurl) instead of this property. If `contentsURL` is non-null, `contents` will be ignored.

### See Also

- [HTMLFlow.contentsURL](HTMLFlow.md#attr-htmlflowcontentsurl)
- [HTMLFlow.dynamicContents](HTMLFlow.md#attr-htmlflowdynamiccontents)

**Flags**: IRW

---
## Attr: HTMLPane.supportsContentsAsPage

### Description
Can this component have its [HTMLPane.contents](#attr-htmlpanecontents) specified as a complete standalone HTML page to be rendered into an embedded IFRAME?

If true, if [ContentsType](../reference_2.md#type-contentstype) is specified as, or [derived to be](#attr-htmlpaneautoderivecontentstype) "page", the contents will be rendered into an embedded IFRAME using the `srcdoc` attribute rather than written directly into the component handle.

If false, contentsType has no effect unless contents are being loaded from an explicitly specified [HTMLPane.contentsURL](#attr-htmlpanecontentsurl)

**Flags**: IRW

---
## Attr: HTMLPane.defaultHeight

### Description
Default height for the component.

For a component that should potentially be sized automatically by a Layout, set this property rather than [height](Canvas.md#attr-canvasheight) directly, because Layouts regard a height setting as an explicit size that shouldn't be changed.

### Groups

- sizing

**Flags**: IRWA

---
## Attr: HTMLPane.overflow

### Description
HTMLPanes are `overflow:"auto"` by default.

Note that for [contentsType:"page"](../reference_2.md#type-contentstype), `overflow:"visible"` is not supported.

**Flags**: IRW

---
