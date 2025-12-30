# Native Browser Zoom Support

[← Back to API Index](../reference.md)

---

## KB Topic: Native Browser Zoom Support

### Description
Native browser zooming, that is, the ability in most browsers to enlarge or shrink the entire web page, is currently only partly supported in specific browsers due to intractable browser bugs.

Support in this release is restricted to:

*   support for almost all components for Internet Explorer version 11 only, with known issues, almost all cosmetic (see below)
*   supported with the requirement that users refresh the page after changing zoom, with known cosmetic issues listed below. See also the Detecting Zoom Changes section below.
*   no support for Chrome, Safari, other Webkit browsers - support not yet possible (see below)

In addition, support guarantees are limited for zoom-related issues:

*   cosmetic issues that appear only in zoom mode will not be investigated
*   functional issues that appear only in zoom mode will be investigated if they are reproducible, but the normal guarantee of a fix or workaround is not provided, since for most zoom issues, there is no feasible way to work around the problem

Known issues by browser are listed below.
#### Chrome and Opera 15+

*   Core DOM APIs for querying position and sizing information of an element return fractional values even though they shouldn't be, which can impact layout, scrolling, and event handling. See issue [60837](http://crbug.com/60837).
*   The minimum font size feature can cause layout issues when the page zoom is decreased but the page is not refreshed at the new zoom level.
*   Chrome fails `background-image` related CSS Working Group tests with page zoom, causing background images to draw oddly in certain cases. See issues [412914](http://crbug.com/412914) and [421331](http://crbug.com/421331).
*   Borders do not scale properly, causing layout issues, cosmetic issues where borders do not line up with background images or appear beveled, and accessibility issues where borders may be too thin. See issues [257220](http://crbug.com/257220), [382483](http://crbug.com/382483), [388879](http://crbug.com/388879), [406371](http://crbug.com/406371), and [434720](http://crbug.com/434720).
*   Various issues affecting SVG drawings. See issues [181122](http://crbug.com/181122), [407159](http://crbug.com/407159), and [421926](http://crbug.com/421926).

#### Firefox

*   Firefox' approach to page zoom involves changing the layout rather than scaling the entire page content by the zoom factor. This can cause layout and scrolling issues if the zoom level is changed without refreshing the page. See [A Tale Of Two Zooms](http://robert.ocallahan.org/2007/10/tale-of-two-zooms_19.html).
*   Like Chrome and Safari, Firefox has a minimum font size feature which may cause layout issues when the page zoom is changed without refreshing the page at the new zoom level. See bug [912159](https://bugzilla.mozilla.org/show_bug.cgi?id=912159).
*   On Windows and Linux, native checkbox and radio button inputs do not scale with the page zoom. See bug [400364](https://bugzilla.mozilla.org/show_bug.cgi?id=400364).
*   A focus outline might not be drawn around the focus element when zoomed. See bug [1050753](https://bugzilla.mozilla.org/show_bug.cgi?id=1050753).
*   The form element autocomplete box does not move when the page zoom is changed. See bug [731150](https://bugzilla.mozilla.org/show_bug.cgi?id=731150).

#### Internet Explorer

*   IE may draw "seams" on [EdgedCanvas](../classes/EdgedCanvas.md#class-edgedcanvas) objects, which are faint antialiasing artifacts between the images used to make up the `EdgedCanvas`. This affects [drop shadows](../classes/Canvas.md#attr-canvasshowshadow) and showing edges with a high [Canvas.edgeSize](../classes/Canvas.md#attr-canvasedgesize). See issue [808337](https://connect.microsoft.com/IE/Feedback/Details/808337/IE11-still-shows-odd-lines-on-image-nine-patched-with-CSS-background-position).
*   Phantom borders may appear between table cells and other content that should be adjacent with no separation. This issue is also thought to be the cause of a line appearing below a selected [TabSet](../classes/TabSet.md#class-tabset) tab at certain zoom levels. See issues [808838](https://connect.microsoft.com/IE/Feedback/Details/808838/css-border-radius-and-zoom-issues) and [814033](https://connect.microsoft.com/IE/Feedback/Details/814033/weird-lines-when-zoom-set-to-150).
*   SVG content may disappear at high zoom levels. See issue [782997](https://connect.microsoft.com/IE/Feedback/Details/782997/svg-isnt-shown-on-high-zoom-levels-in-ie10).

#### Safari and WebKit

*   Core DOM APIs for querying sizing information of an element may overstate a dimension, which can impact layout, scrolling, and event handling.
*   Like Chrome and Firefox, Safari supports a minimum font size feature. This can cause layout issues to appear when the page zoom is decreased but the page is not refreshed at the new zoom level.
*   CSS `background-position` and background image clipping used for spriting may be misapplied. This can introduce visual effects where different parts of a sprite are visible. See bug [45840](https://bugs.webkit.org/show_bug.cgi?id=45840).
*   Background images can be misdrawn at certain zoom levels, where the first or last row or column of pixels in the image "wrap" to the other side. See bug [125133](https://bugs.webkit.org/show_bug.cgi?id=125133).
*   Transparent 1px-wide gaps can appear around the content area of an [EdgedCanvas](../classes/EdgedCanvas.md#class-edgedcanvas), allowing content below the `EdgedCanvas` in stacking order to show through. See bug [122061](https://bugs.webkit.org/show_bug.cgi?id=122061).
*   A phantom line may appear below a selected [TabSet](../classes/TabSet.md#class-tabset) tab at certain zoom levels.

## Detecting Zoom Changes

There is no officially supported cross-browser way of detecting zoom, and current approaches rely on hacks that browser vendors seem willing to break or deprecate. These current approaches are described at [How to detect page zoom level in all modern browsers?](http://stackoverflow.com/questions/1713771/how-to-detect-page-zoom-level-in-all-modern-browsers/) with a small proof-of-concept JavaScript library called [detect-zoom](https://github.com/tombigel/detect-zoom).

Although the detect-zoom library does not accurately determine the current zoom level, the library can be used in Firefox to detect when the zoom level _changes_ so that a warning message can be displayed to the user.

Note that the latest version of `detect-zoom.min.js` that is committed to the GitHub repository is out of date. It is not recommended to use this file because it causes a runtime `TypeError` if the script is included before the document body has been created (see [issue #41](https://github.com/tombigel/detect-zoom/issues/41)). To rebuild `detect-zoom.min.js`, you will need to install git, npm, and GNU make. Then at a terminal, run the following commands:

```
git clone https://github.com/tombigel/detect-zoom.git
cd detect-zoom
npm install
touch detect-zoom.js && make
```

Here is a complete example of using the detect-zoom library in a SmartClient project:

```
<script type="text/javascript" src="detect-zoom.min.js"></script<
<script type="text/javascript">
var lastZoom = detectZoom.zoom();
isc.Page.setEvent("resize", function () {
    var newZoom = detectZoom.zoom();
    if (newZoom != lastZoom) {
        lastZoom = newZoom;
        isc.warn("After changing the page zoom, you must refresh the page.");
    }
});
</script>
```

## Flickering Scrollbars and Workarounds

When a browser is zoomed, either directly or via OS-level zoom, it can report sizes that are slightly off and vary unpredictably, which if we took no special action would lead to flickering scrollbars, thusly:

*   we ask the browser the size of the content, it tells us it's big enough that scrollbars are required
*   we add scrollbars
*   because of subpixel measurement bugs, the browser now reports that the size of content doesn't require scrollbars
*   we remove scrollbars
*   because of subpixel measurement bugs, the browser changes its mind and decides that the same content now requires scrollbars again
*   we re-add scrollbars

To work around this issue, we rely the idea of a [maximum zoom overflow error](../classes/Canvas.md#attr-canvasmaxzoomoverflowerror), the experimental maximum possible error due to subpixel rendering when browser and/or OS-level zoom is present. This value is typically one or a few pixels, but should always be kept as small as possible because it also represents the maximum amount of unwanted clipping that the Framework might apply to the canvas when overflow is present. If too large, it will easily be noticed and may clip the edges of buttons or other content.

For example, if you execute the following sample in a zoomed desktop browser, you'll see that if you try to grab the bottom edge and drag-resize it shorter, some text will be clipped from the bottom before the scrollbar appears. This is because the [maximum zoom overflow error](../classes/Canvas.md#attr-canvasmaxzoomoverflowerror) for the sample is 25, a much larger value than ever needed but illustrative of its potential for clipping content.

```
isc.HTMLPane.create({  
   width:230, height:100, showEdges:true,
   canDragResize: true, dragResizeAppearance: "target",
   maxZoomOverflowError: 25, correctZoomOverflow: true,
   contents:"Here men from the planet Earth first set foot upon the Moon " + 
            "July 1969, A.D.  We came in peace for all mankind." 
})
 
```
**Note:** the framework should set [Canvas.correctZoomOverflow](../classes/Canvas.md#attr-canvascorrectzoomoverflow) automatically for you where it's needed, but it's explicitly set in the sample above for completeness.

If you can still reproduce the flickering scrollbar problem with our canvas default settings for your browser and OS, please contact Isomorphic and provide as much detail about your setup as possible: framework version, skin in use, whether the skin is customized, browser, browser version, OS platform and version, and any non-default visual settings for the browser or OS.

### See Also

- [Page.getDevicePixelRatio](../classes/Page.md#classmethod-pagegetdevicepixelratio)

---
