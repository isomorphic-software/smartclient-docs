# PrintCanvas Documentation

[← Back to API Index](../reference.md)

---

## Class: PrintCanvas

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
PrintCanvas is a subclass of canvas which renders printable content HTML and provides APIs for printing this content as a separate document.

### Groups

- printing

---
## Attr: PrintCanvas.externalStylesheet

### Description
Setting this property will cause the specified stylesheet to be loaded in this print canvas's frame. The stylesheet should be specified as a URL to load.

**Flags**: IRWA

---
## Attr: PrintCanvas.printFrameURL

### Description
Location of the special printFrame html file provided as part of the SmartClient libraries. This file must be present at the specified location for the printCanvas printing APIs.

**Flags**: IRA

---
## Method: PrintCanvas.setHTML

### Description
Update the HTML content displayed in this print canvas. If the printCanvas is not yet drawn the HTML will be displayed when the canvas is drawn.

Note that if the printCanvas is [redrawn](Canvas.md#method-canvasredraw), or [cleared](Canvas.md#method-canvasclear) and then [drawn](Canvas.md#method-canvasdraw) again, the HTML will be redisplayed inside the print canvas, and the specified callback will be fired again.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| HTML | [String](#type-string) | false | — | HTML to show in this print canvas |
| callback | [PrintCanvasCallback](#type-printcanvascallback) | false | — | callback function to fire when the HTML is displayed. The callback will be passed a pointer to this print canvas as the first parameter with the name `printPreview`. If this canvas is not drawn when this method is called, the callback will not be fired until the canvas is drawn and the HTML rendered out into the page. |

---
## Method: PrintCanvas.print

### Description
Show the native print dialog and allow the user to print the current HTML for this printCanvas. Note that the PrintCanvas must be drawn to be printed.

---
