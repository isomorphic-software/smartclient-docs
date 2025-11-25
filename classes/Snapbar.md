# Snapbar Documentation

[← Back to API Index](../main.md)

---

## Class: Snapbar

*Inherits from:* [Splitbar](Splitbar.md#class-splitbar)

### Description
Subclass of the [Splitbar](Splitbar.md#class-splitbar) class that uses the `grip` functionality to show a stateful open / close indicator.

### See Also

- [Splitbar](Splitbar.md#class-splitbar)
- [Layout](Layout.md#class-layout)

---
## Attr: Snapbar.showDown

### Description
Snapbars show mouse-down styling.

**Flags**: IRW

---
## Attr: Snapbar.showRollOver

### Description
Snapbars show rollover styling.

**Flags**: IRW

---
## Attr: Snapbar.showClosedGrip

### Description
If [Splitbar.showGrip](Splitbar.md#attr-splitbarshowgrip) is true, this property determines whether the grip image displayed should show the `"Closed"` state when the [Splitbar.target](Splitbar.md#attr-splitbartarget) is hidden. Note that if [Splitbar.invertClosedGripIfTargetAfter](Splitbar.md#attr-splitbarinvertclosedgripiftargetafter) is true, we may show the "closed" state when the target is visible, rather than when it is hidden.

### Groups

- grip

**Flags**: IRA

---
## Attr: Snapbar.gripImgSuffix

### Description
Overridden from [Splitbar.gripImgSuffix](Splitbar.md#attr-splitbargripimgsuffix) to simplify providing custom grip media for this widget.

**Flags**: IRA

---
## Attr: Snapbar.showGrip

### Description
Should we show a "grip" image floating above the center of this widget?

### Groups

- grip

**Flags**: IRW

---
## Attr: Snapbar.showRollOverGrip

### Description
If [StretchImg.showGrip](StretchImg.md#attr-stretchimgshowgrip) is true, this property determines whether to show the 'Over' state on the grip image when the user rolls over on this widget. Has no effect if [StatefulCanvas.showRollOver](StatefulCanvas.md#attr-statefulcanvasshowrollover) is false.

### Groups

- grip

**Flags**: IRA

---
## Attr: Snapbar.showDownGrip

### Description
If [StretchImg.showGrip](StretchImg.md#attr-stretchimgshowgrip) is true, this property determines whether to show the 'Down' state on the grip image when the user mousedown's on this widget. Has no effect if [StatefulCanvas.showDown](StatefulCanvas.md#attr-statefulcanvasshowdown) is false.

### Groups

- grip

**Flags**: IRW

---
