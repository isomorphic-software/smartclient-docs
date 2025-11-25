# Img Documentation

[← Back to API Index](../main.md)

---

## Class: Img

*Inherits from:* [StatefulCanvas](StatefulCanvas.md#class-statefulcanvas)

### Description
The Img widget class implements a simple widget that displays a single image.

---
## Attr: Img.usePNGFix

### Description
If false, never apply the png fix needed in Internet Explorer to make png transparency work correctly.

**Flags**: IR

---
## Attr: Img.prompt

### Description
Prompt displayed in hover canvas if [showHover](Canvas.md#attr-canvasshowhover) is true.

### Groups

- hovers

**Flags**: IRW

---
## Attr: Img.imageSize

### Description
Convenience for setting the ${isc.DocUtils.linkForRef('attr:Img.imageWidth','imageWidth) and \\n ${isc.DocUtils.linkForRef('attr:Img.imageHeight','imageHeight\\')')} attributes to the same value, for cases where [Img.imageType](#attr-imgimagetype) settings would normally use the image's natural size (applies to [Img.imageType](#attr-imgimagetype) "center" and "normal" only).

### Groups

- appearance

**Flags**: IR

---
## Attr: Img.src

### Description
The base filename or stateful image configuration for the image. Note that as the [state](StatefulCanvas.md#attr-statefulcanvasstate) of the component changes, the image displayed will be updated as described in [statefulImages](../kb_topics/statefulImages.md#kb-topic-stateful-images).

### Groups

- appearance

**Flags**: IRW

---
## Attr: Img.imageType

### Description
Indicates whether the image should be tiled/cropped, stretched, or centered when the size of this widget does not match the size of the image. CENTER shows the image in it's natural size, but can't do so while the transparency fix is active for IE. The transparency fix can be manually disabled by setting [Img.usePNGFix](#attr-imgusepngfix) to false. See ImageStyle for further details.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Img.size

### Description
Convenience for setting the ${isc.DocUtils.linkForRef('attr:StatefulCanvas.width','width) and ${isc.DocUtils.linkForRef('attr:StatefulCanvas.height','height\\')')} of this widget to the same value, at init time only. See [Img.imageSize](#attr-imgimagesize), or [Img.imageWidth](#attr-imgimagewidth) / [Img.imageHeight](#attr-imgimageheight), to control the size of the image itself for [Img.imageType](#attr-imgimagetype) settings that would normally use the image's natural size ("center" or "normal"), or where the image has no natural size, as with [SVG Symbols](../kb_topics/svgSymbols.md#kb-topic-svg-symbols-overview).

### Groups

- sizing

**Flags**: IR

---
## Attr: Img.showImageDown

### Description
Should the image be updated on mouse down as described in [statefulImages](../kb_topics/statefulImages.md#kb-topic-stateful-images)?

If not explicitly set, behavior is as follows:  
If [Img.src](#attr-imgsrc) is specified as a string, [Img.showDown](#attr-imgshowdown) will be used to determine whether to show a mouse down image.  
If [Img.src](#attr-imgsrc) is specified as a [SCStatefulImgConfig](../main.md#object-scstatefulimgconfig), the appropriate [SCStatefulImgConfig.Down](SCStatefulImgConfig.md#attr-scstatefulimgconfigdown) state image will be displayed if defined.

### Groups

- state

**Flags**: IRW

---
## Attr: Img.showDisabled

### Description
Should we visibly change state when disabled?

This will impact the [styling](StatefulCanvas.md#attr-statefulcanvasbasestyle) of the component when disabled. It may also impact the [image being displayed](#attr-imgsrc) - see also [Img.showImageDisabled](#attr-imgshowimagedisabled).

### Groups

- state

**Flags**: IRW

---
## Attr: Img.showImageDisabled

### Description
Should the image be updated when disabled as described in [statefulImages](../kb_topics/statefulImages.md#kb-topic-stateful-images)?

If not explicitly set, behavior is as follows:  
If [Img.src](#attr-imgsrc) is specified as a string, [Img.showDisabled](#attr-imgshowdisabled) will be used to determine whether to show a disabled image.  
If [Img.src](#attr-imgsrc) is specified as a [SCStatefulImgConfig](../main.md#object-scstatefulimgconfig), the appropriate [SCStatefulImgConfig.Disabled](SCStatefulImgConfig.md#attr-scstatefulimgconfigdisabled) state image will be displayed if defined.

### Groups

- state

**Flags**: IRW

---
## Attr: Img.showRollOver

### Description
Should we visibly change state when the mouse goes over this object?

This will impact the [styling](StatefulCanvas.md#attr-statefulcanvasbasestyle) of the component on roll over. It may also impact the [image being displayed](#attr-imgsrc) - see also [Img.showImageRollOver](#attr-imgshowimagerollover).

### Groups

- state

**Flags**: IRW

---
## Attr: Img.showDown

### Description
Should we visibly change state when the mouse goes down in this object? This will impact the [styling](StatefulCanvas.md#attr-statefulcanvasbasestyle) of the component on mouse down. It may also impact the [image being displayed](#attr-imgsrc) - see also [Img.showImageDown](#attr-imgshowimagedown).

### Groups

- state

**Flags**: IRW

---
## Attr: Img.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: Img.activeAreaHTML

### Description
Setting this attribute configures an image map for this image. The value is expected as a sequence of ≶AREA> tags - e.g:
```
 Img.create({ 
     src: "myChart.gif",
     activeAreaHTML:
         "<AREA shape='rect' coords='10,50,30,200' title='30' href='javascript:alert(\"30 units\")'>" +
         "<AREA shape='rect' coords='50,90,80,200' title='22' href='javascript:alert(\"22 units\")'>"
 });
 
```
Implementation notes:

*   Quotes in the activeAreaHTML must be escaped or alternated appropriately.
*   Image maps do not stretch to fit scaled images. You must ensure that the dimensions of your Img component match the anticipated width and height of your image map (which will typically match the native dimensions of your image).
*   To change the image map of an existing Img component, first set yourImg.activeAreaHTML, then call yourImg.markForRedraw(). Calls to yourImg.setSrc() will not automatically update the image map.
*   activeAreaHTML is not supported on tiled Img components (imageType:"tile").
*   Native browser support for image map focus/blur, keyboard events, and certain AREA tag attributes (eg NOHREF, DEFAULT...) varies by platform. If your image map HTML uses attributes beyond the basics (shape, coords, href, title), you should test on all supported browsers to ensure that it functions as expected.

### Groups

- appearance

**Flags**: IRWA

---
## Attr: Img.altText

### Description
If specified this property will be included as the `alt` text for the image HMTL element. This is useful for improving application accessibility.

**`altText` and hover prompt / tooltip behavior:** Note that some browsers, including Internet Explorer 9, show a native hover tooltip containing the img tag's `alt` attribute. Developers should not rely on this behavior to show the user a hover prompt - instead the [Img.prompt](#attr-imgprompt) attribute should be used.  
To set alt text _and_ ensure a hover prompt shows up in all browsers, developers may set [Img.prompt](#attr-imgprompt) and `altText` to the same value. If both these attributes are set, the standard SmartClient prompt behavior will show a hover prompt in most browsers, but will be suppressed for browsers where a native tooltip is shown for altText. Note that setting `altText` and `prompt` to different values is not recommended - the prompt value will be ignored in favor of the altText in this case.

### Groups

- accessibility

**Flags**: IRW

---
## Attr: Img.imageWidth

### Description
Explicit size for the image, for [Img.imageType](#attr-imgimagetype) settings that would normally use the image's natural size (applies to [Img.imageType](#attr-imgimagetype) "center" and "normal" only).

### Groups

- appearance

**Flags**: IR

---
## Attr: Img.showImageRollOver

### Description
Should the image be updated on rollOver as described in [statefulImages](../kb_topics/statefulImages.md#kb-topic-stateful-images)?

If not explicitly set, behavior is as follows:  
If [Img.src](#attr-imgsrc) is specified as a string, [Img.showRollOver](#attr-imgshowrollover) will be used to determine whether to show a roll-over image.  
If [Img.src](#attr-imgsrc) is specified as a [SCStatefulImgConfig](../main.md#object-scstatefulimgconfig), the appropriate [SCStatefulImgConfig.Over](SCStatefulImgConfig.md#attr-scstatefulimgconfigover) state image will be displayed if defined.

### Groups

- state

**Flags**: IRW

---
## Attr: Img.showTitle

### Description
Determines whether any specified [title](StatefulCanvas.md#method-statefulcanvasgettitle) will be displayed for this component.  
Applies to Image-based components only, where the title will be rendered out in a label floating over the component

**Flags**: IRWA

---
## Attr: Img.showFocused

### Description
Should we visibly change state when the canvas receives focus? If [StatefulCanvas.showFocusedAsOver](StatefulCanvas.md#attr-statefulcanvasshowfocusedasover) is `true`, then **`"over"`** will be used to indicate focus. Otherwise a separate **`"focused"`** state will be used.

This will impact the [styling](StatefulCanvas.md#attr-statefulcanvasbasestyle) of the component on focus. It may also impact the [image being displayed](#attr-imgsrc) - see also [Img.showImageFocused](#attr-imgshowimagefocused).

### Groups

- state

**Flags**: IRW

---
## Attr: Img.showImageFocused

### Description
Should the image be updated on focus as described in [statefulImages](../kb_topics/statefulImages.md#kb-topic-stateful-images)?

If not explicitly set, behavior is as follows:  
If [Img.src](#attr-imgsrc) is specified as a string, [Img.showFocused](#attr-imgshowfocused) will be used to determine whether to show a focused image.  
If [Img.src](#attr-imgsrc) is specified as a [SCStatefulImgConfig](../main.md#object-scstatefulimgconfig), the appropriate [SCStatefulImgConfig.Over](SCStatefulImgConfig.md#attr-scstatefulimgconfigover) state image will be displayed if defined.

Note that if [Img.src](#attr-imgsrc) is defined as a string, the "Over" media may be used to indicate a focused state. See [Img.showFocusedAsOver](#attr-imgshowfocusedasover) and [Img.showImageFocusedAsOver](#attr-imgshowimagefocusedasover).  
This is not the case for components with [Img.src](#attr-imgsrc) defined as a [SCStatefulImgConfig](../main.md#object-scstatefulimgconfig) configuration.

### Groups

- state

**Flags**: IRW

---
## Attr: Img.name

### Description
The value of this attribute is specified as the value of the 'name' attribute in the resulting HTML.

Note: this attribute is ignored if the imageType is set to "tile"

**Flags**: IA

---
## Attr: Img.imageHeight

### Description
Explicit size for the image, for [Img.imageType](#attr-imgimagetype) settings that would normally use the image's natural size (applies to [Img.imageType](#attr-imgimagetype) "center" and "normal" only).

### Groups

- appearance

**Flags**: IR

---
## Attr: Img.showFocusedAsOver

### Description
If [showFocused](StatefulCanvas.md#attr-statefulcanvasshowfocused) is true for this widget, should the `"over"` state be used to indicate the widget as focused. If set to false, a separate `"focused"` state will be used.

This property effects the css styling for the focused state.  
If [Img.src](#attr-imgsrc) is specified as a string it will also cause the "Over" media to be displayed to indicate focus, unless explicitly overridden by [Img.showImageFocusedAsOver](#attr-imgshowimagefocusedasover). Note that this has no impact on the image to be displayed if [Img.src](#attr-imgsrc) is specified as a [SCStatefulImgConfig](../main.md#object-scstatefulimgconfig).

### Groups

- state

**Flags**: IRW

---
## Attr: Img.showImageFocusedAsOver

### Description
If [Img.src](#attr-imgsrc) is defined as a string, and this component is configured to [show focused state images](#attr-imgshowimagefocused), this property will cause the `"over"` state image to be used to indicate focused state. (If unset, [Img.showFocusedAsOver](#attr-imgshowfocusedasover) will be consulted instead).

Note that this has no impact on the image to be displayed if [Img.src](#attr-imgsrc) is specified as a [SCStatefulImgConfig](../main.md#object-scstatefulimgconfig).

### Groups

- state

**Flags**: IRW

---
## Method: Img.setImageType

### Description
Change the style of image rendering.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| imageType | [ImageStyle](../main.md#type-imagestyle) | false | — | new style of image rendering |

---
## Method: Img.getHoverHTML

### Description
If `this.showHover` is true, when the user holds the mouse over this Canvas for long enough to trigger a hover event, a hover canvas is shown by default. This method returns the contents of that hover canvas.

Overridden from Canvas:  
If [Img.prompt](#attr-imgprompt) is specified, and [Img.altText](#attr-imgalttext) is unset, default implementation is unchanged - the prompt text will be displayed in the hover.  
If [Img.altText](#attr-imgalttext) and [Img.prompt](#attr-imgprompt) are set this method will return null to suppress the standard hover behavior in browsers where the alt attribute on an img tag causes a native tooltip to appear, such as Internet Explorer. On other browsers the altText value will be returned.

### Returns

`[String](#type-string)` — the string to show in the hover

### Groups

- hovers

### See Also

- [Canvas.showHover](Canvas.md#attr-canvasshowhover)

---
## Method: Img.setSrc

### Description
Changes the URL of this image and redraws it.

Does nothing if the src has not changed - if `src` has not changed but other state has changed such that the image needs updating, call [Img.resetSrc](#method-imgresetsrc) instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| URL | [SCImgURL](../main.md#type-scimgurl) | false | — | new URL for the image |

### Groups

- appearance

---
## Method: Img.resetSrc

### Description
Refresh the image being shown. Call this when the [Img.src](#attr-imgsrc) attribute has not changed, but other state that affects the image URL (such as being selected) has changed.

### Groups

- appearance

**Flags**: A

---
