# DOM Integration & Third-party Components

[← Back to API Index](../main.md)

---

## KB Topic: DOM Integration & Third-party Components

### Description
SmartClient provides a huge variety of pre-built components and allows you to create new components via combining and composing the existing components. However in rare cases, it can make sense to write code that works directly with raw HTML and the browser's DOM (document object model) APIs. This level of coding is also involved when integrating third-party JavaScript components into SmartClient applications.

First, a warning: when you use HTML and the DOM directly, all of SmartClient's guarantees of cross-browser consistent behavior no longer apply. When you use SmartClient's API, SmartClient is automatically compensating for many, many browser bugs - not just trivial things like different property names or missing utility methods, but problems where browsers fail to fire certain events, report sizes wrong only in certain modes with certain styling, or bugs that only occur with specific timing.

Before deciding to do direct HTML coding, consider whether you really want to expose yourself to all of these possible issues. If you can achieve the same look and feel and behavior through SmartClient's APIs, that's usually best.

#### Adding or modifying the DOM

The DOM structures used by SmartClient necessarily differ by browser in order to work around each browser's specific bugs. This DOM structure is intentionally undocumented because it is subject to change without notice - in may be necessary to modify the DOM structure to work around the bugs in each new browser release.

Instead of trying to modify the SmartClient-generated DOM, you should always **add new elements**. For a new standalone component that will be based on direct use of HTML, you usually do this by subclassing Canvas and overriding [Canvas.getInnerHTML](../classes/Canvas.md#method-canvasgetinnerhtml) and returning an HTML string representing the components you want to create.

You can use a similar approach anywhere HTML is allowed in a widget property: formatting APIs for StaticTextItem, DetailViewer, TileGrid, and other DataBoundComponents, as well as places such as [Tab.title](../classes/Tab.md#attr-tabtitle) or [Button.title](../classes/Button.md#attr-buttontitle).

#### Third-party components

Most third-party JavaScript components have the ability to generate their HTML content into a DOM element specified by ID, or to replace such an element with new HTML. This is true of Google Maps, [CKEditor](http://ckeditor.com) and many other libraries.

To use this form of integration, implement a [Canvas.getInnerHTML](../classes/Canvas.md#method-canvasgetinnerhtml) function that returns a DOM element with a known ID, then have the third-party library target that DOM element once the Canvas is drawn. For example, CKEDITOR.replace() takes the ID of a `<textarea>` element, and the following code would create a `<textarea>` and have the CKEditor replace it with a CKEditor widget:

```
 isc.defineClass("CKEditor", "Canvas");
 isc.CKEditor.addProperties({
     // write out a textarea with a known ID
     getInnerHTML : function () {
         return "<textarea style="width:100%;height:100%" ID='" + 
                           this.getID() + "_ckEditor'></textarea>";
     },
     // call superclass method to draw, then have CKEditor replace the textarea we
     // wrote out with the CKEditor widget
     draw : function () {
         if (!this.readyToDraw()) return this;
         this.Super("draw", arguments);
         CKEDITOR.replace(this.getID() + "_ckEditor");
         return this;
     },
     redrawOnResize:false // see next section
 });
 
```

This same approach can be used when you want to insert third-party generated HTML into just a specific part of a SmartClient widget. For example, you might want to insert [JQuery 'sparklines'](https://www.google.com/search?q=jquery+sparklines), which are essentially miniature charts, into cells of a ListGrid. You could use [a cell formatter](../classes/ListGridField.md#method-listgridfieldformatcellvalue) to write out `<div>` elements with known IDs into the cells, then target them with JQuery.  

If a third party component is being embedded into a SmartClient widget, developers should consider which [overflow setting](../classes/Canvas.md#attr-canvasoverflow) is most appropriate to use. Oftentimes you'll want your embedded component to size to the available space. In this case you should use `overflow:"hidden"`. However if the embedded component will render at a specific size, and you want to have the component size to fit it, `overflow:"visible"` may be appropriate.

Developers embedding third party text editing components into SmartClient widgets should typically set [Canvas.canSelectText](../classes/Canvas.md#attr-canvascanselecttext) to `true` on the SmartClient widget. This prevents the SmartClient event management system potentially interfering with any native events such as focus, selection and copy/paste behavior as the user interacts with the embedded editor.

#### Resizing and Redraw

When implementing `canvas.getInnerHTML()`, your getInnerHTML() function will be called every time the component redraw()s, and the new HTML will replace the old.

Also by default, your component will redraw() if it is resized. In the example above with CKEditor, we wouldn't want this because it would wipe out the CKEditor widget every time it was resized, so we set [Canvas.redrawOnResize](../classes/Canvas.md#attr-canvasredrawonresize) to false. In other circumstances you may want to redraw on every resize in order to generate new HTML.

If you do not redraw HTML on resize, you either have to write the HTML in a way that makes it flow into available space (width/height 100% may be enough here) **or** you need to manually resize the DOM element when the [resized event](../classes/Canvas.md#method-canvasresized) fires.

In the latter case, you should adjust the size of the DOM element to match the [inner width](../classes/Canvas.md#method-canvasgetinnerwidth) and [inner height](../classes/Canvas.md#method-canvasgetinnerheight) of the containing Canvas. The "inner" dimensions are the dimensions after border and margins have been subtracted, so this will work even if a border is added to your Canvas subclass via CSS or [Canvas.setBorder](../classes/Canvas.md#method-canvassetborder).

#### Other redraws

Once you have set [Canvas.redrawOnResize](../classes/Canvas.md#attr-canvasredrawonresize) to false you may still see redraws from other sources. Generally this would be from code in your application which calls [Canvas.redraw](../classes/Canvas.md#method-canvasredraw) or [Canvas.markForRedraw](../classes/Canvas.md#method-canvasmarkforredraw) unnecessarily. To troubleshoot, you can enable the "redraws" log category in the Developer Console - this will log the source of any redraws in the system.

#### Component-specific considerations
In addition to complete redraws, certain components will refresh areas of the DOM dynamically without a full redraw. For example if you are using a ListGrid cell formatter to write out a particular DOM structure in a grid cell, this structure may be removed from the DOM or regenerated in a number of ways including explicit calls to [ListGrid.refreshCell](../classes/ListGrid_2.md#method-listgridrefreshcell), automatic cell refresh due to data changing, cells being shown or hidden due to [incremental rendering](../classes/ListGrid_1.md#attr-listgridshowallrecords), etc. Developers will need to consider how best to handle the lifecycle of the DOM elements they create  
HTML customization within other components may require similar consideration.

Another consideration specific to ListGrids is that fact that in some circumstances the HTML returned by a cell formatter may be rendered outside the grid body. An example of this is the drag tracker HTML generated when [ListGrid.dragTrackerMode](../classes/ListGrid_1.md#attr-listgriddragtrackermode) is set to "record". The [inactive cell formatter](../classes/ListGrid_2.md#method-listgridformatinactivecellvalue) may be provided to emit alternative HTML for rendering these 'inactive' versions of the cell content (allowing developers to, for example, exclude explicit element IDs).

#### Masking during drags

Third-party components that utilize iframes, browser plugins or other special elements will "swallow" events such that SmartClient never receives them. This is a problem whenever a drag interaction goes over the component, including drag resizing of the component itself. To avoid this issue, set [Canvas.useDragMask](../classes/Canvas.md#attr-canvasusedragmask) for any component that contains an iframe or browser plugin, or that appears to be swallowing events during drag. The telltale sign is that when the mouse goes over the plugin, the visual effect of the drag (differs by [Canvas.dragAppearance](../classes/Canvas.md#attr-canvasdragappearance)) stops updating or stutters.

#### Overflow & Auto-Sizing

Consider which [Canvas.overflow](../classes/Canvas.md#attr-canvasoverflow) setting to use for your custom component:

*   `overflow:"hidden"` is the most common. In the context of third-party components, it means the component is prepared to render itself at any requested size (above a minimum).
*   `overflow:"visible"` means you want SmartClient to attempt to automatically determine a minimum size based on the HTML content generated by the custom component
*   `overflow:"auto"` is similar to `overflow:"hidden"`, but means your custom component needs SmartClient to create scrollbars whenever its HTML content does not fit in the allocated space.

Note that with the automatic measurement of HTML content enabled by `overflow:"visible"` or `overflow:"auto"`, if you make on-the-fly modifications to the HTML you returned from `getInnerHTML()`, there is no cross-browser-reliable way for the Canvas to detect this and auto-size again. Instead, call [Canvas.adjustForContent](../classes/Canvas.md#method-canvasadjustforcontent) to trigger auto-sizing again.

#### zIndex

zIndex values control what component is rendered "on top" when multiple components appear in the same area of the page.

To work around various browser issues, SmartClient components use a very high range of zIndex values. If a component creates pop-up widgets such as hovers or floating toolbars via direct HTML/DOM usage, these pop-up widgets will appear **behind** all SmartClient components unless they set a very high zIndex.

For your own custom HTML/DOM components, the simplest strategy is to create pop-up widgets based on SmartClient components, even if they are triggered by interacting with hand-created HTML. For example, even if you've written some kind of advanced SVG-based data visualization component, you can still implement pop-up configuration dialogs based on the SmartClient [Window](../classes/Window.md#class-window) class; there's no reason to implement such dialogs directly in low-level HTML/DOM code.

If a third-party widget is creating pop-ups you don't directly control, you may be able to configure the third-party widget to use a certain zIndex range, or you may be able to directly reach into the widget's DOM and modify zIndexes that way. You can use [Canvas.getZIndex](../classes/Canvas.md#method-canvasgetzindex) to discover the zIndex of any SmartClient widget you need to appear above, then set a higher value.

Finally, as a last resort and completely unsupported approach, you can modify the zIndex range used by SmartClient using the following JavaScript code :

```
 isc.Canvas.addClassProperties({
    // default zIndex for the next item to be drawn
    _nextZIndex:200000,

    // zIndex of the next item to be sent to the back
    _SMALL_Z_INDEX:199950,

    // zIndex of the next item to be brought to the front
    _BIG_Z_INDEX:800000
 });
 
```

#### Tab Order
Focusable elements embedded in a SmartClient page should be accessible via tabbing. Developers may use the [TabIndexManager](../classes/TabIndexManager.md#class-tabindexmanager) to ensure custom elements are reachable via tab keypresses and show up at the appropriate place in the page's tab order. For details on how to achieve this, see the overview [here](customTabElements.md#kb-topic-including-custom-elements-in-the-tab-order). For a more general overview of the tab order within SmartClient, see the [tab order overview](tabOrderOverview.md#kb-topic-tab-order-overview).

#### Other issues

There are several other issues, listed below, for which there really is no general strategy for solving the issue, although some general pointers are provided.

Because of problems like these, it's a very very bad idea to freely intermix components from multiple component libraries. While mixing components may appear to be an appealing strategy and you may experience apparent success with early attempts, the issues below will ultimately prevent you from completing an application of sufficient quality for enterprise use.

In the following discussion, "third-party widgets" should be understood to include widgets that you write using direct DOM/HTML techniques.

*   **tabbing order / accessibility**: a correct tabbing order that visits all components on the page is a requirement for your application to be considered accessible, as is ARIA markup (for more information, see [accessibility](accessibility.md#kb-topic-accessibility--section-508-compliance)).  
    Third party widgets may or may not write out ARIA markup. This may require you to modify them or reach into their DOM to add ARIA attributes.
*   **modality**: aside from zIndex issues covered above, modality means that the tab order should be a closed loop that reaches only active widgets, which can create additional complexity in getting tabbing to work correctly. Also, keyboard shortcuts should be disabled for inactive widgets; this may require calls to [EventHandler.targetIsMasked](../classes/EventHandler.md#classmethod-eventhandlertargetismasked) to make third-party widgets respect SmartClient modality, or may require calls to [Canvas.showClickMask](../classes/Canvas.md#method-canvasshowclickmask) to cause SmartClient components to consider themselves inactive when a third-party widget opens a pop-up that is intended to be modal. Multi-layered modality, such as a modal window that in turn pops a modal dialog, is yet more complex.
*   **bad CSS**: some third-party widgets introduce CSS selectors that target, for example, every table cell on the entire page. This very bad practice will interfere with SmartClient (or any other HTML on the page). This may require modifying the third-party component, or extensively modifying SmartClient CSS to reverse any changes caused by third-party CSS. For example, it may be necessary to modify every SmartClient CSS style that may be applied to a table cell to reverse a change in padding for all table cells that is introduced by bad third-party CSS.
*   **skinning**: third-party widgets may lack sufficient skinning APIs to allow you to match look and feel to SmartGWT, which may necessitate creating a custom SmartGWT skin to match the look and feel of third-party widgets (see [Skinning Overview](skinning.md#kb-topic-skinning--theming))
*   **event interference**: third-party widgets may register page-wide event handling logic that conflicts with or destroys similar event handling logic in SmartClient. For best results, load third-party JavaScript libraries **before** SmartClient since SmartClient makes a best effort to preserve any previously installed handlers and allows such handlers to cancel native browser behaviors if they do so.
*   **RTL / i18n**: third party widgets may not allow all user-visible messages to be replaced, a requirement for internationalization / localization, or they may not support RTL/BIDI (Right-To-Left / Bi-Directional) rendering

Because of issues like the above, not all of which may be resolvable for some third-party widgets, we recommend the following overall approach:

*   avoid using third-party widgets if you can build equivalent functionality in SmartClient
*   if the third-party component is completely non-interactive, either does not require ARIA markup or already includes such markup, and there are no conflicting look and feel issues, go ahead and use it
*   if you anticipate issues, consider the [Feature Sponsorship Program](http://www.smartclient.com/services/index.jsp#features) as a means of getting new supported functionality added to SmartClient
*   search for existing posts and/or ask about the feasibility of integration on the [SmartClient Forums](http://forums.smartclient.com/).
*   finally, you could attempt to tackle the issues above on your own. To avoid wasting time on dead ends, we would recommend assessing the amount of work involved in fixing **all** problems that need to be solved before attempting actual fixes for any one issue.

---
