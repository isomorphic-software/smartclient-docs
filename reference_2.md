# SmartClient API Reference (12.1) (Part 2 of 2)

[← Back to Part 1](reference.md)

---

## Type: AutoComplete

### Description
AutoComplete behavior for [FormItems](classes/FormItem.md#class-formitem).

### Values

| Value | Description |
|-------|-------------|
| "none" | Disable browser autoComplete. Note that some browsers will disregard this setting and still perform native autoComplete for certain items - typically only for log in / password forms. See the discussion [here](classes/FormItem.md#attr-formitemautocomplete). |
| "native" | Allow native browser autoComplete. |

### Groups

- autoComplete

---
## Type: AutoFitIconFieldType

### Description
How should fields of [type:"icon"](#type-listgridfieldtype) be sized by default?

### Values

| Value | Description |
|-------|-------------|
| "none" | Apply no special sizing to icon fields - treat them like any other field in the grid |
| "iconWidth" | size the field to accommodate the width of the icon |
| "title" | size the field to accommodate the title (or the width of the icon if it exceeds the width of the title. |

### Groups

- autoFitFields

---
## Type: AutoScrollDataApproach

### Description
What should drive the automatic expansion of the chart?

### Values

| Value | Description |
|-------|-------------|
| "labels" | Expand the chart to make room for data label facet value. Unused in Bar-type charts |
| "clusters" | Expand the chart to accommodate [FacetChart.barMargin](classes/FacetChart.md#attr-facetchartbarmargin), [FacetChart.minBarThickness](classes/FacetChart.md#attr-facetchartminbarthickness), and [FacetChart.getMinClusterSize](classes/FacetChart.md#method-facetchartgetminclustersize). |
| "both" | Expand the chart to make room for both labels and clusters (whichever requires more space). |

---
## Type: Axis

### Description
An axis or "side" of a table.

### Values

| Value | Description |
|-------|-------------|
| "row" | Row axis |
| "column" | Column axis |

---
## Type: CSSColor

### Description
CSS color specification applied to a specific HTML element on this page.

This is a string matching the syntax as specified in CSS1, and can be formatted in one of the following ways:

*   A keyword color, “white”
*   Six-digit hex notation, “#ffffff”
*   Three-digit hex notation, “#fff”
*   8-bit decimal notation, “rgb(255, 255, 255)”
*   Percentage notation, “rgb(100%, 100%, 100%)”

Note that when working with [FacetChart](classes/FacetChart.md#class-facetchart)s, it's required that colors be specified using the six-digit hex format listed above, rather than any of the others, since the Framework needs to perform math on the subfields. Affected properties include [FacetChart.dataColors](classes/FacetChart.md#attr-facetchartdatacolors), and affected methods include overrides of [FacetChart.getDataColor](classes/FacetChart.md#method-facetchartgetdatacolor) and [FacetChart.getDataLineColor](classes/FacetChart.md#method-facetchartgetdatalinecolor).

### Groups

- appearance

---
## Type: DeviceMode

### Description
Possible layout modes for UI components that are sensitive to the device type being used (a.k.a. "responsive design"). See for example [SplitPane.deviceMode](classes/SplitPane.md#attr-splitpanedevicemode).

### Values

| Value | Description |
|-------|-------------|
| "handset" | mode intended for handset-size devices (phones). Generally only one UI panel will be shown at a time. |
| "tablet" | mode intended for tablet-size devices. Generally, up to two panels are shown side by side in "landscape" [PageOrientation](#type-pageorientation), and only one panel is shown in "portrait" orientation. |
| "desktop" | mode intended for desktop browsers. Three or more panels may be shown simultaneously. |

---
## Type: DialogButtons

### Description
Default buttons that you can use in your Dialogs.

Refer to these buttons via the syntax `isc.Dialog.OK` when passing them into [Dialog.buttons](classes/Dialog.md#attr-dialogbuttons) or into the `properties` argument of helper methods such as [isc.say](classes/isc.md#staticmethod-iscsay).

All buttons added via `setButtons` will fire the [buttonClick event](classes/Dialog.md#method-dialogbuttonclick) (whether they are built-in or custom buttons). Built-in buttons automatically close a Dialog, with the exception of the "Apply" button.

### Values

| Value | Description |
|-------|-------------|
| OK | Dismisses dialog by calling [Dialog.okClick](classes/Dialog.md#method-dialogokclick). Title derived from [Dialog.OK_BUTTON_TITLE](classes/Dialog.md#classattr-dialogok_button_title). |
| APPLY | Does not dismiss dialog. Calls [Dialog.applyClick](classes/Dialog.md#method-dialogapplyclick) Title derived from [Dialog.APPLY_BUTTON_TITLE](classes/Dialog.md#classattr-dialogapply_button_title). |
| YES | Dismisses dialog by calling [Dialog.yesClick](classes/Dialog.md#method-dialogyesclick). Title derived from [Dialog.YES_BUTTON_TITLE](classes/Dialog.md#classattr-dialogyes_button_title). |
| NO | Dismisses dialog by calling [Dialog.noClick](classes/Dialog.md#method-dialognoclick). Title derived from [Dialog.NO_BUTTON_TITLE](classes/Dialog.md#classattr-dialogno_button_title). |
| CANCEL | Dismisses dialog by calling [Dialog.cancelClick](classes/Dialog.md#method-dialogcancelclick). Title derived from [Dialog.CANCEL_BUTTON_TITLE](classes/Dialog.md#classattr-dialogcancel_button_title). |
| DONE | Dismisses dialog by calling [Dialog.doneClick](classes/Dialog.md#method-dialogdoneclick). Title derived from [Dialog.DONE_BUTTON_TITLE](classes/Dialog.md#classattr-dialogdone_button_title). |

---
## Type: DragAppearance

### Description
Different types of effects for showing dragging behavior.

### Values

| Value | Description |
|-------|-------------|
| "none" | No default drag appearance is indicated. Your custom dragging routines should implement some behavior that indicates that the user is in a dragging situation, and where the mouse is. |
| "tracker" | A "drag tracker" object is automatically shown and moved around with the mouse. This is generally set to an icon that represents what is being dragged. The default tracker is a 10 pixel black square, but you can customize this icon. This dragAppearance is not recommended for use with drag resizing or drag moving. |
| "target" | The target object is actually moved, resized, etc. in real time. This is recommended for drag repositioning, but not for drag resizing of complex objects. |
| "outline" | An outline the size of the target object is moved, resized, etc. with the mouse. This is recommended for drag resizing, especially for objects that take a significant amount of time to draw. |

### Groups

- dragdrop

---
## Type: DragIntersectStyle

### Description
Different styles of determining intersection: with mouse or entire rect of target

### Values

| Value | Description |
|-------|-------------|
| "mouse" | Look for drop targets that are under the current mouse cursor position. |
| "rect" | Look for drop targets by intersection of the entire rect of the drag target with the droppable target. |

### Groups

- dragdrop

---
## Type: EdgeName

### Description
An edge or corner of a rectange, or it's center. Used in APIs such as [Canvas.resizeFrom](classes/Canvas.md#attr-canvasresizefrom) and [Canvas.getEventEdge](classes/Canvas.md#classmethod-canvasgeteventedge).

### Values

| Value | Description |
|-------|-------------|
| "T" | top edge |
| "B" | bottom edge |
| "L" | left edge |
| "R" | right edge |
| "TL" | top-left corner |
| "TR" | top-right corner |
| "BL" | bottom-left corner |
| "BR" | bottom-right corner |
| "C" | center |

---
## Type: FieldAuditMode

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "always" | the field value will be saved for all audited adds and updates, regardless of whether it's changed or present in the update |
| "change" | the field value will be saved for all audited adds, and for updates in which the value changed |
| "never" | the field value will never be saved for any DataSource audit operation |

---
## Type: FireStyle

### Description
Flags to set automatic removal of events from the page event registry.

### Values

| Value | Description |
|-------|-------------|
| null | Call the registered handler any time the event occurs |
| Page.FIRE_ONCE | Call the registered handler the first time the event occurs, then unregister the handler as though [Page.clearEvent](classes/Page.md#classmethod-pageclearevent) had been called |

### Groups

- EventRegistry

### See Also

- [Page.setEvent](classes/Page.md#classmethod-pagesetevent)

---
## Type: FiscalYearMode

### Description
Strategies for calculating the FiscalYear within a [FiscalCalendar](#object-fiscalcalendar) from the specified [FiscalCalendar.defaultDate](classes/FiscalCalendar.md#attr-fiscalcalendardefaultdate) and [FiscalCalendar.defaultMonth](classes/FiscalCalendar.md#attr-fiscalcalendardefaultmonth) If the specified fiscal year date starts in one calendar year and ends in the next.

### Values

| Value | Description |
|-------|-------------|
| "end" | The fiscalYear value for the date range will match the calendar year in which the period ends. For example if the defaultDate and defaultMonth were set to represent April 1st, the fiscal year starting on April 1st 2020 would end on April 1st 2021. Setting the fiscalYearMode to `end` would mean the fiscalYear value for this block would be 2021. |
| "start" | The fiscalYear value for the date range will match the calendar year in which the period starts. For example if the defaultDate and defaultMonth were set to represent April 1st, the fiscal year starting on April 1st 2020 would end on April 1st 2021. Setting the fiscalYearMode to `start` would mean the fiscalYear value for this block would be 2020. |

---
## Type: ForceTextApproach

### Description
Approach to force a text value to be interpreted as text rather than parsed as a date, time or other structured types, as can happen with Microsoft Excel. For background information, see [excelPasting](kb_topics/excelPasting.md#kb-topic-copy-and-paste-with-excel).

### Values

| Value | Description |
|-------|-------------|
| "leadingSpace" | a leading space character is added |
| "formula" | text value is turned into a trivial Excel formula (eg "car" becomes ="car"). In Excel, this renders just the value "car" but editing the cell reveals the formula. |

---
## Type: FormattingContext

### Description
The context for which a data-value is being formatted.

### Values

| Value | Description |
|-------|-------------|
| static | for static display in the chart body |
| hover | for transient display in a hover |

---
## Type: FormItemType

### Description
DynamicForms automatically choose the FormItem type for a field based on the `type` property of the field. The table below describes the default FormItem chosen for various values of the `type` property.

You can also set [field.editorType](classes/FormItem.md#attr-formitemeditortype) to the classname of a [FormItem](classes/FormItem.md#class-formitem) to override this default mapping. You can alternatively override [DynamicForm.getEditorType](classes/DynamicForm.md#method-dynamicformgeteditortype) to create a form with different rules for which FormItems are chosen.

### Values

| Value | Description |
|-------|-------------|
| "text" | Rendered as a [TextItem](classes/TextItem.md#class-textitem), unless the length of the field (as specified by [DataSourceField.length](classes/DataSourceField.md#attr-datasourcefieldlength) attribute) is larger than the value specified by [DynamicForm.longTextEditorThreshold](classes/DynamicForm.md#attr-dynamicformlongtexteditorthreshold), a [TextAreaItem](classes/TextAreaItem.md#class-textareaitem) is shown. |
| "boolean" | Rendered as a [CheckboxItem](classes/CheckboxItem.md#class-checkboxitem) |
| "integer" | Rendered as an [IntegerItem](#class-integeritem), a trivial subclass of [TextItem](classes/TextItem.md#class-textitem), by default. Consider setting editorType:[SpinnerItem](classes/SpinnerItem.md#class-spinneritem). |
| "float" | Rendered as a [FloatItem](#class-floatitem), a trivial subclass of [TextItem](classes/TextItem.md#class-textitem), by default. Consider setting editorType:[SpinnerItem](classes/SpinnerItem.md#class-spinneritem). |
| "date" | Rendered as a [DateItem](classes/DateItem.md#class-dateitem) |
| "time" | Rendered as a [TimeItem](classes/TimeItem.md#class-timeitem) |
| "datetime" | Rendered as a [DateTimeItem](classes/DateTimeItem.md#class-datetimeitem) |
| "enum" | Rendered as a [SelectItem](classes/SelectItem.md#class-selectitem). Also true for any field that specifies a [FormItem.valueMap](classes/FormItem.md#attr-formitemvaluemap). Consider setting editorType:[ComboBoxItem](classes/ComboBoxItem.md#class-comboboxitem). |
| "sequence" | Same as `text` |
| "link" | If [DataSourceField.canEdit](classes/DataSourceField.md#attr-datasourcefieldcanedit)`:false` is set on the field, the value is rendered as a [LinkItem](classes/LinkItem.md#class-linkitem). Otherwise the field is rendered as a [TextItem](classes/TextItem.md#class-textitem). |
| "image" | If the field is editable, rendered as a [TextItem](classes/TextItem.md#class-textitem) to edit the URL or partial URL  
If [non editable](classes/FormItem.md#attr-formitemcanedit), and [readOnlyDisplay](classes/DynamicForm.md#attr-dynamicformreadonlydisplay) is "static", an image will be rendered out, deriving the URL from the field value combined with [FormItem.imageURLPrefix](classes/FormItem.md#attr-formitemimageurlprefix) and [FormItem.imageURLSuffix](classes/FormItem.md#attr-formitemimageurlsuffix) if present. This behavior may be suppressed via [DynamicForm.showImageAsURL](classes/DynamicForm.md#attr-dynamicformshowimageasurl), in which case the value (URL or partial URL) will be rendered out as static text. |
| "imageFile" | Rendered as a [FileItem](classes/FileItem.md#class-fileitem), or a [ViewFileItem](#class-viewfileitem) if not editable |
| "binary" | Rendered as a [FileItem](classes/FileItem.md#class-fileitem), or a [ViewFileItem](#class-viewfileitem) if not editable |

### See Also

- [FormItem.type](classes/FormItem.md#attr-formitemtype)
- [FieldType](#type-fieldtype)

---
## Type: GroupTreeChangeType

### Description
Type of change to the [ListGrid.groupTree](classes/ListGrid_1.md#attr-listgridgrouptree).

### Values

| Value | Description |
|-------|-------------|
| ListGrid.GROUP_BY | [ListGrid.groupBy](classes/ListGrid_2.md#method-listgridgroupby) responsible (grouping fields changed) |
| ListGrid.REGROUP | [ListGrid.regroup](classes/ListGrid_2.md#method-listgridregroup) responsible (grid already grouped) |
| ListGrid.INCREMENTAL | incremental regroup of a single record |

### See Also

- [ListGrid.groupTreeChanged](classes/ListGrid_2.md#method-listgridgrouptreechanged)

---
## Type: Integer

### Description
A whole number, for example, 5. Decimal numbers, for example 5.5, are not allowed. Null is allowed.

### See Also

- [int](#type-int)
- [PositiveInteger](#type-positiveinteger)

---
## Type: LabelCollapseMode

### Description
Strategy to apply when there is too little room for labels to be shown for all data points with comfortable padding ([FacetChart.minLabelGap](classes/FacetChart.md#attr-facetchartminlabelgap)).

### Values

| Value | Description |
|-------|-------------|
| "none" | Show all labels regardless, even though they will overlap |
| "time" | Show significant time values such as the first day of the month or week. Data values in Records must be true Date objects, not Strings. |
| "numeric" | Pick round numbers in the range and show labels for just those numbers. Best for continuous datasets that are not time-based |
| "sample" | Pick periodic values from the dataset and show labels for those. Best when the there are no particular points that would clearly be the best to label |

---
## Type: LineBreakStyle

### Description
The style of line-breaks to use when exporting data

### Values

| Value | Description |
|-------|-------------|
| "default" | Use the default line-break style of the server OS |
| "unix" | Use UNIX-style line-breaks (LF only) |
| "mac" | Use MAC-style line-breaks (CR only) |
| "dos" | Use DOS-style line-breaks (both CR & LF) |

---
## Type: MockDataFormat

### Description
Specifies the format of the mock data.

### Values

| Value | Description |
|-------|-------------|
| "mock" | Mock data in "balsamiq" format |
| "csv" | Mock data in CSV format |
| "xml" | Mock data in XML format |
| "json" | Mock data in JSON format |

---
## Type: MockDataType

### Description
Whether the mock data is for a flat grid-like dataset or for a tree. If "grid" is specified, text shortcuts that would cause a hierarchy to be created (such as starting a line with "\[+\]") will not have special meaning and be considered to be just a normal data value.

### Values

| Value | Description |
|-------|-------------|
| "grid" | Mock data for a ListGrid |
| "tree" | Mock data for a TreeGrid |

---
## Type: MultipleFieldStorage

### Description
Options for how values are stored for a field that is [multiple:true](classes/ListGridField.md#attr-listgridfieldmultiple). See [DataSourceField.multipleStorage](classes/DataSourceField.md#attr-datasourcefieldmultiplestorage).

### Values

| Value | Description |
|-------|-------------|
| "simpleString" | values are saved as a simple delimeter-separated string. Delimeter can be configured via [DataSourceField.multipleStorageSeparator](classes/DataSourceField.md#attr-datasourcefieldmultiplestorageseparator). An empty array is stored as "", and null as the database `null` value. |
| "json" | values are serialized to JSON. Empty array as a distinct value from null (it appears as the text "\[\]"). |
| "none" | no transformation is applied to values; server-side field value remains a Java List when passed to the execute(Fetch|Add|Update|Remove) method of the server-side DataSource class |

### Groups

- multipleField

---
## Type: NavigationMethod

### Description
Method of, or reason for, navigation between panes.

### Values

| Value | Description |
|-------|-------------|
| "backClick" | a "back" [NavigationButton](classes/NavigationButton.md#class-navigationbutton) has been clicked |
| "sideClick" | a side panel [NavigationButton](classes/NavigationButton.md#class-navigationbutton) has been clicked |
| "programmatic" | application code called [setCurrentPane()](classes/SplitPane.md#method-splitpanesetcurrentpane), [showNavigationPane()](classes/SplitPane.md#method-splitpaneshownavigationpane), [showListPane()](classes/SplitPane.md#method-splitpaneshowlistpane), [showDetailPane()](classes/SplitPane.md#method-splitpaneshowdetailpane), etc. |
| "navigatePane" | application code directly called [navigatePane()](classes/SplitPane.md#method-splitpanenavigatepane) |
| "selectionChanged" | a seletion change automatically called [navigatePane()](classes/SplitPane.md#method-splitpanenavigatepane) |
| "historyCallback" | browser navigation triggered [SplitPane](classes/SplitPane.md#class-splitpane) navigation |

---
## Type: Object

### Description
An ordinary JavaScript as obtained by "new Object()" or via [Object Literal](#type-objectliteral) syntax.

Methods that return Objects or take Objects as parameters make use of the ability of a JavaScript Object to contain an arbitrary set of named properties, without requiring declaration in advance. This capability makes it possible to use a JavaScript Object much like a HashMap in Java or .NET, but without the need to call get() or set() to create and retrieve properties.

For example if you created an Object using [Object Literal](#type-objectliteral) syntax like so:

```
    var request = {
        actionURL : "/foo.do",
        showPrompt:false
    };
 
```
You could then access it's properties like so:
```
    var myActionURL = request.actionURL;
    var myShowPrompt = request.showPrompt;
 
```
.. and you could assign new values to those properties like so:
```
    request.actionURL = "newActionURL";
    request.showPrompt = newShowPromptSetting;
 
```
Note that while JavaScript allows you to get and set properties in this way on any Object, SmartClient components require that if a setter or getter exists, it must be called, or no action will occur. For example, if you had a [ListGrid](classes/ListGrid_1.md#class-listgrid) and you wanted to change the [showHeader](classes/ListGrid_1.md#attr-listgridshowheader) property:
```
     myListGrid.setShowHeader(false); // correct
     myListGrid.showHeader = false; // incorrect (nothing happens)
 
```
All documented attributes have [flags](#kb-topic-flag-abbreviations) (eg IRW) that indicate when direct property access is allowed or not.

---
## Type: RecordLayout

### Description
Controls the style of TableView record display

### Values

| Value | Description |
|-------|-------------|
| TableView.TITLE_ONLY | Show [title field](classes/TableView.md#attr-tableviewtitlefield) only |
| TableView.TITLE_DESCRIPTION | Show [title](classes/TableView.md#attr-tableviewtitlefield) and [description](classes/TableView.md#attr-tableviewdescriptionfield) fields only |
| TableView.SUMMARY_INFO | Show [title](classes/TableView.md#attr-tableviewtitlefield), [description](classes/TableView.md#attr-tableviewdescriptionfield) and [info](classes/TableView.md#attr-tableviewinfofield) fields only |
| TableView.SUMMARY_DATA | Show [title](classes/TableView.md#attr-tableviewtitlefield), [description](classes/TableView.md#attr-tableviewdescriptionfield) and [data](classes/TableView.md#attr-tableviewdatafield) fields only |
| TableView.SUMMARY_FULL | Show [title](classes/TableView.md#attr-tableviewtitlefield), [description](classes/TableView.md#attr-tableviewdescriptionfield), [info](classes/TableView.md#attr-tableviewinfofield) and [data](classes/TableView.md#attr-tableviewdatafield) fields similar to the iPhoneOS Mail application |

---
## Type: RelativeDateString

### Description
A string of known format used to specify a datetime offset. For example, a RelativeDateString that represents "one year from today" is written as `"+1y"`.

RelativeDateStrings are comprised of the following parts:

*   direction: the direction in which the quantity applies - one of + or -
*   quantity: the number of units of time to apply - a number
*   timeUnit: an abbreviated timeUnit to use - one of ms/MS (millisecond), s/S (second), mn/MN (minute), h/H (hour), d/D (day), w/W (week), m/M (month), q/Q (quarter, 3-months), y/Y (year), dc/DC (decade) or c/C (century).  
    The timeUnit is case sensitive. A lowercase timeUnit implies an exact offset, so `+1d` refers to the current date / time increased by exactly 24 hours. If the timeUnit is uppercase, it refers to the start or end boundary of the period of time in question, so `+1D` would refer to the end of the day (23:39:59:999) tomorrow, and `-1D` would refer to the start of the day (00:00:00:000) yesterday.
*   \[qualifier\]: an optional timeUnit encapsulated in square-brackets and used to offset the calculation - eg. if +1d is "plus one day", +1d\[W\] is "plus one day from the end of the current week". You may also specify another complete RelativeDateString as the \[qualifier\], which offers more control - eg, +1d\[+1W\] indicates "plus one day from the end of NEXT week".

This format is very flexible. Here are a few example relative date strings:  
`+0D`: End of today. There are often multiple ways to represent the same time using this system - for example this could also be written as `-1ms[+1D]`  
`-0D`: Beginning of today.  
`+1W`: End of next week.  
`+1w[-0W]`: Beginning of next week.  
`+1w[-0D]`: Beginning of the current day of next week.

### See Also

- [RelativeDateShortcut](#type-relativedateshortcut)

---
## Type: ResizeKnobPoint

### Description
Specifies the position of a resize knob with respect to its draw item.

### Values

| Value | Description |
|-------|-------------|
| "TL" | Top Left corner |
| "TR" | Top Right corner |
| "BL" | Bottom Left corner |
| "BR" | Bottom Right corner |
| "T" | Centered on the top edge |
| "B" | Centered on the bottom edge |
| "R" | Centered on the left edge |
| "L" | Centered on thie right edge |

---
## Type: RPCTransport

### Description
SmartClient supports multiple RPC transports for maximum compatibility and feature richness. All of transports use HTTP as the underlying protocol, but use different mechanisms for sending the HTTP request and processing the response. The transport is typically auto-selected for by based on the feature being used and the current browser settings. For advanced use cases, [RPCRequest.transport](classes/RPCRequest.md#attr-rpcrequesttransport) and [RPCManager.defaultTransport](classes/RPCManager.md#classattr-rpcmanagerdefaulttransport) are exposed as override points.

### Values

| Value | Description |
|-------|-------------|
| "xmlHttpRequest" | Uses the XMLHttpRequest object to make the request to the server. Note that in some browsers with certain configurations, this transport may not be available. See [platformDependencies](kb_topics/platformDependencies.md#kb-topic-platform-dependencies) for more information. This transport is not useful with file uploads. Cannot be used to target cross-domain URLs directly. |
| "scriptInclude" | Write a SCRIPT tag into the DOM with a SRC attribute that targets an arbitrary URL. This transport is the only one that allows direct cross-domain URL access.

For [RPCRequest.callback](classes/RPCRequest.md#attr-rpcrequestcallback) to work, the server being contacted must support the ability to generate JavaScript code in the response that will call a JavaScript function generated by SmartClient. SmartClient passes the name of the function to call via a URL parameter, which can be controlled with [RPCRequest.callbackParam](classes/RPCRequest.md#attr-rpcrequestcallbackparam). This callback mechanism is sometimes called the "JSONP" (JSON with Padding) approach. |
| "hiddenFrame" | Available with SmartClient Server only. An HTML form is dynamically assembled that targets a hidden IFRAME. This mechanism is supported on all browsers and cannot be disabled by end users.

If using the SmartClient Server and using [Server-side data integration](kb_topics/serverDataIntegration.md#kb-topic-server-datasource-integration), the "hiddenFrame" transport is automatically used for all RPCManager and DataSource requests if the "xmlHttpRequest" transport is not available.

Cannot be used to target cross-domain URLs directly. |

---
## Type: SCImgURL

### Description
Properties that refer to images by URL, such as [Img.src](classes/Img.md#attr-imgsrc) and [Button.icon](classes/Button.md#attr-buttonicon), are specially interpreted in SmartClient to allow for simpler and more uniform image URLs, and to allow applications to be restructured more easily.

**the application image directory**

When specifying URLs to image files via SmartClient component properties such as [StretchImg.src](classes/StretchImg.md#attr-stretchimgsrc), any relative path is assumed to be relative to the "application image directory" (`appImgDir`). The application image directory can be set via [Page.setAppImgDir](classes/Page.md#classmethod-pagesetappimgdir), and defaults to "images/", representing the typical practice of placing images in a subdirectory relative to the URL at which the application is accessed.

For applications that may be launched from multiple URLs, the `appImgDir` can be set to the correct relative path to the image directory by calling [Page.setAppImgDir](classes/Page.md#classmethod-pagesetappimgdir) before any SmartClient components are created. This enables applications or components of an application to be launched from multiple locations, or to be relocated, without changing any image URLs supplied to SmartClient components.

**the "\[SKIN\]" URL prefix**

The special prefix "\[SKIN\]" can be used to refer to images within the skin folder whenever image URLs are supplied to SmartClient components.

The value of "\[SKIN\]" is the combination of:

*   the "skin directory", established in `load_skin.js` via [Page.setSkinDir](classes/Page.md#classmethod-pagesetskindir), plus..
*   the setting for [skinImgDir](classes/Canvas.md#attr-canvasskinimgdir) on the component where you set an image URL property

`skinImgDir` defaults to "images/", so creating an [Img](classes/Img.md#class-img) component with [Img.src](classes/Img.md#attr-imgsrc) set to "\[SKIN\]myButton/button.gif" will expand to `Page.getSkinDir() + "/images/myButton/button.gif"`.

Some components that use a large number of images use `skinImgDir` to group them together and make it possible to relocate all the media for the component with a single setting. For example, the [TreeGrid](classes/TreeGrid.md#class-treegrid) class sets `skinImgDir` to "images/TreeGrid/". This allows [TreeGrid.folderIcon](classes/TreeGrid.md#attr-treegridfoldericon) to be set to just "\[SKIN\]folder.gif" but refer to `Page.getSkinDir() + "/images/TreeGrid/folder.gif"`.

A custom subclass of TreeGrid can set `skinImgDir` to a different path, such as "/images/MyTreeGrid", to source all media from a different location.

TIPS:

*   subcomponents may not share the parent component's setting for skinImgDir. For example, the [Window.minimizeButton](classes/Window.md#attr-windowminimizebutton) has the default setting for "skinImgDir" ("images/"), so the [src](classes/Img.md#attr-imgsrc) property used with this component is set to "\[SKIN\]/Window/minimize.png" (in the "SmartClient" sample skin).
*   for a particular image, the skinImgDir setting on the component may not be convenient. The prefix "\[SKINIMG\]" can be used to refer to `Page.getSkinDir() + "/images"` regardless of the setting for `skinImgDir`

**Stateful image URLs**

Many image URLs in SmartClient are "stateful", meaning that the actual URL used to fetch an image will vary according to the component's state (eg, "Disabled"), generally, by adding a suffix to the image URL. See the [Skinning Overview](kb_topics/skinning.md#kb-topic-skinning--theming) for more information on statefulness and the [Img.src](classes/Img.md#attr-imgsrc) documentation for information on how stateful image URLs are formed.

**SVG Images**

If the URL represents an SVG image, you may specify `tag` as a query param to control whether it's rendered in an object or image tag, provided [Canvas.useImageForSVG](classes/Canvas.md#attr-canvasuseimageforsvg) isn't set. If that query param is present and has any value other than `object`, then the SVG image will be rendered in an image tag. Otherwise, it will be rendered in an object tag. For example, an `SCImgURL` of "circle.svg?tag=image" will render in an image tag.

---
## Type: SelectedAppearance

### Description
Appearance when a component is in [edit mode](classes/Canvas.md#method-canvasseteditmode) and is selected.

Modes such as "tintMask" or "outlineMask" create an ["edit mask"](classes/EditProxy.md#attr-editproxyeditmask) that is layered over the selected component, and blocks all normal interaction with the component, so that behaviors like [EditProxy.supportsInlineEdit](classes/EditProxy.md#attr-editproxysupportsinlineedit) can completely take the place of the component's normal interactivity.

"outlineEdges" mode allows normal interaction with the component, which allows the end user to do things like [freeze ListGrid fields](classes/ListGrid_1.md#attr-listgridcanfreezefields), which the [GridEditProxy](classes/GridEditProxy.md#class-grideditproxy) can implement as a ${isc.DocUtils.linkForRef('attr:GridEditProxy.saveFieldFrozenState','persistent change to grid\\'s configuration')}.

### Values

| Value | Description |
|-------|-------------|
| "tintMask" | editMask on top of the component is updated with [EditProxy.selectedTintColor](classes/EditProxy.md#attr-editproxyselectedtintcolor) and [EditProxy.selectedTintOpacity](classes/EditProxy.md#attr-editproxyselectedtintopacity) |
| "outlineMask" | editMask on top of the component is updated with [EditProxy.selectedBorder](classes/EditProxy.md#attr-editproxyselectedborder) |
| "outlineEdges" | MultiAutoChild is created on top of the component. This constructs a border around the component using 4 separate `outlineEdge` components so that interactivity is not blocked. |
| "none" | no change in appearance. Override [EditProxy.showSelectedAppearance](classes/EditProxy.md#method-editproxyshowselectedappearance) to create a custom appearance. |

---
## Type: SnapGridStyle

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "crosses" | show array of crosses to indicate snap points |
| "lines" | show grid of lines to indicate snap points |

---
## Type: SortArrow

### Description
Do we display an arrow for the sorted field ?

### Values

| Value | Description |
|-------|-------------|
| "none" | Don't show a sort arrow at all. |
| "corner" | Display sort arrow in the upper-right corner (above the scrollbar) only. |
| "field" | Display sort arrow above each field header only. |
| "both" | Display sort arrow above each field header AND in corner above scrollbar.BOTH:"both", // NOTE: Canvas establishes this constant |

### Groups

- sorting
- appearance

---
## Type: TreeGridViewState

### Description
An object containing the "view state" information for a treeGrid. In addition to the state data contained by a [ListGridViewState](#type-listgridviewstate) object, this will also contain the current open state of the treeGrid in question.  
Note that this object is not intended to be interrogated directly, but may be stored (for example) as a blob on the server for view state persistence across sessions.

### Groups

- viewState

---
## Type: ZoomStartPosition

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "start" | start at the beginning of the range |
| "end" | start at the end of the range |

---
## Object: DetailViewerRecord

### Description
A DetailViewerRecord is an object literal with properties that define the values for the various fields of a [DetailViewer](classes/DetailViewer.md#class-detailviewer).

For example a DetailViewer that defines the following fields:

```
 fields : [
     {name: "field1"},
     {name: "field2"}
 ],
 
```
Might have the following data:
```
 data : [
     {field1: "foo", field2: "bar"},
     {field1: "field1 value", field2: "field2 value"}
 ]
 
```
Each element in the data array above is an instance of DetailViewerRecord - notice that these are specified simply as object literals with properties.

---
## Object: FileLoader

### Description
This class enables background (deferred) loading and caching of JS, CSS and Image files. It is designed to work standalone from the rest of the SmartClient framework to provide a lightweight caching and loading mechanism for SmartClient modules as well as user-built application modules/fragments.

The most common usage scenarios are:

*   Caching JS, CSS, Image files in the browser in anticipation of a transition to a page that requires these files. For example, a plain HTML (non-SmartClient) login page or landing page can begin caching SmartClient in the background while allowing the user to login, or giving the user something to read. Normally, loading SmartClient or other large JavaScript files would block page loading and display. By loading SmartClient in the background only after a simple HTML landing page has loaded, you can completely eliminate perceived download time associated with loading a rich UI application, making a much larger difference in user experience than any difference in framework/application size.
*   Loading a multi-phase UI. In this scenario, an initial rendering of a page is done with minimal data transfer to the browser. Then JS, CSS, and Image files are fetched in the background to provide richer UI components. During this time the user can continue to normally interact with the initial page. Once loading is complete, the UI is updated with richer components.

The recommended usage pattern is to use the `loadISC` custom tag provided as part of the SmartClient SDK. You can specify `cacheOnly="true"` to loadISC to cache the SmartClient framework in the background or alternately `defer="true"` to load the SmartClient framework and make it available in the current page. You can specify the `onload` attribute of the tag to provide a JavaScript callback to your code that will be called when the framework loading is complete.

If you're not working in a JSP environment, you can use the [FileLoader.cacheISC](classes/FileLoader.md#staticmethod-fileloadercacheisc)/[FileLoader.loadISC](classes/FileLoader.md#staticmethod-fileloaderloadisc) APIs to accomplish the same effect as the `loadISC` JSP tag.

Additional APIs are provided for performing dynamic caching and loading of other JS, CSS, and Image files to improve the performance of your application. See below.

**You must set `window.isomorphicDir` before loading and using this module unless the default of '../isomorphic/' is acceptable. E.g. if your html file is in your toplevel webroot directory, then your HTML file should say (note the trailing slash):**

```
 <SCRIPT>window.isomorphicDir='isomorphic/'</SCRIPT>
 <SCRIPT SRC=isomorphic/system/modules/ISC_FileLoader.js></SCRIPT>
 
```
In addition, **if you are using Smart GWT**, you must set [modulesDir](classes/FileLoader.md#classattr-fileloadermodulesdir) to "modules/", as follows:
```
   isc.FileLoader.modulesDir = "modules/";
 
```
This module is usable independent of the rest of SmartClient - you can use it on pages that don't load any other modules. In practice, the general pattern is to use this module on static HTML pages such as a login page to pre-cache SmartClient modules, application logic, skin files, and css so that once the user logs in, there's no latency to load the rich UI.

You can also load the FileLoader itself dynamically - see [FileLoader.ensureLoaded](classes/FileLoader.md#staticmethod-fileloaderensureloaded)

Note: You can also reference this class via the alias isc.FL

---
## Object: FormItemIcon

### Description
Form item icon descriptor objects used by Form Items to specify the appearance and behavior of icons displayed after the item in the page flow.

### Groups

- formIcons

### See Also

- [FormItem.icons](classes/FormItem.md#attr-formitemicons)

---
## Object: GaugeSector

### Description
Represents a sector on the gauge.

---
## Object: MessageID

### Description
Opaque message identifier for messages shown by the [Notify](classes/Notify.md#class-notify) class

---
## Object: NodeLocator

### Description
An object containing sufficient context to unambiguously identify a single node in the tree. For normal trees, the node itself - or its ID - is sufficient for this purpose, but for [multi-link trees](classes/Tree.md#method-treeismultilinktree), we also need to know the node's parent, and its position within that parent. For cases where we need to propagate change back up the node's parent chain, in order to maintain a given parent node's openList, the node, parent and position are not enough context; for those cases, we need either the node's position in the tree's openList, or a full path to the node. `NodeLocator` objects contain this extra context, and can be passed to APIs such as [Tree.openFolder](classes/Tree.md#method-treeopenfolder), which would ordinarily accept a parameter of type [TreeNode](#object-treenode).

---
## Object: Operator

### Description
Specification of an operator for use in filtering, for example "equals". Use with [DataSource.addSearchOperator](classes/DataSource.md#method-datasourceaddsearchoperator) to define custom filtering behaviors for client-side filtering.

### Groups

- advancedFilter

---
## Object: PaletteNode

### Description
An object representing a component which the user may create dynamically within an application.

A PaletteNode expresses visual properties for how the palette will display it (eg [title](classes/PaletteNode.md#attr-palettenodetitle), [icon](classes/PaletteNode.md#attr-palettenodeicon)) as well as instructions for creating the component the paletteNode represents ([PaletteNode.type](classes/PaletteNode.md#attr-palettenodetype), [PaletteNode.defaults](classes/PaletteNode.md#attr-palettenodedefaults)).

Various types of palettes ([ListPalette](#class-listpalette), [TreePalette](#class-treepalette), [MenuPalette](#class-menupalette), [TilePalette](#class-tilepalette)) render a PaletteNode in different ways, and allow the user to trigger creation in different ways (eg drag and drop, or just click). All share a common pattern for how components are created from palettes.

Note that in a TreePalette, a PaletteNode is essentially a [TreeNode](#object-treenode) and can have properties expected for a TreeNode (eg, [showDropIcon](classes/TreeGrid.md#attr-treegridcustomicondropproperty)). Likewise a PaletteNode in a MenuPalette can have the properties of a [MenuItem](#object-menuitem), such as [MenuItem.enableIf](classes/MenuItem.md#method-menuitemenableif).

---
## Object: ServerObject

### Description
The ServerObject tells the ISC server how to find or create a server-side object involved in [DMI](kb_topics/dmiOverview.md#kb-topic-direct-method-invocation) (Direct Method Invocation).

A ServerObject declaration appears in the XML definition of a [DataSource](classes/DataSource.md#class-datasource) (for responding to [DSRequest](#object-dsrequest)s) or in an Application configuration file (.app.xml) for responding to [RPCRequest](#object-rpcrequest)s.

NOTE: Please take note of the points made in [this discussion](kb_topics/serverDataSourceImplementation.md#kb-topic-notes-on-server-side-datasource-implementations) of caching and thread-safety issues in server-side DataSources.

### See Also

- [DMI](classes/DMI.md#class-dmi)

---
## Object: Tab

### Description
Tabs are specified as objects, not class instances. For example, when developing in JavaScript, a typical initialization block for a TabSet would look like this:
```
 TabSet.create({
     tabs: [
         {title: "tab1", pane: "pane1"},
         {title: "tab2"}
     ]
 });
 
```
And in XML:
```
 <TabSet>
    <tabs>
        <Tab title="tab1" pane="pane1"/>
        <Tab title="tab2"/>
    </tabs>
 </TabSet>
 
```

---
## Object: TaskDecision

### Description
Identifies a potential decision (branch) within a [DecisionGateway](classes/DecisionGateway.md#class-decisiongateway). Each decision has a criteria and a target ProcessElement ID.

---
## Object: TileRecord

### Description
A TileRecord is a JavaScript Object whose properties contain values for each TileField. A TileRecord may have additional properties which affect the record's appearance or behavior, or which hold data for use by custom logic or other, related components.

---
## Object: UserSummary

### Description
An object representing a user-created and user-modifiable summary, which can be created and edited with a [SummaryBuilder](classes/SummaryBuilder.md#class-summarybuilder) either directly or via the [ListGrid.canAddSummaryFields](classes/ListGrid_1.md#attr-listgridcanaddsummaryfields) behavior.

---
