# SVG Symbols Overview

[← Back to API Index](../main.md)

---

## KB Topic: SVG Symbols Overview

### Description
SVG or Structured Vector Graphics are not bitmapped-images in the tradition sense, but rather an XML-based vector image format that defines a list of vectors that describe how one or more lines or shapes should be rendered. This means that SVG graphics are typically small and compressible as text, and can be drawn at any size without losing quality, a powerful capability when dealing with images.

SVG can be loaded directly in a page and, when loaded in this way, can be accessed/modified in JavaScript and affected by CSS at runtime. However, such modifications can be costly and are known to cause flickering in some browsers, due to files being reloaded and necessary DOM changes when images are reloaded/updated.

#### Spriting with SVG `<symbol>`s
Unlike bitmaps, SVG are individual entities and can't be sewn together into a "compound image", in the traditional sense, for use with spriting. However, it is possible to combine individual `<svg>`s into a single `<svg>` container as `<symbol>` elements. These are template definitions which aren't rendered in the browser - but instances of them can be created by id at runtime using the framework sprite mechanism, via the special src-string prefix `sprite:svg:`.

This approach is great for working with SVG graphics in your app because it works for any SVG and doesn't cause server trips or make sizable DOM modifications. However, it does require some preparation and has limits in terms of runtime styling.

#### Making the sprite container
The `<svg>` container can be defined externally in a .svg file or inline in your HTML, but it must conform to the following rules:

*   it should contain the root `<svg>` element
*   the `<svg>` tag should contain `<symbol>` tags, which are equivalent to the `<svg>` tag itself and support all of the same child elements. See below for notes on preparing symbols.
*   the root element may also define a `<style>` element, and a top-level `<defs>` tag may be included to define shared reusable elements such as gradients - however, these elements may prevent runtime styling, or may not be available in the main document when the `<symbol>` fragments are reused in different contexts. If your `<symbol>`s are styled by CSS classes, these must be defined in a separate .css file, which should be loaded in your page. See **_Styling Symbols_** below.

A valid `<svg>` container for reusable `<symbol>` fragments might look like this:
```
 <svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
     aria-hidden="true" style="position: absolute; width: 0; height: 0; overflow: hidden;" 
 >
    <symbol id="icon-play" viewBox="0 0 32 32">
        <path d="M6 4l20 12-20 12z"></path>
    </symbol>
    <symbol id="icon-pause" viewBox="0 0 32 32">
        <path d="M4 4h10v24h-10zM18 4h10v24h-10z"></path>
    </symbol>
 </svg>
 
```

An `<svg>` container structured in this way will not be rendered in the browser, but the `<symbol>`s it defines are made available as a set of templates which can be re-used later in `src` strings, via the special prefix _"sprite:svg:"_. The format of `src` strings differs slightly according to where your `<svg>` container is defined. If it's defined inline in the HTML, only the fragment-id is required - for example

```
src: "sprite:svg:#icon-play"
```
If it's defined in a separate file, you must also specify which file:
```
src: "sprite:svg:path/to/fileName.svg#icon-play"
```
When the external file-name is specified in this way, there is no need for the developer to explicitly load the file.

Note that this mechanism is not explicitly supported in any version of Internet Explorer, since that browser has never had full SVG support.

#### Preparing symbols
To convert a .svg file to a symbol tag, copy the `<svg>` and its content, remove everything from the opening svg tag except for the viewbox setting, which represents the designed size, add a unique id attribute to reference this image later in src-strings, and rename it from an svg tag to a symbol tag. If you want one of the colors in your symbol to be mutable at runtime, find and replace it with the special value "currentColor" (see **_Styling Symbols_** below).

Since SVG is XML-based, individual SVG editors and other tools often write additional metadata into .svg files. This extra context is not relevant to using these graphics as symbols in the framework and can usually be entirely removed without ill effects. For example, here is a .svg file exported from a popular image-editing software and its equivalent symbol element-content.

```
 <?xml version="1.0" encoding="UTF-8" standalone="no"?>
 <!-- Generator: Adobe Illustrator 28.0.0, SVG Export Plug-In . SVG Version: 6.00 Build 0)  -->
 
 <svg
   version="1.1"
   id="someID"
   x="0px"
   y="0px"
   viewBox="0 0 2500 2500"
   enable-background="new 0 0 2500 2500"
   xml:space="preserve"
   xmlns="http://www.w3.org/2000/svg"
   xmlns:svg="http://www.w3.org/2000/svg"><defs
   id="defs1" />
<path
   fill-rule="evenodd"
   clip-rule="evenodd"
   d="M1237.77,0.57c-33.09,4.54-61.94,30.54-70.21,63.29 ..."
   id="path1"
   style="fill:#3d618a;fill-opacity:1" />
</svg>
 
```

Following the instructions above, this .svg will end up as a runtime-stylable symbol like this:

```
<symbol id="add" viewBox="0 0 2500 2500" >
    <path
   fill-rule="evenodd"
   clip-rule="evenodd"
   d="M1237.77,0.57c-33.09,4.54-61.94,30.54-70.21,63.29 ..."
   id="path1"
   style="fill:currentColor;fill-opacity:1" />
</symbol>
 
```
#### Using symbols
Symbols are used by referencing them in src-strings prefixed "sprite:svg:". This format supports a number of inline attributes separated by ";" characters. The basic format is:
```
 "sprite:svg:[path-to-file.svg]#[symbolId];" 
```
Additional supported properties include:

*   size:\[w,h\] - the pixel-size of the SVG when rendered - if not provided, size is derived from image-related sizes on the container, such as [Img.imageWidth](../classes/Img.md#attr-imgimagewidth) or [FormItem.pickerIconWidth](../classes/FormItem.md#attr-formitempickericonwidth) - if no such sizes exist, SVGs will be rendered at the browser's default size for symbols, which is typically 300x150.
*   color:\[color\] - applies a fixed color to this symbol-usage - this color will not change with state
*   opacity:\[0-1\] - applies CSS opacity in the range 0.0 to 1.0, where 1.0 is fully opaque
*   cssClass:\[className\] - applies a CSS class-name to the span that wraps the SVG - the CSS class may be simple or stateful - if "color" is also in the src-string, color wins
*   statefulId:\[true/false\] - uses a different symbol for states, by appending "\_\[State\]" to the end of the provided symbolId - for example, an "Over" state requires that there be a symbol in the same sprite container with the id _\[symbolId\]_\_Over
*   statefulClass:\[true/false\] - when set to false, prevents the cssClass from having states appended to it - defaults to true, or to false if _statefulId_ is true
*   rotate:\[angle\] - rotates the image via a CSS _transform_ like "transform: rotate({angle}deg);" - this is a shortcut for directly using "transform", which is also supported in src-strings
*   transform:\[CSS-transform\] - applies one or more space-separated CSS transforms to the image - if you use this, don't use "rotate" separately in your src-string, because elements can only have one _transform_ setting

The following attributes are also supported but are unlikely to be as useful - see the following section on **_Styling symbols_** for more details.

*   fill:\[color\] - a color to apply as a fill to closed shapes that don't specify a color
*   stroke:\[color} - a color to apply to stroked lines that don't specify a stroke - may also form the outlines of closed shapes
*   stroke-width:\[1px, eg} - the width of stroked lines that don't specify a width

See below for example usages.

#### Styling symbols
As with regular SVG, it's possible to modify the colors and other styles of `<symbol>`s at runtime. However, browsers render `<symbol>`s inside `<use>` tags, and these elements keep their content separate from the main document, in DocumentFragments in the browser's shadow DOM. These fragments are not subject to the main document's scope/CSS cascade so, while it's possible to modify the styles of complex/multi-color `<symbol>`s, it does rely on your graphics having been carefully constructed to include no direct styling, or to ensure that styling is applied via CSS classes which are declared externally and loaded directly.

At its most basic, individual graphics elements in a `<symbol>` which do not specify colors inline can be easily modified. If all child elements are unstyled (ie, the symbol is single-color, even if it has multiple child graphics), the image-color can be changed as a whole by applying external CSS that sets the SVG _fill_ and _stroke_ settings to different colors. If some child elements have inlined styles, they will not be modified by such external CSS - this means that certain parts of a `<symbol>` can be of a fixed-color, via inlined styles, while other parts can be left unstyled and can be customized via external CSS later, to highlight only those unstyled parts.

**Note, however, that this is not the recommended approach:** Applying custom styles via _fill_ and _stroke_ can be difficult to achieve consistently across different images, which may use fills or strokes in any combination, or use "compound paths" to render what looks like a stroked line-drawing but is actually various filled shapes. We provide a sample of this mechanism in our [online showcase](https:\\www.smartclient.com\smartclient-latest\showcase\?id=svgSymbols) - the graphics in this sample are all stroked lines which also form closed-shapes, meaning that both stroke and fill have an effect; but this is unlikely to be true in many cases.

#### The recommended approach
The recommended approach to applying custom colors is to ensure that all parts of your `<symbol>` that should change color are given the special fill or stroke value "currentColor", like `fill="currentColor"` or `style="fill:currentColor;"`. This value is always equal to the current/inherited CSS `color` and can be referenced by graphics elements. If your CSS class sets `fill` and `color` to different values, graphics elements that use `currentColor` will assume the `color` value, while filled paths that do not specify a `fill` will respond to CSS "fill".

To achieve this, your SVGs will need to be saved with fill/stroke colors inline where they apply, and the parts that should change color later should all use the same known color. As part of preparing your symbol, find and replace that known color with "currentColor". Now, when this graphic is used later, any parts with fill or stroke set to "currentColor" will inherit the CSS "color" value from its container, or from a "cssClass" or "color" setting in the src string.

As noted above, it's also possible to fully re-style more complex, multi-color SVG - but this involves ensuring that all styling is externalized and backed by CSS; these details are highly dependent on the graphics and as such are the responsibility of the graphics designer or generator tool.

For demonstration code, see the _SVG Symbols_ sample in our [online showcase](https:\\www.smartclient.com\smartclient-latest\showcase\?id=svgSymbols)

#### Simple Icons Example
Consider a set of single-color SVG `<symbol>`s that you want to leverage as re-usable icons in your projects. You may want to show them in different colors in different contexts such as buttons, menus or formItems, and you may want them to be stateful, changing color as you roll over or disable them. This is easily achieved in two ways:

*   if your graphics do not apply any fill or stroke colors at all, browsers will use their default fill and stroke colors when rendering your symbols (typically, both black), but you can modify these defaults by applying a simple CSS class that sets them. SmartClient skins provide a builtin `svgIcon` style that you can use or modify for this purpose, or you can create your own custom styles. However, note that this technique can be inconsistent depending on design-choices across images, as described above
*   if your graphics set one or more fill or stroke settings to "currentColor", your images will inherit their color from their container, or from a cssClass or color setting applied in the src string.

For example, an external CSS class could be created:
```
 // grey color changing to red on rollover
 .icon { color: grey; }
 .iconOver { color: red; }
 
```
This class can then be applied to a stateful widget housing a symbol, via its [baseStyle](../classes/StatefulCanvas.md#attr-statefulcanvasbasestyle) or similar, or by including it directly in `src` strings via "cssClass", or as separate per-state URLs in an [SCStatefulImgConfig](../main.md#object-scstatefulimgconfig) object.
```
 isc.Img.create({
     // show stateful styles
     showRollOver: true,

     // use baseStyle for statefulness
     src: "sprite:svg:fileName.svg#icon-id;",
     baseStyle: "icon"

     // or, use cssClass in config-strings for statefulness
     src: "sprite:svg:fileName.svg#icon-id;cssClass:icon;"

     // or, use a specific cssClass for each state, in an SCStatefulImgConfig block
     // - note, all states are supported, but this sample code only shows 2
     src: {
         _base: "sprite:svg:fileName.svg#icon-id;cssClass:icon;",
         Over: "sprite:svg:fileName.svg#icon-id;cssClass:iconOver;",
     }

 })
 
```

Developers can also override `color` on a per usage basis, by specifying it directly in sprite-config `src` strings

```
 isc.Img.create({
     src: {
         _base: "sprite:svg:fileName.svg#icon-id;color:grey;",
         Over: "sprite:svg:fileName.svg#icon-id;color:red;",
     }
 })
 
```

Most UI elements provide colors that will be picked up by child symbols that don't specify a cssClass or color - for example, a symbol used as the icon in a MenuItem will show skin-appropriate stateful colors automatically. [MenuItem.icon](../classes/MenuItem.md#attr-menuitemicon) is not itself a stateful attribute, but its colors will be inherited from the menu's stateful [icon-field](../classes/Menu.md#attr-menuiconfieldproperties) if not specified.

```
 isc.Menu.create({
     items: [
         { title: "Option 1", icon: "sprite:svg:fileName.svg#icon-id" }
     ]
 })
 
```

### Related

- [Media.svgAutoScale](../classes/Media.md#classattr-mediasvgautoscale)
- [Media.svgUseDefaultSize](../classes/Media.md#classattr-mediasvgusedefaultsize)
- [Media.svgDefaultSize](../classes/Media.md#classattr-mediasvgdefaultsize)

---
