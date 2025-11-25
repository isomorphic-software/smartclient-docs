# TourWindow Documentation

[← Back to API Index](../main.md)

---

## Class: TourWindow

*Inherits from:* [Window](Window.md#class-window)

### Description
A specific purpose Window class for showing individual steps in a tour.

---
## Attr: TourWindow.contentComponents

### Description
Additional content components to show below [TourWindow.contents](#attr-tourwindowcontents) or [TourWindow.title](#attr-tourwindowtitle) if there are no other content.

**Flags**: IR

---
## Attr: TourWindow.showCancelButton

### Description
If true, show a cancel button below the contents which calls [TourWindow.cancelClick](#method-tourwindowcancelclick) when clicked.

### Groups

- appearance

**Flags**: IR

---
## Attr: TourWindow.actionButton

### Description
Button show below contents that will call [TourWindow.actionClick](#method-tourwindowactionclick) when clicked.

**Flags**: R

---
## Attr: TourWindow.actionButtonTitle

### Description
Title for the [TourWindow.actionButton](#attr-tourwindowactionbutton), shown if [TourWindow.showActionButton](#attr-tourwindowshowactionbutton) is true.

### Groups

- appearance

**Flags**: IR

---
## Attr: TourWindow.cancelButton

### Description
Button show below contents that will call [TourWindow.cancelClick](#method-tourwindowcancelclick) when clicked.

**Flags**: R

---
## Attr: TourWindow.contents

### Description
Text to show in body of window.

### Groups

- appearance
- i18nMessages

**Flags**: IR

---
## Attr: TourWindow.title

### Description
Title for this Window, shown if [showTitle](Window.md#attr-windowshowtitle) is true.

### Groups

- appearance
- i18nMessages

**Flags**: IR

---
## Attr: TourWindow.showProgressPercentInline

### Description
Show progress percent over the progress bar instead of next to it when [TourWindow.showProgress](#attr-tourwindowshowprogress) is enabled?

**Flags**: IR

---
## Attr: TourWindow.showProgressPercent

### Description
Show progress percent next to progress bar when [TourWindow.showProgress](#attr-tourwindowshowprogress) is enabled? The percent can also be shown over the progress bar by setting [TourWindow.showProgressPercentInline](#attr-tourwindowshowprogresspercentinline).

### See Also

- [TourWindow.showProgressPercentInline](#attr-tourwindowshowprogresspercentinline)

**Flags**: IR

---
## Attr: TourWindow.showProgress

### Description
Should a progress bar be shown to indicate progress through the tour?

**Flags**: IR

---
## Attr: TourWindow.cancelButtonPrompt

### Description
Prompt displayed in hover for cancel button.

### Groups

- appearance

**Flags**: IR

---
## Attr: TourWindow.actionButtonURL

### Description
URL to open in another tab or window when the the [TourWindow.actionButton](#attr-tourwindowactionbutton) is clicked. The normal [TourWindow.actionClick](#method-tourwindowactionclick) event is still called.

**Flags**: IR

---
## Attr: TourWindow.cancelButtonDisabled

### Description
Should cancel button be disabled?

### Groups

- appearance

**Flags**: IR

---
## Attr: TourWindow.showActionButton

### Description
If true, show an action button below the contents which calls [TourWindow.actionClick](#method-tourwindowactionclick) when clicked.

### Groups

- appearance

**Flags**: IR

---
## Attr: TourWindow.cancelButtonTitle

### Description
Title for the [TourWindow.cancelButton](#attr-tourwindowcancelbutton), shown if [TourWindow.showCancelButton](#attr-tourwindowshowcancelbutton) is true.

### Groups

- appearance

**Flags**: IR

---
## Method: TourWindow.cancelClick

### Description
Handles a click on the cancel button of this window. The default implementation calls [close()](Window.md#method-windowclose) and returns false to prevent bubbling of the click event.

Override this method if you want other actions to be taken. Custom implementations may call `close()` to trigger the default behavior.

### Returns

`[Boolean](#type-boolean)` — Return false to cancel bubbling the click event

### Groups

- buttons

---
## Method: TourWindow.actionClick

### Description
Handles a click on the action button of this window. No default implementation.

Implement this method to act on this event.

### Returns

`[Boolean](#type-boolean)` — Return false to cancel bubbling the click event

### Groups

- buttons

---
