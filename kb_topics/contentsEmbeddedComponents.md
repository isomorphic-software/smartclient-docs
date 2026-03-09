# Embedded Components in Contents

[← Back to API Index](../reference.md)

---

## KB Topic: Embedded Components in Contents

### Description
SmartClient's [Layout](../classes/Layout.md#class-layout) and its subclasses provide a powerful layout engine, but some designs are more naturally expressed with CSS — for example, CSS flexbox with `gap` and `flex-wrap`, CSS grid with named `grid-template-areas`, or a page where SmartClient widgets are interspersed with static HTML such as headings, paragraphs, and images.

**Embedded components in contents** bridge this gap: you provide an HTML template as [Canvas.contents](../classes/Canvas.md#attr-canvascontents) (a plain string, as it has always been), and mark slots for SmartClient widgets using the `scID` attribute on placeholder elements. The CSS in the template controls all layout and sizing; the framework takes care of connecting widgets to the placeholders at draw time.

#### Basic Usage

Place one or more elements with an `scID` attribute in the [Canvas.contents](../classes/Canvas.md#attr-canvascontents) string. Each `scID` value identifies a child component by _name_ — either a child already present in the [Canvas.children](../classes/Canvas.md#attr-canvaschildren) array (matched by [Canvas.name](../classes/Canvas.md#attr-canvasname)), or an [AutoChild](autoChildren.md#kb-topic-autochildren) that will be created automatically if the corresponding `*Defaults` / `*Constructor` properties exist on the Canvas.

After the contents HTML is inserted into the DOM at draw time, the framework scans for `scID` placeholders, resolves each one to a child or AutoChild, and connects the widget to the placeholder element via [Canvas.htmlElement](../classes/Canvas.md#attr-canvashtmlelement) and [Canvas.matchElement](../classes/Canvas.md#attr-canvasmatchelement). The widget renders inside the placeholder and sizes itself to match it, so the HTML's CSS rules control all layout and sizing.

#### Example: Mixing HTML and SmartClient Widgets

The most common use case is a page section that mixes static HTML content (headings, text, images) with SmartClient widgets:

```
 isc.Canvas.create({
     width: "100%", height: "100%",
     overflow: "auto",
     contents:
         '<h2>Employee Directory</h2>' +
         '<p>Select a row to see details.</p>' +
         '<div scID="mainGrid"' +
         '     style="height:400px"></div>' +
         '<footer style="margin-top:10px;' +
         '     color:#888">&copy; 2026 Acme</footer>',
     mainGridDefaults: {
         _constructor: "ListGrid",
         autoFetchData: true,
         dataSource: "employees"
     }
 });
 
```
The ``<h2>``, ``<p>``, and ``<footer>`` are ordinary HTML rendered by the browser. The `mainGrid` AutoChild fills the 400px-tall placeholder. Because the child is `position:relative` inside the content flow, the entire Canvas scrolls naturally when [overflow](../classes/Canvas.md#attr-canvasoverflow) is `"auto"`.

As with all AutoChildren, the created component is accessible as an instance property on the parent — in this case, `this.mainGrid`. See [AutoChildren](autoChildren.md#kb-topic-autochildren) for details.

#### Example: CSS Flexbox

```
 isc.Canvas.create({
     width: "100%", height: "100%",
     contents:
         '<div style="display:flex; gap:10px;' +
         '     height:100%">' +
             '<div scID="mainGrid"' +
             '     style="flex:1"></div>' +
             '<div scID="detail"' +
             '     style="width:300px"></div>' +
         '</div>',
     mainGridDefaults: {
         _constructor: "ListGrid",
         autoFetchData: true,
         dataSource: "employees"
     },
     detailDefaults: {
         _constructor: "DetailViewer",
         dataSource: "employees"
     }
 });
 
```
The CSS `flex` rules control the split between the grid and the detail viewer.

#### Example: CSS Grid with Named Areas

CSS Grid's `grid-template-areas` is a particularly natural fit for `scID`, since both use names to identify regions:

```
 isc.Canvas.create({
     width: "100%", height: "100%",
     contents:
         '<div style="display:grid; height:100%;' +
         '     grid-template-columns: 1fr 300px;' +
         '     grid-template-rows: auto 1fr auto;' +
         '     grid-template-areas:' +
         "     'header header'" +
         "     'grid   detail'" +
         "     'footer footer';" +
         '     gap: 8px">' +
         '<h2 style="grid-area:header;' +
         '     margin:0">Dashboard</h2>' +
         '<div scID="mainGrid"' +
         '     style="grid-area:grid"></div>' +
         '<div scID="detail"' +
         '     style="grid-area:detail"></div>' +
         '<div style="grid-area:footer;' +
         '     text-align:center;' +
         '     color:#888">Status bar</div>' +
         '</div>',
     mainGridDefaults: {
         _constructor: "ListGrid",
         autoFetchData: true,
         dataSource: "employees"
     },
     detailDefaults: {
         _constructor: "DetailViewer",
         dataSource: "employees"
     }
 });
 
```
The header and footer are plain HTML; the grid and detail areas are SmartClient widgets sized by the CSS grid engine.

#### Example: Explicit Children

Instead of AutoChildren, pre-created children can be supplied in the [Canvas.children](../classes/Canvas.md#attr-canvaschildren) array. Each child's [Canvas.name](../classes/Canvas.md#attr-canvasname) must match the corresponding `scID`:

```
 isc.Canvas.create({
     width: "100%", height: "100%",
     contents:
         '<div style="display:flex; gap:10px;' +
         '     height:100%">' +
             '<div scID="gridArea"' +
             '     style="flex:1"></div>' +
             '<div scID="chartArea"' +
             '     style="flex:1"></div>' +
         '</div>',
     children: [
         isc.ListGrid.create({
             name: "gridArea",
             autoDraw: false,
             dataSource: "employees",
             autoFetchData: true
         }),
         isc.FacetChart.create({
             name: "chartArea",
             autoDraw: false,
             facets: [{ id: "region" }],
             dataSource: "employees",
             autoFetchData: true
         })
     ]
 });
 
```

#### How It Works

The framework processes `scID` placeholders during [Canvas.draw](../classes/Canvas.md#method-canvasdraw), between HTML insertion and [drawChildren()](#canvasdrawchildren). For each `scID` found in the DOM:

1.  The name is resolved to an existing child (by [Canvas.name](../classes/Canvas.md#attr-canvasname)) or an AutoChild (via [Canvas.addAutoChild()](../classes/Class.md#method-classaddautochild)). If neither resolves, a warning is logged and the placeholder is left empty.
2.  The child is connected to the placeholder element with [Canvas.htmlElement](../classes/Canvas.md#attr-canvashtmlelement) set to the placeholder, [Canvas.htmlPosition](../classes/Canvas.md#attr-canvashtmlposition) set to `"afterBegin"`, and [Canvas.matchElement](../classes/Canvas.md#attr-canvasmatchelement) set to `true`. This causes the widget to render inside the placeholder and size itself to match.
3.  The child draws in the normal [drawChildren()](#canvasdrawchildren) pass.

Because the child is rendered `position:relative` inside the placeholder, it participates in normal document flow. The placeholder's CSS (width, height, flex, grid-area, etc.) controls the widget's size and position, and [Canvas.persistentMatchElement](../classes/Canvas.md#attr-canvaspersistentmatchelement) ensures the widget tracks the placeholder through subsequent page reflows.

#### Scrolling and Responsive Behavior

Because embedded children are `position:relative` within the contents, they scroll naturally with the rest of the content when [overflow](../classes/Canvas.md#attr-canvasoverflow) is set to `"auto"` or `"scroll"`. This is a key difference from SmartClient's Layout system, which uses absolute positioning internally.

CSS media queries, `flex-wrap`, and other responsive techniques work as expected — when the browser reflows the template (for example, due to a viewport resize), [Canvas.persistentMatchElement](../classes/Canvas.md#attr-canvaspersistentmatchelement) detects the placeholder's new size and automatically resizes the embedded widget to match.

#### Dynamic Contents

[Dynamic contents](../classes/Canvas.md#attr-canvasdynamiccontents) (`${}` expressions) can be combined with `scID` placeholders. The `${}` expressions are evaluated first, producing the final HTML string, and then the framework scans the resulting DOM for `scID` attributes. This allows the template itself to be data-driven while still embedding SmartClient components.

#### Visibility

When an embedded child is hidden (via [Canvas.hide](../classes/Canvas.md#method-canvashide), [Canvas.visibleWhen](../classes/Canvas.md#attr-canvasvisiblewhen), etc.), the child's DOM handle becomes invisible but the `scID` placeholder element is unaffected — it retains whatever size and position the CSS template gives it. This follows the existing [Canvas.matchElement](../classes/Canvas.md#attr-canvasmatchelement) contract: the framework controls the widget; the CSS template controls the placeholder.

If a design requires the placeholder to collapse when the child is hidden (for example, so that flex siblings expand to fill the vacated space), this can be achieved by toggling the placeholder's own CSS from application code — for instance, setting `display:none` on the placeholder in a [Canvas.visibilityChanged](../classes/Canvas.md#method-canvasvisibilitychanged) override.

#### Redraw Behavior

When a Canvas with `scID` placeholders is redrawn (e.g., via [Canvas.setContents](../classes/Canvas.md#method-canvassetcontents) or [Canvas.markForRedraw](../classes/Canvas.md#method-canvasmarkforredraw)), the framework preserves embedded children using a detach-and-reattach strategy:

1.  Each embedded child's DOM handle is detached from its placeholder (without destroying the widget).
2.  The contents HTML is replaced in the DOM.
3.  The DOM is re-scanned for `scID` placeholders.
4.  Children already connected to an `scID` are reattached to the corresponding new placeholder element without re-resolving.

If a placeholder that previously existed is absent after redraw, the corresponding child is [cleared](../classes/Canvas.md#method-canvasclear) but not destroyed, allowing it to be reconnected if the placeholder reappears in a subsequent redraw. Conversely, if a new `scID` appears that was not in the previous contents, [Canvas.resolveContentsComponent](../classes/Canvas.md#method-canvasresolvecontentscomponent) is called to resolve it, including AutoChild creation if applicable.

For [Canvas.htmlPosition](../classes/Canvas.md#attr-canvashtmlposition) variants where the child is absolutely positioned over (rather than inside) the placeholder, a [clear()](../classes/Canvas.md#method-canvasclear) / [draw()](../classes/Canvas.md#method-canvasdraw) cycle is used instead of detach/reattach, because the child's position depends on coordinates that must be recalculated.

#### Layout Interaction

When `scID` placeholders are used in a [Layout](../classes/Layout.md#class-layout) or its subclasses (VLayout, HLayout, etc.), embedded children are positioned by the CSS template, _not_ by the Layout engine. These children are part of the [Canvas.children](../classes/Canvas.md#attr-canvaschildren) array but are not added as [Layout.members](../classes/Layout.md#attr-layoutmembers), so [Layout.layoutChildren](#method-layoutlayoutchildren) does not attempt to size or position them.

#### Restrictions

*   `scID` resolution is local to the owning Canvas. A placeholder cannot reference a widget that is not a child or AutoChild of the Canvas whose contents contains the placeholder.
*   A given `scID` value must be unique within a single Canvas's contents.
*   The placeholder element should be a block-level element (typically a ``<div>``). Using inline elements may produce unexpected sizing behavior.
*   Embedded children should not also be added as [Layout.members](../classes/Layout.md#attr-layoutmembers) of the same Canvas.
*   Embedded children are normal [Canvas.children](../classes/Canvas.md#attr-canvaschildren) and follow standard child lifecycle — they are destroyed when the parent is [destroyed](../classes/Canvas.md#method-canvasdestroy).

### Related

- [Canvas.resolveContentsComponent](../classes/Canvas.md#method-canvasresolvecontentscomponent)
- [Canvas.contentsComponentConnected](../classes/Canvas.md#method-canvascontentscomponentconnected)
- [Canvas.contentsComponentDefaults](../classes/Canvas.md#attr-canvascontentscomponentdefaults)

### See Also

- [Canvas.contents](../classes/Canvas.md#attr-canvascontents)
- [Canvas.htmlElement](../classes/Canvas.md#attr-canvashtmlelement)
- [Canvas.matchElement](../classes/Canvas.md#attr-canvasmatchelement)
- [autoChildren](autoChildren.md#kb-topic-autochildren)

---
