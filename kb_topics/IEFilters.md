# Internet Explorer "filter" effects

[← Back to API Index](../main.md)

---

## KB Topic: Internet Explorer "filter" effects

### Description
In order to compensate for various bugs and missing features in Internet Explorer, it's necessary to use Microsoft-proprietary "filter" settings, as follows:

*   IE6-8: Opacity filter required for opacity to work at all
*   IE6: AlphaImageLoader filter required for PNG transparency to work at all
*   IE7-8: AlphaImageLoader filter required for PNG transparency to work properly with opacity (eg, translucent rounded windows), otherwise, PNGs will turn entirely black or show other severe artifacts when opacity is applied

Using these filters has a range of side-effects:

*   AlphaImageLoader will cause the UI to appear frozen until users have downloaded all PNG media shown on the page
*   moderate to severe impact on rendering speed (20-60%)
*   font smoothing is disabled

For an application that is frequently used (where images will typically be cached) on recent machines, and where font smoothing is not considered important, no special steps need to be taken.

If any of the above side effects are important, our recommendations are:

*   minimize use of PNG media - use .gif instead
*   for IE7-8, [disable AlphaImageLoader](../classes/Canvas.md#classattr-canvasneverusepngworkaround) and [disable Opacity](../classes/Canvas.md#attr-canvasuseopacityfilter) globally since these browsers can only render PNGs correctly in the absence of opacity settings. Selectively enable opacity only in widgets that do not contain PNGs (eg the modalMask shown by a Window). Avoid the use of opacity fades as a transition effect for IE unless you have eliminated all or almost all PNG media and the remaining artifacts are considered acceptable. Also eliminate all use of filter effects in CSS, and [disable the workaround](../classes/Canvas.md#classattr-canvasallowexternalfilters) that makes this possible.
*   if IE6 performance is critically important, eliminate all PNG media and all use of opacity and [disable all filters](../classes/Canvas.md#classattr-canvasneverusefilters).

Note that the .gif format does not support partially transparent pixels, hence can't be used for very high-quality antialiasing effects. However, certain specific tools can produce high-quality anti-aliased images in the less known PNG8 format, and this particular format has the least artifacts in the above situations. Details [here](http://blogs.sitepoint.com/2007/09/18/png8-the-clear-winner/).

### Related

- [Canvas.setNeverUseFilters](../classes/Canvas.md#classmethod-canvassetneverusefilters)
- [Canvas.setAllowExternalFilters](../classes/Canvas.md#classmethod-canvassetallowexternalfilters)
- [Canvas.neverUsePNGWorkaround](../classes/Canvas.md#classattr-canvasneverusepngworkaround)
- [Canvas.neverUseFilters](../classes/Canvas.md#classattr-canvasneverusefilters)
- [Canvas.allowExternalFilters](../classes/Canvas.md#classattr-canvasallowexternalfilters)
- [Canvas.useOpacityFilter](../classes/Canvas.md#attr-canvasuseopacityfilter)
- [DrawImage.useMatrixFilter](../classes/DrawImage.md#attr-drawimageusematrixfilter)

---
