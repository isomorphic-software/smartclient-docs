# SplitPane Documentation

[← Back to API Index](../reference.md)

---

## Class: SplitPane

*Inherits from:* [Layout](Layout.md#class-layout)

### Description
A device- and orientation-sensitive layout that implements the common pattern of rendering two panes side-by-side on desktop machines and on tablets in landscape orientation, while switching to showing a single pane for handset-sized devices or tablets in portrait orientation (this type of behavior is sometimes called "responsive design").

A `SplitPane` can manage either two or three panes — a [navigationPane](#attr-splitpanenavigationpane) and the [detailPane](#attr-splitpanedetailpane) are required, and a [listPane](#attr-splitpanelistpane) can also be provided which appears in the same place as the navigation pane, with built-in navigation between the panes based on [NavigationBar](NavigationBar.md#class-navigationbar). An example of 3-pane usage would be an email application:

*   `navigationPane`: [TreeGrid](TreeGrid.md#class-treegrid) of folders
*   `listPane`: [ListGrid](ListGrid_1.md#class-listgrid) showing messages in a folder
*   `detailPane`: message detail view (perhaps a [DetailViewer](DetailViewer.md#class-detailviewer) over an [HTMLFlow](HTMLFlow.md#class-htmlflow) or similar arrangement)

The placement of the panes is by default sensitive to whether the device is detected as a handset (phone), tablet or desktop device (see [DeviceMode](../reference.md#type-devicemode)) and to the current [PageOrientation](../reference.md#type-pageorientation). You can also configure a `SplitPane` with a fixed [SplitPane.pageOrientation](#attr-splitpanepageorientation) or [SplitPane.deviceMode](#attr-splitpanedevicemode).

Beyond providing the panes listed above, typical usage is simply to call [showListPane()](#method-splitpaneshowlistpane) and [showDetailPane()](#method-splitpaneshowdetailpane) when the `SplitPane` should navigate to a new pane. For example, in an email application, clicking on a folder in the `navigationPane` should cause the `listPane` to show messages from the folder, then `showListPane(_"folder name"_)` would be called to show the `listPane` and give it a new title reflecting the name of the folder.

Similarly, clicking on a message in the `listPane` should show the message details in the `detailPane` and call `showDetailPane(_"message title"_)` to reveal the `detailPane` and give it an appropriate title.

#### Auto-Navigation

By default, SplitPane will analyze the controls placed in each pane and the DataSources they are bound to, and automatically navigate between panes.

For example, in a two-pane SplitPane with a ListGrid in the navigationPane and a DynamicForm in the detailPane, both with the same DataSource, when a record is selected in the grid, [DynamicForm.editRecord](DynamicForm.md#method-dynamicformeditrecord) will be called to populate the form, and the detailPane will be shown.

In a 3-pane SplitPane with a TreeGrid and ListGrid in the navigationPane and listPane respectively, if there is a 1-to-Many relation from the TreeGrid's DataSource to the ListGrid's DataSource, [ListGrid.fetchRelatedData](ListGrid_2.md#method-listgridfetchrelateddata) will be used to load related records when tree nodes are clicked, and the listPane will be shown.

For a full description of auto-navigation, see [SplitPane.autoNavigate](#attr-splitpaneautonavigate). Just set `autoNavigate` to false if you don't want these behaviors.

#### Automatic control placement

[SplitPane.detailToolButtons](#attr-splitpanedetailtoolbuttons) allows you to define a set of controls that are specially placed based on the `deviceMode` and `pageOrientation`. See [SplitPane.detailToolButtons](#attr-splitpanedetailtoolbuttons) for details.

#### NavigationBar and ToolStrips

By default, bars are created as follows:

*   in `deviceMode:"tablet"` and `deviceMode` "handset", the [SplitPane.navigationBar](#attr-splitpanenavigationbar) is always created.
*   in `deviceMode:"desktop"`, the `navigationBar` is created by default only if the [SplitPane.navigationTitle](#attr-splitpanenavigationtitle) is specified and non-empty or [SplitPane.showRightButton](#attr-splitpaneshowrightbutton) and/or [SplitPane.showLeftButton](#attr-splitpaneshowleftbutton) is `true`, or [SplitPane.showNavigationBar](#attr-splitpaneshownavigationbar) is `true`.
*   in `deviceMode:"desktop"` and `deviceMode` "tablet", the [SplitPane.detailToolStrip](#attr-splitpanedetailtoolstrip) is shown _above_ the `detailPane`.
*   in `deviceMode:"handset"`, the [SplitPane.detailToolStrip](#attr-splitpanedetailtoolstrip) is created **only** if `detailToolButtons` are specified, and is placed _underneath_ the `detailPane`.
*   [SplitPane.listToolStrip](#attr-splitpanelisttoolstrip) - separate bar for the `listPane`, only present for `deviceMode:"desktop"` when a `listPane` is provided.

All of these bars are [AutoChildren](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) and hence completely optional. You can omit them entirely, or, if you want navigation bars or tool strips but want to customize them more than the AutoChild system allows, you can prevent the built-in bars from being created and place your own [NavigationBar](NavigationBar.md#class-navigationbar)s either _inside_ your navigation, list or detail panes, or _outside_ the `SplitPane` as a whole. This allows you to completely customize your navigation but still use `SplitPane` to handle device- and orientation-aware layout. See [SplitPane.showNavigationBar](#attr-splitpaneshownavigationbar), [SplitPane.showListToolStrip](#attr-splitpaneshowlisttoolstrip), and [SplitPane.showDetailToolStrip](#attr-splitpaneshowdetailtoolstrip).

Note that in addition to the [navigationBar](#attr-splitpanenavigationbar), the other automatically created bars are also instances of [NavigationBar](NavigationBar.md#class-navigationbar) despite the "toolStrip" naming convention. These controls will not generally contain navigation elements; the `NavigationBar` class is used for consistent styling, since the `navigationBar` appears adjacent to the toolstrips in some modes and orientations, so they should have the same height and styling.

---
## Attr: SplitPane.detailToolStrip

### Description
Toolstrip servicing the [detailPane](#attr-splitpanedetailpane).

In [deviceMode](#attr-splitpanedevicemode) "desktop" and `deviceMode` "tablet", the `detailToolStrip` is shown _above_ the `detailPane`. In [deviceMode](#attr-splitpanedevicemode) "handset", the `detailToolStrip` is created **only** if [detailToolButtons](#attr-splitpanedetailtoolbuttons) are specified, and is placed _underneath_ the `detailPane`.

**Flags**: IR

---
## Attr: SplitPane.navigationPane

### Description
An arbitrary widget that is visible in all configurations when the [currentPane](#attr-splitpanecurrentpane) is "navigation" (it may also be visible when the `currentPane` is "list" or "detail").

The `navigationPane` is typically used for navigation, to initialize the content of the [listPane](#attr-splitpanelistpane) (when using a `listPane`) or the [detailPane](#attr-splitpanedetailpane). For example, in an email application the `navigationPane` pane widget could be a [TreeGrid](TreeGrid.md#class-treegrid) of the inboxes and folders.

**Flags**: IRW

---
## Attr: SplitPane.showMiniNav

### Description
If true, a [MiniNavControl](../reference.md#class-mininavcontrol) will be shown:

*   In the [navigationBar](#attr-splitpanenavigationbar) when the device mode is "handset" and the [currentPane](#attr-splitpanecurrentpane) is "detail".
*   In the [detailToolStrip](#attr-splitpanedetailtoolstrip) when the device mode is "tablet" and the [pageOrientation](#attr-splitpanepageorientation) is "portrait".

### See Also

- [SplitPane.detailNavigationControl](#attr-splitpanedetailnavigationcontrol)

**Flags**: IR

---
## Attr: SplitPane.detailNavigationControl

### Description
Navigation control that appears only when the navigation pane is not showing (showing detail pane on handset, or portrait mode on tablet).

See also [SplitPane.showMiniNav](#attr-splitpaneshowmininav) for a way to enable a built-in control.

**Flags**: IRWA

---
## Attr: SplitPane.showLeftButton

### Description
Should the [SplitPane.leftButton](#attr-splitpaneleftbutton) be shown in the [navigation bar](#attr-splitpanenavigationbar)?

When set to true, the [SplitPane.leftButton](#attr-splitpaneleftbutton) is displayed to the left of the [SplitPane.navigationTitle](#attr-splitpanenavigationtitle), and to the right of the [SplitPane.backButton](#attr-splitpanebackbutton), when [SplitPane.deviceMode](#attr-splitpanedevicemode) is not "desktop".

### See Also

- [SplitPane.leftButton](#attr-splitpaneleftbutton)
- [SplitPane.backButton](#attr-splitpanebackbutton)

**Flags**: IRW

---
## Attr: SplitPane.notifyAfterNavigationClick

### Description
Whether or not to call [SplitPane.navigationClick](#method-splitpanenavigationclick), if present, after navigation has already occurred. This may be set to provide backcompat with legacy code, as by default the Framework will call [SplitPane.navigationClick](#method-splitpanenavigationclick) before navigation to allow cancelation.

Note that if this property is set, [SplitPane.navigationClick](#method-splitpanenavigationclick) cannot be canceled.

### See Also

- [SplitPane.paneChanged](#method-splitpanepanechanged)
- [SplitPane.navigationClick](#method-splitpanenavigationclick)

**Flags**: IRW

---
## Attr: SplitPane.showResizeBars

### Description
If enabled, the `SplitPane` will add resize bars between the [navigationPane](#attr-splitpanenavigationpane) and [detailPane](#attr-splitpanedetailpane) when these panes are shown side-by-side, and between the [listPane](#attr-splitpanelistpane) and [detailPane](#attr-splitpanedetailpane) in [deviceMode:"desktop"](#attr-splitpanedevicemode).

**Flags**: IR

---
## Attr: SplitPane.detailToolButtons

### Description
`detailToolButtons` allows you to specify a set of controls that are specially placed based on the [deviceMode](#attr-splitpanedevicemode) and [pageOrientation](#attr-splitpanepageorientation). This is generally useful for a compact strip of [ImgButton](ImgButton.md#class-imgbutton) controls, approximately 5 of which will fit comfortably using typically-sized icons and in the most space-constricted modes.

These controls are placed as follows:

*   in `deviceMode:"desktop"` and `deviceMode` "tablet" with `pageOrientation` "landscape", `detailToolButtons` appear in the [SplitPane.detailToolStrip](#attr-splitpanedetailtoolstrip) shown _above_ of the `detailPane`.
*   in `deviceMode:"handset"`, `detailToolButtons` appear in a [SplitPane.detailToolStrip](#attr-splitpanedetailtoolstrip) _underneath_ the detailPane. This toolstrip is only created in "handset" mode if `detailToolButtons` are provided.
*   in `deviceMode:"tablet"` and `pageOrientation:"portrait"`, `detailToolButtons` appear in `splitPane.navigationBar`.

**Flags**: IRW

---
## Attr: SplitPane.navigationBar

### Description
A `NavigationBar` instance managed by this `SplitPane` that is placed above the [navigationPane](#attr-splitpanenavigationpane).

The following [passthroughs](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) apply:

*   [animateNavigationBarStateChanges](#attr-splitpaneanimatenavigationbarstatechanges) for [NavigationBar.animateStateChanges](NavigationBar.md#attr-navigationbaranimatestatechanges)
*   [showRightButton](#attr-splitpaneshowrightbutton) for [NavigationBar.showRightButton](NavigationBar.md#attr-navigationbarshowrightbutton)

Note that in [deviceMode](#attr-splitpanedevicemode) "desktop" with [showNavigationBar](#attr-splitpaneshownavigationbar) unset, the `navigationBar` is automatically hidden when it would be empty ([navigationTitle](#attr-splitpanenavigationtitle) is an empty string and `showRightButton` and `showLeftButton` are both `false`). The `navigationBar` will be shown if the `navigationTitle` [is set](#method-splitpanesetnavigationtitle) to a non-empty string, or `showRightButton` or `showLeftButton` is set to `true`.

### See Also

- [SplitPane.showNavigationBar](#attr-splitpaneshownavigationbar)

**Flags**: IR

---
## Attr: SplitPane.detailPane

### Description
The right-hand of the two panes managed by this widget, used for viewing details.

**Flags**: IRW

---
## Attr: SplitPane.animateNavigationBarStateChanges

### Description
Whether to animate state changes of the [navigationBar](#attr-splitpanenavigationbar). Enabled by default except when the browser is known to have poor animation performance.

### See Also

- [NavigationBar.animateStateChanges](NavigationBar.md#attr-navigationbaranimatestatechanges)

**Flags**: IR

---
## Attr: SplitPane.pageOrientation

### Description
Current [PageOrientation](../reference.md#type-pageorientation). The default behavior of the `SplitPane` is to register for orientation change notifications from the device (see [Page.getOrientation](Page.md#classmethod-pagegetorientation)) and automatically change orientation based on the [type of device](#attr-splitpanedevicemode).

You can instead set a specific value for `pageOrientation` if you only want to use a specific layout, and not respond to orientation information from the device.

**Flags**: IRW

---
## Attr: SplitPane.detailTitle

### Description
The title for the [detailPane](#attr-splitpanedetailpane).

**Flags**: IRW

---
## Attr: SplitPane.listPane

### Description
An optional list pane displayed in the left-hand of the panes or in a side panel according to the pane layout.

**Flags**: IRW

---
## Attr: SplitPane.detailPaneTitleTemplate

### Description
Default value chosen for [detailPaneTitle](#method-splitpanesetdetailtitle) when [SplitPane.navigateDetailPane](#method-splitpanenavigatedetailpane) is called.

Available variables are the same as for [SplitPane.listPaneTitleTemplate](#attr-splitpanelistpanetitletemplate).

### Groups

- i18nMessages

### See Also

- [SplitPane.listPaneTitleTemplate](#attr-splitpanelistpanetitletemplate)

**Flags**: IRW

---
## Attr: SplitPane.listTitle

### Description
The title for the [listPane](#attr-splitpanelistpane).

**Flags**: IRW

---
## Attr: SplitPane.listPaneTitleTemplate

### Description
Default value chosen for [listPaneTitle](#method-splitpanesetlisttitle) when [SplitPane.navigateListPane](#method-splitpanenavigatelistpane) is called.

Available variables are:

*   "titleField" - the value of the [DataSource.titleField](DataSource.md#attr-datasourcetitlefield) in the selected record from the [SplitPane.navigationPane](#attr-splitpanenavigationpane)
*   "index" - position of the selected record
*   "totalRows" - total number of rows in the component where the record is selected
*   "record" - the entire selected Record

### Groups

- i18nMessages

### See Also

- [SplitPane.detailPaneTitleTemplate](#attr-splitpanedetailpanetitletemplate)

**Flags**: IRW

---
## Attr: SplitPane.currentPane

### Description
The most recently shown pane. In handset [DeviceMode](../reference.md#type-devicemode), the `currentPane` is the only pane that is actually visible to the user. In other modes more than one pane can be simultaneously visible, so the `currentPane` is the most recent pane that was brought into view via a call to [SplitPane.setCurrentPane](#method-splitpanesetcurrentpane) or [SplitPane.showNavigationPane](#method-splitpaneshownavigationpane).

The default value of `currentPane` is "navigation".

**Flags**: IRW

---
## Attr: SplitPane.navigationTitle

### Description
The title for the [navigationPane](#attr-splitpanenavigationpane), displayed in the [navigationBar](#attr-splitpanenavigationbar) and also used for the title of a back button in some configurations.

**Flags**: IRW

---
## Attr: SplitPane.showDetailToolStrip

### Description
If set to `false`, the [detailToolStrip](#attr-splitpanedetailtoolstrip) will not be shown. Otherwise, the [SplitPane.detailToolStrip](#attr-splitpanedetailtoolstrip) will be shown if either the [deviceMode](#attr-splitpanedevicemode) is not "handset" or [SplitPane.detailToolButtons](#attr-splitpanedetailtoolbuttons) are specified.

**Flags**: IRW

---
## Attr: SplitPane.addHistoryEntries

### Description
Should default history-tracking support be enabled? If `true`, then a history management scheme utilizing [History.addHistoryEntry](History.md#staticmethod-historyaddhistoryentry) and [History.registerCallback](History.md#staticmethod-historyregistercallback) is enabled. The history callback is registered as an additive callback, allowing other history callbacks including the primary callback to be registered.

The default history management scheme is as follows:

*   History entries are only added after [page load](Page.md#classmethod-pageisloaded) and when the `SplitPane` is drawn.
*   A history entry is added for a pane that is hidden by [SplitPane.showNavigationPane](#method-splitpaneshownavigationpane), [SplitPane.showListPane](#method-splitpaneshowlistpane), or [SplitPane.showDetailPane](#method-splitpaneshowdetailpane) for the current [deviceMode](#attr-splitpanedevicemode) and [pageOrientation](#attr-splitpanepageorientation) settings.
    
    Example 1: When `deviceMode` is "desktop", all 3 panes are shown simultaneously, so no history entries are added.
    
    Example 2: When `deviceMode` is "handset", calling [SplitPane.showDetailPane](#method-splitpaneshowdetailpane) will hide the current pane (the [SplitPane.listPane](#attr-splitpanelistpane) if present, otherwise the [SplitPane.navigationPane](#attr-splitpanenavigationpane)). A history entry is added for the pane that was hidden
    

The default history management scheme can be supplemented with application-specific history management. For example, when `deviceMode` is "tablet", the [SplitPane.detailPane](#attr-splitpanedetailpane) is always visible, but changes to the content of the `detailPane` are transparent to the `SplitPane`. The application can add history entries of its own when the user causes new information to be displayed in the `detailPane`.

**Flags**: IRW

---
## Attr: SplitPane.leftButton

### Description
An additional [NavigationButton](NavigationButton.md#class-navigationbutton) which may be shown to the left of the [title](#attr-splitpanenavigationtitle) in the [navigation bar](#attr-splitpanenavigationbar).

**Important note:** by default, this button has no [direction](NavigationButton.md#attr-navigationbuttondirection) and does not fire the [navigationClick](#method-splitpanenavigationclick) notification. You can provide a `direction` and apply a click handler via the autoChild system.

### See Also

- [SplitPane.showLeftButton](#attr-splitpaneshowleftbutton)
- [SplitPane.backButton](#attr-splitpanebackbutton)

**Flags**: IR

---
## Attr: SplitPane.reverseOrder

### Description
**Note**: This is a Layout property which is inapplicable on this class. A SplitPane always works from left to right.

### Groups

- layoutPolicy

**Flags**: IRW

---
## Attr: SplitPane.showRightButton

### Description
Should the [rightButton](NavigationBar.md#attr-navigationbarrightbutton) be shown in the [navigationBar](#attr-splitpanenavigationbar)?

**Flags**: IRW

---
## Attr: SplitPane.listToolStrip

### Description
Bar displayed above the [listPane](#attr-splitpanelistpane), if a `listPane` is present, **only** for [deviceMode](#attr-splitpanedevicemode) "desktop".

**Flags**: IR

---
## Attr: SplitPane.navigationPaneWidth

### Description
Sets a size for the navigation pane.

This size is active only on platforms where multiple panes are showing at once; if a single pane is showing, `navigationPaneWidth` is ignored.

Note that setting a `navigationPaneWidth` which creates more size in one of the panes may backfire on mobile, where all panes end up having the same width (the device width). If you make one pane larger to accommodate more controls or content, make sure you use techniques such as showing fewer columns on mobile, or using adaptive components such as [AdaptiveMenu](AdaptiveMenu.md#class-adaptivemenu).

If you simply want side-by-side display with arbitrary proportions, and don't care about tablet and mobile adaptation, use [HLayout](../reference.md#class-hlayout) instead.

### See Also

- [Canvas.width](Canvas.md#attr-canvaswidth)

**Flags**: IRW

---
## Attr: SplitPane.backButton

### Description
A [NavigationButton](NavigationButton.md#class-navigationbutton) shown to the left of the [title](#attr-splitpanenavigationtitle) in the [navigationBar](#attr-splitpanenavigationbar).

In [deviceModes](#attr-splitpanedevicemode) other than "desktop", this button is automatically created and allows transitioning back to the [navigationPane](#attr-splitpanenavigationpane) (in tablet and handset modes) or the [listPane](#attr-splitpanelistpane) (in handset mode). In these [deviceModes](#attr-splitpanedevicemode), setting [showLeftButton](#attr-splitpaneshowleftbutton) to true shows the [leftButton](#attr-splitpaneleftbutton) _in addition to_ the automatically-created back button.

When [deviceMode](#attr-splitpanedevicemode) is "desktop", this button is never shown. See [showLeftButton](#attr-splitpaneshowleftbutton) for more information.

This button's [title](Button.md#attr-buttontitle) is determined automatically by the `SplitPane`. See [listTitle](#attr-splitpanelisttitle) and [detailTitle](#attr-splitpanedetailtitle).

**Flags**: IR

---
## Attr: SplitPane.showListToolStrip

### Description
If set to `false`, the [listToolStrip](#attr-splitpanelisttoolstrip) will not be shown. Otherwise, the [SplitPane.listToolStrip](#attr-splitpanelisttoolstrip) will be shown if the [deviceMode](#attr-splitpanedevicemode) is "desktop" and a [SplitPane.listPane](#attr-splitpanelistpane) is provided.

**Flags**: IRW

---
## Attr: SplitPane.vertical

### Description
**Note**: This is a Layout property which is inapplicable on this class.

### Groups

- layoutPolicy

**Flags**: IRW

---
## Attr: SplitPane.deviceMode

### Description
UI layout mode used for this `SplitPane`.

A `SplitPane` can be configured with up to 3 panes: the [SplitPane.navigationPane](#attr-splitpanenavigationpane), [SplitPane.listPane](#attr-splitpanelistpane) and [SplitPane.detailPane](#attr-splitpanedetailpane). Both [DeviceMode](../reference.md#type-devicemode) and [PageOrientation](../reference.md#type-pageorientation) influence the placement of these panes as follows:

*   "handset" `deviceMode`: only a single pane is shown at a time. Not orientation sensitive
*   "tablet" `deviceMode` with `pageOrientation`:"landscape": the `detailPane` is shown side by side with either the `navigationPane` or `listPane`
*   "tablet" `deviceMode` with `pageOrientation`:"portrait": the `detailPane` is shown only. End user navigation that would show the `listPane` or `navigationPane` shows those panes on top of the `detailPane` (temporarily covering part of its content)
*   "desktop" `deviceMode`: all 3 panes are shown simultaneously. Not orientation sensitive

The `listPane` is optional; if not present, wherever the `listPane` is mentioned above, the `navigationPane` is shown instead.

**Flags**: IR

---
## Attr: SplitPane.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: SplitPane.showNavigationBar

### Description
If set to `false`, the [navigationBar](#attr-splitpanenavigationbar) will not be shown. If set to `true`, the `navigationBar` will always be shown, even when the [deviceMode](#attr-splitpanedevicemode) is "desktop"

If this property is unset, the [SplitPane.navigationBar](#attr-splitpanenavigationbar) will be shown if at least one of the following conditions holds:

*   the [deviceMode](#attr-splitpanedevicemode) is not "desktop"
*   the [SplitPane.navigationTitle](#attr-splitpanenavigationtitle) is specified and non-empty
*   [SplitPane.showRightButton](#attr-splitpaneshowrightbutton) and/or [SplitPane.showLeftButton](#attr-splitpaneshowleftbutton) is `true`,

**Flags**: IRW

---
## Attr: SplitPane.autoNavigate

### Description
If set, the `SplitPane` will automatically monitor selection changes in the [SplitPane.navigationPane](#attr-splitpanenavigationpane) and [SplitPane.listPane](#attr-splitpanelistpane), and call [SplitPane.navigateListPane](#method-splitpanenavigatelistpane) or [SplitPane.navigateDetailPane](#method-splitpanenavigatedetailpane) when selections are changed.

If a pane is not a [DataBoundComponent](../reference.md#interface-databoundcomponent), but contains a component (selected via a breadth-first search), then that inner component will be monitored for selection changes instead. In either case, `autoNavigate` does nothing unless the monitored component has a valid [DataSource](DataSource.md#class-datasource) and there is a DataSource relationship declared between panes. Note that for [Layout](Layout.md#class-layout)s, the [members](Layout.md#attr-layoutmembers) will be searched when looking for a component rather than the [children](Canvas.md#attr-canvaschildren).

Auto-navigation occurs after the [recordClick()](ListGrid_2.md#method-listgridrecordclick) or [selectionUpdated()](DataBoundComponent.md#method-databoundcomponentselectionupdated) method is called, so if you implement these methods, your code will run first. Importantly, if your methods call [fetchData()](ListGrid_2.md#method-listgridfetchdata), [setCriteria()](ListGrid_2.md#method-listgridsetcriteria), [DynamicForm.editRecord](DynamicForm.md#method-dynamicformeditrecord) or [DynamicForm.editNewRecord](DynamicForm.md#method-dynamicformeditnewrecord) on the target component, navigation will still occur, but duplicate calls to fetch related data, set data into the target, or start editing the record in the target will be skipped.

The selection of the pane or pane inner component for monitoring is done only when the `SplitPane` is created, and when a new [SplitPane.navigationPane](#attr-splitpanenavigationpane) or [SplitPane.listPane](#attr-splitpanelistpane) is assigned, except when the `SplitPane` is in [edit mode](Canvas.md#method-canvasseteditmode) (e.g. when using [Reify](../kb_topics/reify.md#kb-topic-reify-overview)). where the component redetection logic gets run every time a pane's widget hierarchy changes. Changing the hierarchy under a pane at other times in a way that will affect the breadth-first selection of an inner component may lead to unexpected behavior.

Note that only one inner component under each pane (or the pane itself) will be monitored, even if multiple inner components might satisfy the related-data requirement.

**Flags**: IR

---
## Method: SplitPane.setNavigationTitle

### Description
Sets the title for the [navigationPane](#attr-splitpanenavigationpane).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| title | [HTMLString](../reference.md#type-htmlstring) | false | — | new title for the navigation pane. |

---
## Method: SplitPane.setShowRightButton

### Description
Show or hide the [rightButton](NavigationBar.md#attr-navigationbarrightbutton) of the [navigationBar](#attr-splitpanenavigationbar).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| visible | [boolean](../reference.md#type-boolean) | false | — | if `true`, the button will be shown, otherwise hidden. |

---
## Method: SplitPane.showNavigationPane

### Description
Causes a transition to the [navigationPane](#attr-splitpanenavigationpane).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| direction | [NavigationDirection](../reference.md#type-navigationdirection) | true | — | when [SplitPane.animateNavigationBarStateChanges](#attr-splitpaneanimatenavigationbarstatechanges) is `true`, this is the direction passed to [NavigationBar.setViewState](NavigationBar.md#method-navigationbarsetviewstate). |

---
## Method: SplitPane.setDetailPaneTitleTemplate

### Description
Sets a new [detailPaneTitleTemplate](#attr-splitpanedetailpanetitletemplate) at runtime.

By calling this method it is assumed you want the detail pane title to change to the new template.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| template | [HTMLString](../reference.md#type-htmlstring) | false | — | new template, can use HTML to be styled. |

---
## Method: SplitPane.setPageOrientation

### Description
Explicitly sets the page orientation to a fixed value instead of being responsive to device orientation changes. Pass `null` to return to responding automatically to device orientation.

See [PageOrientation](../reference.md#type-pageorientation) for details of how page orientation affects layout.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newOrientation | [PageOrientation](../reference.md#type-pageorientation) | false | — | new orientation to use. |

---
## Method: SplitPane.downClick

### Description
Notification method fired when the [miniNav is showing](#attr-splitpaneshowmininav) and the down button on the [navigationBar](#attr-splitpanenavigationbar)'s [MiniNavControl](../reference.md#class-mininavcontrol) is clicked.

---
## Method: SplitPane.setShowListToolStrip

### Description
Setter for [SplitPane.showListToolStrip](#attr-splitpaneshowlisttoolstrip). **Note:** If the property is set `false` after the [SplitPane.detailToolStrip](#attr-splitpanedetailtoolstrip) autochild has already been created, it will be hidden but not destroyed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showListToolStrip | [Boolean](#type-boolean) | false | — | new value |

---
## Method: SplitPane.navigateDetailPane

### Description
Calls [SplitPane.navigatePane](#method-splitpanenavigatepane) with the [SplitPane.detailPane](#attr-splitpanedetailpane) as the target pane.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| title | [HTMLString](../reference.md#type-htmlstring) | true | — | optional title to use instead of the automatically chosen one |

---
## Method: SplitPane.showListPane

### Description
Causes a transition to the [listPane](#attr-splitpanelistpane), optionally updating the [list title](#method-splitpanesetlisttitle).

If, based on the [deviceMode](#attr-splitpanedevicemode) and [pageOrientation](#attr-splitpanepageorientation), this causes the [navigationPane](#attr-splitpanenavigationpane) to be hidden, the [back button](#attr-splitpanebackbutton) will be updated with the current title of the `navigationPane`, or the `backButtonTitle` passed to this method. When [SplitPane.addHistoryEntries](#attr-splitpaneaddhistoryentries) is enabled and `backButtonTitle` is passed, then `backButtonTitle` will be used for the back button title if the user goes back to the `listPane`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| listPaneTitle | [HTMLString](../reference.md#type-htmlstring) | true | — | optional new list title. |
| backButtonTitle | [HTMLString](../reference.md#type-htmlstring) | true | — | optional new title for the [back button](#attr-splitpanebackbutton). |
| direction | [NavigationDirection](../reference.md#type-navigationdirection) | true | — | when [SplitPane.animateNavigationBarStateChanges](#attr-splitpaneanimatenavigationbarstatechanges) is `true`, this is the direction passed to [NavigationBar.setViewState](NavigationBar.md#method-navigationbarsetviewstate). |

---
## Method: SplitPane.setListTitle

### Description
Sets the title for the [listPane](#attr-splitpanelistpane).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| title | [HTMLString](../reference.md#type-htmlstring) | false | — | new title for the list pane. |

---
## Method: SplitPane.setDetailPane

### Description
Sets a new [detailPane](#attr-splitpanedetailpane) at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pane | [Canvas](#type-canvas) | false | — | new detail pane for this widget. |

---
## Method: SplitPane.navigationClick

### Description
Notification method fired when the user clicks the default back / forward buttons on the navigation bar for this `SplitPane`.

Note that the return value will be ignored and cancelation won't be possible if [SplitPane.notifyAfterNavigationClick](#attr-splitpanenotifyafternavigationclick) has been set true, since that forces this method to run after we've already navigated to the new pane.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| direction | [NavigationDirection](../reference.md#type-navigationdirection) | false | — | direction in which the user is attempting to navigate. |

### Returns

`[Boolean](#type-boolean)` — false to cancel navigation

---
## Method: SplitPane.setShowNavigationBar

### Description
Setter for [SplitPane.showNavigationBar](#attr-splitpaneshownavigationbar).

**Note:** If the property is set `false` after the [SplitPane.navigationBar](#attr-splitpanenavigationbar) autochild has already been created, it will be hidden but not destroyed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showNavigationBar | [Boolean](#type-boolean) | false | — | new value |

---
## Method: SplitPane.setListPane

### Description
Sets a new [listPane](#attr-splitpanelistpane) at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pane | [Canvas](#type-canvas) | false | — | new list pane for this widget. |

---
## Method: SplitPane.showDetailPane

### Description
Causes a transition to the [detailPane](#attr-splitpanedetailpane), optionally updating the [detail title](#method-splitpanesetdetailtitle).

If, based on the [deviceMode](#attr-splitpanedevicemode) and [pageOrientation](#attr-splitpanepageorientation), this causes the [navigationPane](#attr-splitpanenavigationpane) or [listPane](#attr-splitpanelistpane) to be hidden, the [back button](#attr-splitpanebackbutton) will be updated with the current title of the `navigationPane` or `listPane`, or the `backButtonTitle` passed to this method. When [SplitPane.addHistoryEntries](#attr-splitpaneaddhistoryentries) is enabled and `backButtonTitle` is passed, then `backButtonTitle` will be used for the back button title if the user goes back to the `detailPane`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| detailPaneTitle | [HTMLString](../reference.md#type-htmlstring) | true | — | optional new [detail title](#attr-splitpanedetailtitle). |
| backButtonTitle | [HTMLString](../reference.md#type-htmlstring) | true | — | optional new title for the [back button](#attr-splitpanebackbutton). |
| direction | [NavigationDirection](../reference.md#type-navigationdirection) | true | — | when [SplitPane.animateNavigationBarStateChanges](#attr-splitpaneanimatenavigationbarstatechanges) is `true`, this is the direction passed to [NavigationBar.setViewState](NavigationBar.md#method-navigationbarsetviewstate). |

---
## Method: SplitPane.setNavigationPane

### Description
Update the [navigationPane](#attr-splitpanenavigationpane) at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pane | [Canvas](#type-canvas) | false | — | new navigation pane for this widget. |

---
## Method: SplitPane.upClick

### Description
Notification method fired when the [miniNav is showing](#attr-splitpaneshowmininav) and the up button on the [navigationBar](#attr-splitpanenavigationbar)'s [MiniNavControl](../reference.md#class-mininavcontrol) is clicked.

---
## Method: SplitPane.navigatePane

### Description
Causes the target pane component to load data and update its title based on the current selection in the source pane. Also shows the target pane if it's not already visible.

For the target pane to load data, both the source pane and target pane must be [DataBoundComponent](../reference.md#interface-databoundcomponent)s or contain a component as a descendant widget, and have a [DataSource](DataSource.md#class-datasource), and either:

*   The two DataSources must have a Many-To-One relationship declared via [DataSourceField.foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey), so that [ListGrid.fetchRelatedData](ListGrid_2.md#method-listgridfetchrelateddata) can be used on the target pane. A common example of this would be navigation from a source pane that's a [TreeGrid](TreeGrid.md#class-treegrid) to a [ListGrid](ListGrid_1.md#class-listgrid) target.
*   The two DataSources must be the same, so that the record selected in the source pane can be displayed in the target pane via simply calling [setData()](DetailViewer.md#method-detailviewersetdata). This would apply, for example, if the source pane is a [ListGrid](ListGrid_1.md#class-listgrid) and the target is a [DynamicForm](DynamicForm.md#class-dynamicform), so that [editRecord()](DynamicForm.md#method-dynamicformeditrecord) gets called, or if the target is a [DetailViewer](DetailViewer.md#class-detailviewer).

For purposes of this check, if the pane is not itself a component, we will use the first component we can find in a breath-first search of the hierarchy underneath it, skipping over [search forms](SearchForm.md#class-searchform). If the pane is itself a [search form](SearchForm.md#class-searchform), it will never load related data. Note that one or more records must be selected in the source component for related data to be loaded (which should be automatically true for [auto-navigation](#attr-splitpaneautonavigate)). and only one inner pane component (or the pane itself) will receive the related data, even if multiple inner components meet the requirements.

Even if we can't load related data into the target pane by the above rules, we'll still show the target pane if it's not already visible, except during [auto-navigation](#attr-splitpaneautonavigate).

Defaults:

*   The default `target` is "list" if the [listPane](#attr-splitpanelistpane) is present, otherwise "detail".
*   The title applied to the target pane is based on [SplitPane.listPaneTitleTemplate](#attr-splitpanelistpanetitletemplate) if the target pane is the `listPane`, otherwise [SplitPane.detailPaneTitleTemplate](#attr-splitpanedetailpanetitletemplate).
*   The source pane usually does not need to be specified: if the target pane is the `detailPane`, the default source pane is the `listPane` if present, otherwise the [SplitPane.navigationPane](#attr-splitpanenavigationpane). If the target pane is the `listPane`, the source pane is always the `navigationPane`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| target | [CurrentPane](../reference.md#type-currentpane) | true | — | pane that should navigate |
| title | [HTMLString](../reference.md#type-htmlstring) | true | — | optional title to use for target pane. If not specified, the title is based on [SplitPane.listPaneTitleTemplate](#attr-splitpanelistpanetitletemplate) if the target pane is the `listPane`, otherwise [SplitPane.detailPaneTitleTemplate](#attr-splitpanedetailpanetitletemplate). |
| source | [CurrentPane](../reference.md#type-currentpane) | true | — | source pane used for selection |

---
## Method: SplitPane.setLeftButtonTitle

### Description
Setter for the [leftButtonTitle](NavigationBar.md#attr-navigationbarleftbuttontitle) of the [navigationBar](#attr-splitpanenavigationbar).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newTitle | [HTMLString](../reference.md#type-htmlstring) | false | — | new title for the left button. |

---
## Method: SplitPane.setDetailToolButtons

### Description
Updates the [detailToolButtons](#attr-splitpanedetailtoolbuttons) at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| buttons | [Array of Canvas](#type-array-of-canvas) | false | — | new controls for the toolstrip. |

---
## Method: SplitPane.getPageOrientation

### Description
Returns the current [PageOrientation](../reference.md#type-pageorientation). If [SplitPane.pageOrientation](#attr-splitpanepageorientation) has been set to a non-null value, it is returned; otherwise returns the current device orientation from [Page.getOrientation](Page.md#classmethod-pagegetorientation).

### Returns

`[PageOrientation](../reference.md#type-pageorientation)` — current page orientation

---
## Method: SplitPane.setShowLeftButton

### Description
Show or hide the [leftButton](#attr-splitpaneleftbutton) in the navigation bar.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| show | [boolean](../reference.md#type-boolean) | false | — | if `true`, the `leftButton` will be shown, otherwise hidden. |

---
## Method: SplitPane.setRightButtonTitle

### Description
Setter for the [rightButtonTitle](NavigationBar.md#attr-navigationbarrightbuttontitle) of the [navigationBar](#attr-splitpanenavigationbar).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newTitle | [HTMLString](../reference.md#type-htmlstring) | false | — | new title for the right button. |

---
## Method: SplitPane.setCurrentPane

### Description
Reveals the pane indicated by the `newPane` parameter.

This has different effects based on the [DeviceMode](../reference.md#type-devicemode) and [PageOrientation](../reference.md#type-pageorientation). For example, in "handset" mode, the new pane will be the only one showing. In other modes such as "desktop", this method may do nothing, but should still be called in order to ensure correct behavior with other [DeviceMode](../reference.md#type-devicemode) settings.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newPane | [CurrentPane](../reference.md#type-currentpane) | false | — | new pane to show. |

---
## Method: SplitPane.setDetailTitle

### Description
Sets the title for the [detailPane](#attr-splitpanedetailpane).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| title | [HTMLString](../reference.md#type-htmlstring) | false | — | new title for the detail pane. |

---
## Method: SplitPane.setAddHistoryEntries

### Description
Setter for [SplitPane.addHistoryEntries](#attr-splitpaneaddhistoryentries).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| addHistoryEntries | [boolean](../reference.md#type-boolean) | false | — | the new setting. |

---
## Method: SplitPane.setDetailNavigationControl

### Description
Navigation control that appears only when the navigation pane is not showing (showing detail pane on handset, or portrait mode on tablet).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| control | [Canvas](#type-canvas) | false | — | — |

---
## Method: SplitPane.setListPaneTitleTemplate

### Description
Sets a new [listPaneTitleTemplate](#attr-splitpanelistpanetitletemplate) at runtime.

By calling this method it is assumed you want the list pane title to change to the new template.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| template | [HTMLString](../reference.md#type-htmlstring) | false | — | new template, can use HTML to be styled. |

---
## Method: SplitPane.setShowDetailToolStrip

### Description
Setter for [SplitPane.showDetailToolStrip](#attr-splitpaneshowdetailtoolstrip). **Note:** If the property is set `false` after the [SplitPane.detailToolStrip](#attr-splitpanedetailtoolstrip) autochild has already been created, it will be hidden but not destroyed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showDetailToolStrip | [Boolean](#type-boolean) | false | — | new value |

---
## Method: SplitPane.paneChanged

### Description
Notification fired when the [SplitPane.currentPane](#attr-splitpanecurrentpane) changes, either due to end-user action or due to a programmatic call to [setCurrentPane()](#method-splitpanesetcurrentpane) or other APIs that can change the pane.

Note that depending on the [DeviceMode](../reference.md#type-devicemode), this event may not signal that any pane has actually been shown or hidden, since in some modes multiple panes are shown simultaneously.

Never fires while the `SplitPane` is not drawn.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newPane | [CurrentPane](../reference.md#type-currentpane) | false | — | new [SplitPane.currentPane](#attr-splitpanecurrentpane) value. |
| oldPane | [CurrentPane](../reference.md#type-currentpane) | false | — | old [SplitPane.currentPane](#attr-splitpanecurrentpane) value. |
| navigationMethod | [NavigationMethod](../reference_2.md#type-navigationmethod) | false | — | reason for pane change |

---
## Method: SplitPane.navigateListPane

### Description
Calls [SplitPane.navigatePane](#method-splitpanenavigatepane) with the [SplitPane.listPane](#attr-splitpanelistpane) as the target pane.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| title | [HTMLString](../reference.md#type-htmlstring) | true | — | optional title to use instead of the automatically chosen one |

---
