# ReportScreen Documentation

[← Back to API Index](../reference.md)

---

## Class: ReportScreen

### Description
The deployable frame around a [DataReport](DataReport.md#class-datareport): a VLayout stacking a report-level [ReportToolbar](ReportToolbar.md#class-reporttoolbar) (an autoChild, like a Window's header) above the DataReport body. This is the composite ReportBuilder authors and that a deployment renders like any other screen. Because the toolbar is an autoChild and [EditProxy.allowNestedDrops](EditProxy.md#attr-editproxyallownesteddrops) is false, Reify treats the ReportScreen as fixed chrome + a single editable content area (the DataReport) -- a viewer/author cannot drop components between the toolbar and the report.

---
## Attr: ReportScreen.slicerBarEmptyMessageStyle

### Description
CSS style applied to [ReportScreen.slicerBarEmptyMessage](#attr-reportscreenslicerbaremptymessage). Defaults to the same style the report body uses for its own empty-state guidance, so the two read as one family rather than two unrelated greys.

**Flags**: IRW

---
## Attr: ReportScreen.destroyReportOnReplace

### Description
Whether the report body should be [destroyed](Canvas_1.md#method-canvasdestroy) when it is replaced by a different body, or unlinked by `setDataReport(null)`, rather than just removed from the frame. Defaults to false so a caller that supplied its own [ReportScreen.dataReport](#attr-reportscreendatareport) keeps ownership of it and can re-use it elsewhere.

This property has no effect on a body created via the autoChild pattern, using [ReportScreen.dataReportProperties](#attr-reportscreendatareportproperties) / [ReportScreen.dataReportDefaults](#reportscreendatareportdefaults): a ReportScreen that built its own body owns it, and always destroys it on replacement, regardless of this property's value.

Note that once a DataReport has been destroyed it cannot be re-used elsewhere within an application.

**Flags**: IRW

---
## Attr: ReportScreen.showSlicerBar

### Description
Whether the report's filter bar is shown between the [ReportToolbar](ReportToolbar.md#class-reporttoolbar) and the report body. The bar holds the report's [DataReport.slicers](DataReport.md#attr-datareportslicers); with this false they are not shown, though a hidden slicer's criteria still reach the report.

**Flags**: IR

---
## Attr: ReportScreen.showSlicerReset

### Description
Whether the filter bar offers a control returning its slicers to the selections the report's author saved. See [ReportScreen.resetSlicers](#method-reportscreenresetslicers).

**Flags**: IR

---
## Attr: ReportScreen.slicerFlow

### Description
The wrapping row of slicers inside [ReportScreen.slicerBar](#attr-reportscreenslicerbar).

**Flags**: R

---
## Attr: ReportScreen.dataReport

### Description
The report body -- the [DataReport](DataReport.md#class-datareport) whose portlets make up the report. May be supplied as a live DataReport instance; otherwise, if [ReportScreen.dataReportProperties](#attr-reportscreendatareportproperties) is set, one is built as the `dataReport` autoChild (the standalone pattern, mirroring [CanvasItem.canvas](CanvasItem.md#attr-canvasitemcanvas) / [CanvasItem.canvasProperties](CanvasItem.md#attr-canvasitemcanvasproperties)). In an editing context (Reify / ReportBuilder) or a loaded screen the body instead arrives as a child component and is found via [ReportScreen.getDataReport](#method-reportscreengetdatareport).

**Flags**: IR

---
## Attr: ReportScreen.slicerBarEmptyMessage

### Description
Text shown across an empty filter bar, naming what the region is for. An empty bar is otherwise indistinguishable from blank space.

**Flags**: IRW

---
## Attr: ReportScreen.slicerResetButton

### Description
Control that returns the filter bar's slicers to the author's saved selections. Centered beneath the slicers, in a fixed place of its own, so it does not move as slicers are added or removed.

**Flags**: R

---
## Attr: ReportScreen.dataReportConstructor

### Description
Class used to build the [ReportScreen.dataReport](#attr-reportscreendatareport) autoChild.

**Flags**: IR

---
## Attr: ReportScreen.slicerBar

### Description
The report's filter bar, holding the [DataReport.slicers](DataReport.md#attr-datareportslicers) of the report body in [ReportScreen.slicerFlow](#attr-reportscreenslicerflow) plus the reset control beneath them.

**Flags**: R

---
## Attr: ReportScreen.dataReportProperties

### Description
Properties for the auto-created [ReportScreen.dataReport](#attr-reportscreendatareport) body. Setting this, when no live [ReportScreen.dataReport](#attr-reportscreendatareport) is supplied, makes the ReportScreen build its own DataReport body as an autoChild. Leave null in an editing / loaded-screen context, where the body is supplied as a child component.

**Flags**: IR

---
## Method: ReportScreen.setDataReport

### Description
Link a [DataReport](DataReport.md#class-datareport) as the report body: records it as [ReportScreen.dataReport](#attr-reportscreendatareport) and adds it as a member (below the toolbar). This is the way a DataReport is attached to a ReportScreen -- an explicit [DataReport](DataReport.md#class-datareport) or [ReportScreen.dataReportProperties](#attr-reportscreendatareportproperties) at init calls it, a standalone caller calls it directly, and framework-driven adds (a ReportBuilder editNode, or a serialized child on screen load) are funnelled through it, so linkage is always established one way.

A frame holds exactly one body, so passing a different DataReport replaces the current one and passing null unlinks it. In both cases the outgoing body is removed from the frame, and destroyed if [ReportScreen.destroyReportOnReplace](#attr-reportscreendestroyreportonreplace) is set (or if the frame built it itself). Passing the body that is already linked is a no-op.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataReport | [DataReport](#type-datareport) | false | — | the report body, or null to unlink the current one |

### Returns

`[DataReport](#type-datareport)` — the linked report body, or null

---
## Method: ReportScreen.getDataReport

### Description
The linked report body, or null. See [ReportScreen.setDataReport](#method-reportscreensetdatareport).

### Returns

`[DataReport](#type-datareport)` — the report body, or null

---
## Method: ReportScreen.refreshSlicerBar

### Description
Rebuild the filter bar from the report body's [DataReport.slicers](DataReport.md#attr-datareportslicers). Called when the frame is created and whenever the report's slicers change.

---
## Method: ReportScreen.resetSlicers

### Description
Return the report's filter-bar slicers to the selections its author saved, discarding the current reader's choices.

A slicer the author marked hidden is left alone: its selection is the author's constraint rather than the reader's, and the reader has no control for it.

---
