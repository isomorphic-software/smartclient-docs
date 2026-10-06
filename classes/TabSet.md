# TabSet Documentation

[← Back to API Index](../reference.md)

---

## Class: TabSet

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
The TabSet class allows components on several panes to share the same space. The tabs at the top can be selected by the user to show each pane.

Tabs are configured via the `tabs` property, each of which has a `pane` property which will be displayed in the main pane when that tab is selected.

---
## Attr: TabSet.moreTabPane

### Description
Pane contents for the "more" tab based on a VLayout. Typically contains a [NavigationBar](NavigationBar.md#class-navigationbar) and [TableView](TableView.md#class-tableview).

**Flags**: R

---
## Attr: TabSet.bottomEdgeSizes

### Description
If this tabSet will [show edges](#attr-tabsetshowpanecontaineredges) for the paneContainer, and [TabSet.symmetricEdges](#attr-tabsetsymmetricedges) is set to false, the `leftEdgeSizes`, `rightEdgeSizes`, `topEdgeSizes` and `bottomEdgeSizes` properties allow the sizes of edges for the paneContainer to be customized depending on the [TabSet.tabBarPosition](#attr-tabsettabbarposition).

The attribute should be specified an [edgeSizes map](../reference.md#type-edgesizes), specifying the desired edge sizes where for the appropriate [TabSet.tabBarPosition](#attr-tabsettabbarposition).

**Flags**: IR

---
## Attr: TabSet.symmetricEdges

### Description
If this tabSet will [show edges](#attr-tabsetshowpanecontaineredges) for the paneContainer, this property determines whether the same edge media will be used regardless of the tab bar position, or whether different media should be used (necessary if the edge appearance is not symmetrical on all sides).

If this property is set to false the paneContainer edge image URLs will be prefixed with the tabBarPosition of the tabSet - for example `"[SKIN]edge_top_T.gif"` rather than just `"[SKIN]edge_T.gif"`.

When `symmetricEdges` is false, custom edge sizes for the pane container may be specified via [TabSet.topEdgeSizes](#attr-tabsettopedgesizes) et al, and custom edge offsets via [TabSet.topEdgeOffsets](#attr-tabsettopedgeoffsets) et al.

### Groups

- appearance

**Flags**: IR

---
## Attr: TabSet.tabBarPosition

### Description
Which side of the TabSet the TabBar should appear on.

### Groups

- tabBar

**Flags**: IR

---
## Attr: TabSet.titleEditorProperties

### Description
Properties for the auto-generated [TabSet.titleEditor](#attr-tabsettitleeditor). This is the text item we use to edit tab titles in this tabSet.

### See Also

- [TabSet.titleEditor](#attr-tabsettitleeditor)
- [TabSet.canEditTabTitles](#attr-tabsetcanedittabtitles)

**Flags**: IR

---
## Attr: TabSet.tabBarProperties

### Description
This attribute allows developers to specify custom properties for this tabset's [TabSet.tabBar](#attr-tabsettabbar)

**Flags**: IR

---
## Attr: TabSet.titleEditor

### Description
TextItem we use to edit tab titles in this TabSet. You can override this property using the normal [AutoChild](../reference.md#type-autochild) facilities.

### See Also

- [TabSet.canEditTabTitles](#attr-tabsetcanedittabtitles)
- [Tab.canEditTitle](Tab.md#attr-tabcanedittitle)
- [TabSet.editTabTitle](#method-tabsetedittabtitle)

**Flags**: R

---
## Attr: TabSet.showTabBar

### Description
Should the tabBar be displayed or not If shrinkElementOnHide is true, the paneContainer will expand over the space occupied by TabBar

**Flags**: IRW

---
## Attr: TabSet.simpleTabIconOnlyBaseStyle

### Description
If [TabSet.useSimpleTabs](#attr-tabsetusesimpletabs) is true, `simpleTabIconOnlyBaseStyle` will be the base style used to determine the css style to apply to the tabs if [Tab.canAdaptWidth](Tab.md#attr-tabcanadaptwidth) is set and the title is not being shown.

This property will be suffixed with the side on which the tab-bar will appear, followed by with the tab's state (selected, over, etc), resolving to a className like "iconOnlyTabButtonTopOver".

Note that this property is only defined for certain skins, where it's needed. If not defined, [TabSet.simpleTabBaseStyle](#attr-tabsetsimpletabbasestyle) will serve as base style whether or not the title is hidden.

### See Also

- [Button.baseStyle](Button.md#attr-buttonbasestyle)
- [Button.iconOnlyBaseStyle](Button.md#attr-buttonicononlybasestyle)
- [TabSet.simpleTabBaseStyle](#attr-tabsetsimpletabbasestyle)

**Flags**: IRW

---
## Attr: TabSet.canAddTabs

### Description
Causes the [TabSet.addTabButton](#attr-tabsetaddtabbutton) to appear after the [TabSet.tabs](#attr-tabsettabs) and before the [TabSet.tabBarControls](#attr-tabsettabbarcontrols).

There is no default behavior for what happens when the `addTabButton` is clicked. Add a handler for the [TabSet.addTabClick](#method-tabsetaddtabclick) event to implement a behavior.

**Flags**: IR

---
## Attr: TabSet.scrollerButtonSize

### Description
If [TabSet.showTabScroller](#attr-tabsetshowtabscroller) is true, this property governs the size of scroller buttons. Applied as the width of buttons if the tabBar is horizontal, or the height if tabBar is vertical. Note that the other dimension is determined by [this.tabBarThickness](#attr-tabsettabbarthickness)

### Groups

- tabBarControls

**Flags**: IR

---
## Attr: TabSet.showTabScroller

### Description
If there is not enough space to display all the tab-buttons in this tabSet, should scroll buttons be displayed to allow access to tabs that are clipped? If unset, defaults to false for [handsets](Browser.md#classattr-browserishandset) and true otherwise.

### Groups

- tabBarControls

**Flags**: IR

---
## Attr: TabSet.tabBarControlLayout

### Description
[AutoChild](../reference.md#type-autochild) of type [Layout](Layout.md#class-layout) that holds the [TabSet.tabBarControls](#attr-tabsettabbarcontrols) as well as the built-in controls such as the [tab picker menu](#attr-tabsetshowtabpicker).

**Flags**: IR

---
## Attr: TabSet.tabBar

### Description
TabBar for this TabSet, an instance of [TabBar](TabBar.md#class-tabbar).

**Flags**: R

---
## Attr: TabSet.moreTabPaneNavBar

### Description
Navigation bar shown in the [TabSet.moreTabPane](#attr-tabsetmoretabpane);

**Flags**: IR

---
## Attr: TabSet.destroyPanes

### Description
Whether [destroy()](Canvas.md#method-canvasdestroy) should be called on [Tab.pane](Tab.md#attr-tabpane) when it a tab is removed via [TabSet.removeTab](#method-tabsetremovetab).

With the default setting of `null` panes will be automatically destroyed. An application might set this to false in order to re-use panes in different tabs or in different parts of the application.

### Groups

- lifecycle

**Flags**: IR

---
## Attr: TabSet.canReorderTabs

### Description
If true, tabs can be reordered by dragging on them.

To disallow drag-reorder of a specific tab, see [Tab.canReorder](Tab.md#attr-tabcanreorder).

### Groups

- dragdrop

**Flags**: IR

---
## Attr: TabSet.defaultTabWidth

### Description
If set, is passed as "width" to all tabs when [TabSet.tabBarPosition](#attr-tabsettabbarposition) is set to `"top"` or `"bottom"`.

If unset, width will be picked up from the Tab constructor class defaults. Tabs expand to fit their content, so this width acts as a minimum. Setting width:1 will result in tabs that are only as wide as their titles. May be customized by individual [skins](../kb_topics/skinning.md#kb-topic-skinning--theming).

**Flags**: IR

---
## Attr: TabSet.titleEditorTopOffset

### Description
If set, offsets the tab title editor further down from the top edge of the tab, by the number of pixels set in this property. You can use this property, together with the left and right offset properties, to fine tune positioning of the editor within or around the tab button.

**Note:** The height of the editor is an attribute of the editor itself, and can be set by specifying a "height" property in [titleEditorDefaults](#attr-tabsettitleeditor).

### See Also

- [TabSet.titleEditorLeftOffset](#attr-tabsettitleeditorleftoffset)
- [TabSet.titleEditorRightOffset](#attr-tabsettitleeditorrightoffset)

**Flags**: IRW

---
## Attr: TabSet.selectedTab

### Description
Specifies the index of the initially selected tab.

### Groups

- tabBar

**Flags**: IRW

---
## Attr: TabSet.tabProperties

### Description
Properties to apply to all Tabs created by this TabSet.

**Flags**: IR

---
## Attr: TabSet.closeTabIcon

### Description
Default src for the close icon for tabs to display if [TabSet.canCloseTabs](#attr-tabsetcanclosetabs) is true.

### Groups

- appearance

**Flags**: IR

---
## Attr: TabSet.tabs

### Description
An array of [Tab](../reference.md#object-tab) objects, specifying the title and pane contents of each tab in the TabSet. When developing in JavaScript, tabs are specified as an array of object literals, not instances - see [Tab](../reference.md#object-tab).

After providing [Tab](../reference.md#object-tab) instances to `setTabs()`, the TabSet creates actual UI widgets to serve as interactive tabs. Any further modifications to tabs should be performed via TabSet APIs such as [TabSet.setTabTitle](#method-tabsetsettabtitle), [TabSet.setTabIcon](#method-tabsetsettabicon) and [TabSet.setTabPane](#method-tabsetsettabpane).

You can add and remove tabs after creating the TabSet by calling [TabSet.addTab](#method-tabsetaddtab) and [TabSet.removeTab](#method-tabsetremovetab)

**Flags**: IRW

---
## Attr: TabSet.canEditTabTitles

### Description
If true, users can edit the titles of tabs in this TabSet when the [titleEditEvent](#attr-tabsettitleeditevent) fires. You can override this behavior per tab with the [Tab.canEditTitle](Tab.md#attr-tabcanedittitle) property.

Note that this TabSet's [titleEditEvent](#attr-tabsettitleeditevent) must be set to a supported [TabTitleEditEvent](../reference.md#type-tabtitleeditevent) in order for users to be able to edit the titles of tabs.

**Flags**: IRW

---
## Attr: TabSet.rightEdgeOffsets

### Description
If this tabSet will [show edges](#attr-tabsetshowpanecontaineredges) for the paneContainer, and [TabSet.symmetricEdges](#attr-tabsetsymmetricedges) is set to false, the `leftEdgeOffsets`, `rightEdgeOffsets`, `topEdgeOffsets` and `bottomEdgeOffsets` properties allow the offsets of edges for the paneContainer to be customized depending on the [TabSet.tabBarPosition](#attr-tabsettabbarposition).

The attribute should be specified an [edgeSizes map](../reference.md#type-edgesizes), specifying the desired edge offsets where for the appropriate [TabSet.tabBarPosition](#attr-tabsettabbarposition).

**Flags**: IR

---
## Attr: TabSet.moreTabPaneTable

### Description
[TableView](TableView.md#class-tableview) used to show links to other tabs in the [TabSet.moreTabPane](#attr-tabsetmoretabpane);

**Flags**: IR

---
## Attr: TabSet.paneMargin

### Description
Space to leave around the panes in our paneContainer

Note that this property may be specified on a per-tab basis via [Tab.paneMargin](Tab.md#attr-tabpanemargin).

**Flags**: IR

---
## Attr: TabSet.paneContainerClassName

### Description
CSS style used for the paneContainer.

### Groups

- appearance

**Flags**: IRW

---
## Attr: TabSet.defaultTabHeight

### Description
If set, is passed as "height" to all tabs when [TabSet.tabBarPosition](#attr-tabsettabbarposition) is set to `"left"` or `"right"`.

If unset, height will be picked up from the Tab constructor class defaults. Note that tabs expand to fit their content so this height acts as a minimum. May be customized by individual [skins](../kb_topics/skinning.md#kb-topic-skinning--theming).

**Flags**: IR

---
## Attr: TabSet.symmetricScroller

### Description
If this TabSet is showing [tab scroller buttons](#attr-tabsetshowtabscroller), this property determines whether the [TabSet.scrollerHSrc](#attr-tabsetscrollerhsrc) and [TabSet.scrollerVSrc](#attr-tabsetscrollervsrc) media will be used for vertical and horizontal tab-bar scroller buttons, or whether separate media should be used for each possible [tabBarPosition](#attr-tabsettabbarposition) based on the [TabSet.scrollerSrc](#attr-tabsetscrollersrc) property for this tabSet.

### Groups

- tabBarScrolling

**Flags**: IR

---
## Attr: TabSet.moreTabImage

### Description
If [TabSet.showMoreTab](#attr-tabsetshowmoretab) is enabled this property determines the image to display on the "More" tab button.

**Flags**: IR

---
## Attr: TabSet.tabBarAlign

### Description
Alignment of the tabBar.

If the [tabBarPosition](#attr-tabsettabbarposition) is "top" or "bottom", then this attribute may be set to "left", "right" or "center". The default is "left", or "right" in [RTL mode](Page.md#classmethod-pageisrtl).

If the [tabBarPosition](#attr-tabsettabbarposition) is "left" or "right", then this attribute may be set to "top", "bottom" or "center". The default is "top".

### Groups

- tabBar

**Flags**: IRW

---
## Attr: TabSet.topEdgeOffsets

### Description
If this tabSet will [show edges](#attr-tabsetshowpanecontaineredges) for the paneContainer, and [TabSet.symmetricEdges](#attr-tabsetsymmetricedges) is set to false, the `leftEdgeOffsets`, `rightEdgeOffsets`, `topEdgeOffsets` and `bottomEdgeOffsets` properties allow the offsets of edges for the paneContainer to be customized depending on the [TabSet.tabBarPosition](#attr-tabsettabbarposition).

The attribute should be specified an [edgeSizes map](../reference.md#type-edgesizes), specifying the desired edge offsets where for the appropriate [TabSet.tabBarPosition](#attr-tabsettabbarposition).

**Flags**: IR

---
## Attr: TabSet.paneContainer

### Description
Container where the component specified by [Tab.pane](Tab.md#attr-tabpane) is shown.

Note: paneContainer and showEdges:true for rounded tabsets: you can enable decorative image-based edges on the paneContainer by setting [showEdges:true](Canvas.md#attr-canvasshowedges) via paneContainerDefaults (to skin all tabsets) or paneContainerProperties (to use edges on one instance). In this structure, the [baseLine](../reference.md#kb-topic-baseline) should use media that matches the appearance of the decorative edges and fully overlaps the edge of the paneContainer that it is adjacent to. In the most typical appearance (symmetric edges on all 4 sides), both [TabBar.baseLineCapSize](TabBar.md#attr-tabbarbaselinecapsize) and [TabBar.baseLineThickness](TabBar.md#attr-tabbarbaselinethickness) match the [edgeSize](Canvas.md#attr-canvasedgesize) set on the paneContainer. See the load\_skin.js file for the "SmartClient" skin for an example of setting all relevant properties.

To disable edges for a particular TabSet, which you may want to do for a TabSet that is already within a clearly defined container, configure the paneContainer to show only it's top edge:

```
      paneContainerProperties : { customEdges:["T"] },
 
```
To completely flatten even the top edge of the TabSet:
```
      paneContainerProperties : { customEdges:["T"] },
      tabBarProperties :{ baseLineCapSize:0 },
 
```
This "flattens" the baseLine so that only the center image is used.

**Flags**: R

---
## Attr: TabSet.simpleTabButtonConstructor

### Description
Tab button constructor if [TabSet.useSimpleTabs](#attr-tabsetusesimpletabs) is true.

**Flags**: IRA

---
## Attr: TabSet.tabPicker

### Description
A button control that allows tabs to be picked directly from a popup menu. The tabPicker is created automatically when needed and when `"tabPicker"` is specified in the [TabSet.tabBarControls](#attr-tabsettabbarcontrols).

### Groups

- tabBarControls

**Flags**: R

---
## Attr: TabSet.titleEditorRightOffset

### Description
If set, offsets the tab title editor further in from the right-hand edge of the tab, by the number of pixels set in this property. Note that the editor is always offset to avoid overlapping the endcaps of the tab; this property is applied on top of that default offset.

### See Also

- [TabSet.titleEditorLeftOffset](#attr-tabsettitleeditorleftoffset)
- [TabSet.titleEditorTopOffset](#attr-tabsettitleeditortopoffset)

**Flags**: IRW

---
## Attr: TabSet.moreTabCount

### Description
This property defines the number tab buttons that should be shown before automatically adding a "more" button to handle the remaining tabs. This property is only used when [TabSet.showMoreTab](#attr-tabsetshowmoretab) is enabled.

**Flags**: IR

---
## Attr: TabSet.scrollerVSrc

### Description
If this TabSet is showing [tab scroller buttons](#attr-tabsetshowtabscroller), and [symmetricScroller](#attr-tabsetsymmetricscroller) is true, this property governs the base URL for the tab bar back and forward scroller button images for vertical tab bars \[IE for tab sets with [tabBarPosition](#attr-tabsettabbarposition) set to "left" or "right"\].

Note that if [symmetricScroller](#attr-tabsetsymmetricscroller) is false, [TabSet.scrollerSrc](#attr-tabsetscrollersrc) will be used instead.

To get the path to the image to display, this base URL will be modified as follows:

*   If appropriate a state suffix of `"Down"` or `"Disabled"` will be appended.
*   A suffix of `"forward"` or `"back"` will be appended for the forward or backward scrolling button.

For example - if the scrollerVSrc is set to `"[SKIN]vscroll.gif"`, the image displayed for the back-scroller button on a tabSet with `tabBarPosition` set to "left" and `symmetricScroller` set to true would be one of `"[SKIN]vscroll_back.gif"`, `"[SKIN]vscroll_Down_back.gif"`, and `"[SKIN]vscroll_Disabled_back.gif"`.

Note that for best results the media should be sized to match the scroller button sizes, determined by [TabSet.tabBarThickness](#attr-tabsettabbarthickness) and [TabSet.scrollerButtonSize](#attr-tabsetscrollerbuttonsize).

### Groups

- tabBarScrolling

### See Also

- [TabSet.symmetricScroller](#attr-tabsetsymmetricscroller)

**Flags**: IR

---
## Attr: TabSet.moreTab

### Description
[Tab](../reference.md#object-tab) to be shown when [TabSet.showMoreTab](#attr-tabsetshowmoretab) is enabled more than [TabSet.moreTabCount](#attr-tabsetmoretabcount) tabs are provided.

**Flags**: R

---
## Attr: TabSet.touchPickerButtonSize

### Description
The size of the tab picker button when [Browser.isTouch](Browser.md#classattr-browseristouch) is `true`.

### Groups

- tabBarControls

### See Also

- [TabSet.pickerButtonSize](#attr-tabsetpickerbuttonsize)

**Flags**: IR

---
## Attr: TabSet.symmetricPickerButton

### Description
If this TabSet is showing a [tab picker button](#attr-tabsetshowtabpicker), this property determines whether the [TabSet.pickerButtonHSrc](#attr-tabsetpickerbuttonhsrc) and [TabSet.pickerButtonVSrc](#attr-tabsetpickerbuttonvsrc) media will be used for vertical and horizontal tab-bar picker buttons, or whether separate media should be used for each possible [tabBarPosition](#attr-tabsettabbarposition) based on the [TabSet.pickerButtonSrc](#attr-tabsetpickerbuttonsrc) property for this tabSet.

### Groups

- tabBarScrolling

**Flags**: IR

---
## Attr: TabSet.pickerButtonHSrc

### Description
If [TabSet.showTabPicker](#attr-tabsetshowtabpicker) is true, and [TabSet.symmetricPickerButton](#attr-tabsetsymmetricpickerbutton) is set to true, this property governs the base URL for the picker button image, when displayed in a horizontal tab-bar \[IE [TabSet.tabBarPosition](#attr-tabsettabbarposition) is set to `"top"` or `"bottom"`\].

Note that if `symmetricPickerButton` is false, the [TabSet.pickerButtonSrc](#attr-tabsetpickerbuttonsrc) property will be used instead.

This base URL will have a suffix of `"Down"` appended when the user holds the mouse down over the button, and `"Disabled"` if the tabset as a whole is disabled.

### Groups

- tabBarScrolling

### See Also

- [TabSet.symmetricPickerButton](#attr-tabsetsymmetricpickerbutton)

**Flags**: IR

---
## Attr: TabSet.scrollerSrc

### Description
If this TabSet is showing [tab scroller buttons](#attr-tabsetshowtabscroller), and [symmetricScroller](#attr-tabsetsymmetricscroller) is false, this property governs the base URL for the tab bar back and forward scroller button images.

Note that if [symmetricScroller](#attr-tabsetsymmetricscroller) is true, [TabSet.scrollerHSrc](#attr-tabsetscrollerhsrc) and [TabSet.scrollerVSrc](#attr-tabsetscrollervsrc) will be used instead.

To get the path to the image to display, this base URL will be modified as follows:

*   If appropriate a state suffix of `"Down"` or `"Disabled"` will be appended.
*   The [tabBarPosition](#attr-tabsettabbarposition) for this tabSet will be appended.
*   A suffix of `"forward"` or `"back"` will be appended for the forward or backward scrolling button.

For example - if the scrollerSrc is set to `"[SKIN]scroll.gif"`, the image displayed for the back-scroller button on a tabSet with `tabBarPosition` set to "top" and `symmetricScroller` set to false would be one of `"[SKIN]scroll_top_back.gif"`, `"[SKIN]scroll_Down_top_back.gif"`, and `"[SKIN]scroll_Disabled_top_back.gif"`.

Note that for best results the media should be sized to match the scroller button sizes, determined by [TabSet.tabBarThickness](#attr-tabsettabbarthickness) and [TabSet.scrollerButtonSize](#attr-tabsetscrollerbuttonsize).

### Groups

- tabBarScrolling

### See Also

- [TabSet.symmetricScroller](#attr-tabsetsymmetricscroller)

**Flags**: IR

---
## Attr: TabSet.topEdgeSizes

### Description
If this tabSet will [show edges](#attr-tabsetshowpanecontaineredges) for the paneContainer, and [TabSet.symmetricEdges](#attr-tabsetsymmetricedges) is set to false, the `leftEdgeSizes`, `rightEdgeSizes`, `topEdgeSizes` and `bottomEdgeSizes` properties allow the sizes of edges for the paneContainer to be customized depending on the [TabSet.tabBarPosition](#attr-tabsettabbarposition).

The attribute should be specified an [edgeSizes map](../reference.md#type-edgesizes), specifying the desired edge sizes where for the appropriate [TabSet.tabBarPosition](#attr-tabsettabbarposition).

**Flags**: IR

---
## Attr: TabSet.showMoreTab

### Description
Should tabs exceeding [TabSet.moreTabCount](#attr-tabsetmoretabcount) be shown on a "more" tab?

This setting is used to emulate an iPhone-style tab bar "more" button.

**Flags**: IR

---
## Attr: TabSet.useIOSTabs

### Description
Setting this to true turns on a different appearance for tabs, similar to iOS tabs from the "Music" app, where the tab.icon is enlarged and shown as a black and white mask. This mode does not support a clickable icon - clicking the enlarged icon just switches tabs.

This attribute only has an effect for tabs that are not [closable](Tab.md#attr-tabcanclose), and only for Mobile WebKit.

**Flags**: IR

---
## Attr: TabSet.animateTabScrolling

### Description
If [TabSet.showTabScroller](#attr-tabsetshowtabscroller) is true, should tabs be scrolled into view via an animation when the user interacts with the scroller buttons?

### Groups

- tabBarControls

**Flags**: IR

---
## Attr: TabSet.bottomEdgeOffsets

### Description
If this tabSet will [show edges](#attr-tabsetshowpanecontaineredges) for the paneContainer, and [TabSet.symmetricEdges](#attr-tabsetsymmetricedges) is set to false, the `leftEdgeOffsets`, `rightEdgeOffsets`, `topEdgeOffsets` and `bottomEdgeOffsets` properties allow the offsets of edges for the paneContainer to be customized depending on the [TabSet.tabBarPosition](#attr-tabsettabbarposition).

The attribute should be specified an [edgeSizes map](../reference.md#type-edgesizes), specifying the desired edge offsets where for the appropriate [TabSet.tabBarPosition](#attr-tabsettabbarposition).

**Flags**: IR

---
## Attr: TabSet.showTabPicker

### Description
If there is not enough space to display all the tab-buttons in this tabSet, should a drop-down "picker" be displayed to allow selection of tabs that are clipped?

### Groups

- tabBarControls

**Flags**: IR

---
## Attr: TabSet.paneContainerOverflow

### Description
Specifies the overflow of the pane container (the component that holds the pane contents for all tabs). By default this is set to "auto", meaning the pane container will automatically introduce scrolling when the pane contents exceed the TabSet's specified size.

For other values and their meaning, see [Overflow](../reference.md#type-overflow)

**Flags**: IRWA

---
## Attr: TabSet.leftEdgeSizes

### Description
If this tabSet will [show edges](#attr-tabsetshowpanecontaineredges) for the paneContainer, and [TabSet.symmetricEdges](#attr-tabsetsymmetricedges) is set to false, the `leftEdgeSizes`, `rightEdgeSizes`, `topEdgeSizes` and `bottomEdgeSizes` properties allow the sizes of edges for the paneContainer to be customized depending on the [TabSet.tabBarPosition](#attr-tabsettabbarposition).

The attribute should be specified an [edgeSizes map](../reference.md#type-edgesizes), specifying the desired edge sizes where for the appropriate [TabSet.tabBarPosition](#attr-tabsettabbarposition).

**Flags**: IR

---
## Attr: TabSet.tabBarControls

### Description
This property determines what controls should show up after the tabBar for this TabSet. Standard controls can be included using the strings `"tabScroller"` and `"tabPicker"`. These correspond to the [TabSet.scroller](#attr-tabsetscroller) and [TabSet.tabPicker](#attr-tabsettabpicker) AutoChildren, respectively. The `"tabScroller"` standard control shows two buttons for scrolling through the tabs in order and the `"tabPicker"` standard control allows tabs to be picked directly from a menu. The standard controls show up only if [TabSet.showTabScroller](#attr-tabsetshowtabscroller) or [TabSet.showTabPicker](#attr-tabsetshowtabpicker) is true and there is not enough space available to show all of the tabs in the tabBar.

*This sample* illustrates the usage of this property

Additional controls can be included by adding any widget to this array. Controls will show up in the order in which they are specified. For example, the following code would add a button in the tabBar area, while preserving the normal behavior of the tabScroller and tabPicker:

```
 isc.TabSet.create({
     width:300,
     tabs : [
         { title: "Tab one" }
     ],
     tabBarControls : [
         isc.ImgButton.create({
             src:"[SKINIMG]/actions/add.png",
             width:16, height:16,
             layoutAlign:"center"
         }),
         "tabScroller", "tabPicker"
     ]
 });
 
```
You can also refer to the default tabPicker/tabScroll controls from Component XML:
```
 <TabSet width="300">
     <tabBarControls>
         <Button title="Custom Button"/>
         <value xsi:type="string">tabPicker</value>
         <value xsi:type="string">tabScroller</value>
      </tabBarControls>
      <tabs>
          <tab title="Foo"/>
          <tab title="Bar"/>
     </tabs>
 </TabSet>
 
```

When [Browser.isTouch](Browser.md#classattr-browseristouch) is `true` and native touch scrolling is supported, then by default, only the `"tabPicker"` is shown. The `"tabScroller"` control is omitted by default on touch devices because the tabs in the tab bar are native touch-scrollable, so the `"tabScroller"` control is unnecessary. To override the omission of the `"tabScroller"`, simply add "tabScroller" to the `tabBarControls` array.

**Note:** Due to tabs supporting [adaptive width](Tab.md#attr-tabcanadaptwidth) and other complexities of TabSet widget layout, [flexible-sized](Canvas.md#attr-canvaswidth) controls (including [spacers](../reference.md#class-layoutspacer)) aren't supported in `tabBarControls`. However, if you take into account the width of your tabs and whether the [picker](#attr-tabsettabpicker) and [TabSet.scroller](#attr-tabsetscroller) are present, you can add a fixed-width spacer to achieve the desired appearance, as long as the set of tabs and TabSet width are static.

### Groups

- tabBarControls

**Flags**: IRA

---
## Attr: TabSet.skinImgDir

### Description
Default directory for skin images (those defined by the class), relative to the Page-wide [skinDir](Page.md#classmethod-pagegetskindir).

### Groups

- images

**Flags**: IR

---
## Attr: TabSet.scrollerHSrc

### Description
If this TabSet is showing [tab scroller buttons](#attr-tabsetshowtabscroller), and [symmetricScroller](#attr-tabsetsymmetricscroller) is true, this property governs the base URL for the tab bar back and forward scroller button images for horizontal tab bars \[IE for tab sets with [tabBarPosition](#attr-tabsettabbarposition) set to "top" or "bottom"\].

Note that if [symmetricScroller](#attr-tabsetsymmetricscroller) is false, [TabSet.scrollerSrc](#attr-tabsetscrollersrc) will be used instead.

To get the path to the image to display, this base URL will be modified as follows:

*   If appropriate a state suffix of `"Down"` or `"Disabled"` will be appended.
*   A suffix of `"forward"` or `"back"` will be appended for the forward or backward scrolling button.

For example - if the scrollerHSrc is set to `"[SKIN]hscroll.gif"`, the image displayed for the back-scroller button on a tabSet with `tabBarPosition` set to "top" and `symmetricScroller` set to true would be one of `"[SKIN]hscroll_back.gif"`, `"[SKIN]hscroll_Down_back.gif"`, and `"[SKIN]hscroll_Disabled_back.gif"`.

Note that for best results the media should be sized to match the scroller button sizes, determined by [TabSet.tabBarThickness](#attr-tabsettabbarthickness) and [TabSet.scrollerButtonSize](#attr-tabsetscrollerbuttonsize).

### Groups

- tabBarScrolling

### See Also

- [TabSet.symmetricScroller](#attr-tabsetsymmetricscroller)

**Flags**: IR

---
## Attr: TabSet.showPartialEdges

### Description
If the paneContainer for this tab set is showing [edges](Canvas.md#attr-canvasshowedges), setting this attribute to `true` will set the paneContainer to show [customEdges](Canvas.md#attr-canvascustomedges) for the three sides opposing the tabBarPosition.

**Flags**: IRA

---
## Attr: TabSet.scroller

### Description
A component containing back and forward buttons for scrolling through all of the tabs of the TabSet. The scroller is created automatically when needed and when `"tabScroller"` is specified in the [TabSet.tabBarControls](#attr-tabsettabbarcontrols).

By default, the scroller constructor is [StretchImgButton](StretchImgButton.md#class-stretchimgbutton). Note that the scroller [items](StretchImg.md#attr-stretchimgitems) are determined automatically, so any items set in scrollerProperties will be ignored.

### Groups

- tabBarControls

**Flags**: R

---
## Attr: TabSet.tabBarThickness

### Description
Thickness of tabBar, applies to either orientation (specifies height for horizontal, width for vertical orientation). Note that overriding this value for TabSets that are skinned with images generally means providing new media for the borders.

### Groups

- tabBar

**Flags**: IR

---
## Attr: TabSet.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: TabSet.pickerButtonVSrc

### Description
If [TabSet.showTabPicker](#attr-tabsetshowtabpicker) is true, and [TabSet.symmetricPickerButton](#attr-tabsetsymmetricpickerbutton) is set to true, this property governs the base URL for the picker button image, when displayed in a verricaL tab-bar \[IE [TabSet.tabBarPosition](#attr-tabsettabbarposition) is set to `"LEFT"` or `"right"`\].

Note that if `symmetricPickerButton` is false, the [TabSet.pickerButtonSrc](#attr-tabsetpickerbuttonsrc) property will be used instead.

This base URL will have a suffix of `"Down"` appended when the user holds the mouse down over the button, and `"Disabled"` if the tabset as a whole is disabled.

### Groups

- tabBarScrolling

### See Also

- [TabSet.symmetricPickerButton](#attr-tabsetsymmetricpickerbutton)

**Flags**: IR

---
## Attr: TabSet.ariaCloseableSuffix

### Description
When [screen reader mode](isc.md#staticmethod-iscsetscreenreadermode) is enabled and a tab is [closeable](#attr-tabsetcanclosetabs), the `ariaCloseableSuffix` is a string that is appended to the label of closeable tabs. This suffix is hidden from sighted users, but is announced by screen readers to indicate that the tab may be closed.

Set to `null` to disable appending this suffix.

### Groups

- i18nMessages

**Flags**: IRA

---
## Attr: TabSet.rightEdgeSizes

### Description
If this tabSet will [show edges](#attr-tabsetshowpanecontaineredges) for the paneContainer, and [TabSet.symmetricEdges](#attr-tabsetsymmetricedges) is set to false, the `leftEdgeSizes`, `rightEdgeSizes`, `topEdgeSizes` and `bottomEdgeSizes` properties allow the sizes of edges for the paneContainer to be customized depending on the [TabSet.tabBarPosition](#attr-tabsettabbarposition).

The attribute should be specified an [edgeSizes map](../reference.md#type-edgesizes), specifying the desired edge sizes where for the appropriate [TabSet.tabBarPosition](#attr-tabsettabbarposition).

**Flags**: IR

---
## Attr: TabSet.pickerButtonSize

### Description
If [showTabPicker](#attr-tabsetshowtabpicker) is `true` and [Browser.isTouch](Browser.md#classattr-browseristouch) is `false`, this property governs the size of the tab picker button. This value is applied as the width of the tab picker button if the [tabBar](#attr-tabsettabbar) is horizontal, or the height if the `tabBar` is vertical. Note that the other dimension is determined by [this.tabBarThickness](#attr-tabsettabbarthickness).

On touch browsers (where [Browser.isTouch](Browser.md#classattr-browseristouch) is `true`), [touchPickerButtonSize](#attr-tabsettouchpickerbuttonsize) is used instead.

### Groups

- tabBarControls

**Flags**: IR

---
## Attr: TabSet.leftEdgeOffsets

### Description
If this tabSet will [show edges](#attr-tabsetshowpanecontaineredges) for the paneContainer, and [TabSet.symmetricEdges](#attr-tabsetsymmetricedges) is set to false, the `leftEdgeOffsets`, `rightEdgeOffsets`, `topEdgeOffsets` and `bottomEdgeOffsets` properties allow the offsets of edges for the paneContainer to be customized depending on the [TabSet.tabBarPosition](#attr-tabsettabbarposition).

The attribute should be specified an [edgeSizes map](../reference.md#type-edgesizes), specifying the desired edge offsets where for the appropriate [TabSet.tabBarPosition](#attr-tabsettabbarposition).

**Flags**: IR

---
## Attr: TabSet.moreTabPaneProperties

### Description
Properties to apply to the "more" tab's pane created by this TabSet.

**Flags**: IR

---
## Attr: TabSet.simpleTabBaseStyle

### Description
If [TabSet.useSimpleTabs](#attr-tabsetusesimpletabs) is true, `simpleTabBaseStyle` will be the base style used to determine the css style to apply to the tabs.

This property will be suffixed with the side on which the tab-bar will appear, followed by with the tab's state (selected, over, etc), resolving to a className like "tabButtonTopOver".

### Groups

- appearance

### See Also

- [Button.baseStyle](Button.md#attr-buttonbasestyle)
- [TabSet.simpleTabIconOnlyBaseStyle](#attr-tabsetsimpletabicononlybasestyle)

**Flags**: IRW

---
## Attr: TabSet.moreTabTitle

### Description
Title for the "More" tab.

**Flags**: IR

---
## Attr: TabSet.titleEditorLeftOffset

### Description
If set, offsets the tab title editor further in from the left-hand edge of the tab, by the number of pixels set in this property. Note that the editor is always offset to avoid overlapping the endcaps of the tab; this property is applied on top of that default offset.

### See Also

- [TabSet.titleEditorRightOffset](#attr-tabsettitleeditorrightoffset)
- [TabSet.titleEditorTopOffset](#attr-tabsettitleeditortopoffset)

**Flags**: IRW

---
## Attr: TabSet.titleEditEvent

### Description
The event that triggers title editing on this TabSet.

### See Also

- [TabSet.canEditTabTitles](#attr-tabsetcanedittabtitles)
- [Tab.canEditTitle](Tab.md#attr-tabcanedittitle)

**Flags**: IRW

---
## Attr: TabSet.addTabButton

### Description
Appears when [TabSet.canAddTabs](#attr-tabsetcanaddtabs) is enabled.

**Flags**: IR

---
## Attr: TabSet.useSimpleTabs

### Description
Should we use simple button based tabs styled with CSS rather than image based [ImgTab](ImgTab.md#class-imgtab) tabs?

If set to true the [TabSet.simpleTabButtonConstructor](#attr-tabsetsimpletabbuttonconstructor) will be used and tabs will by styled according to [TabSet.simpleTabBaseStyle](#attr-tabsetsimpletabbasestyle).

**Flags**: IRA

---
## Attr: TabSet.addTabButtonIcon

### Description
Icon for the [TabSet.addTabButton](#attr-tabsetaddtabbutton).

**Flags**: IR

---
## Attr: TabSet.locateTabsBy

### Description
When [AutoTest.getElement](AutoTest.md#classmethod-autotestgetelement) is used to parse locator strings generated by [AutoTest.getLocator](AutoTest.md#classmethod-autotestgetlocator), how should tabs within this tabset be identified? If the locator has a specified [Tab.ID](Tab.md#attr-tabid) or [Tab.name](Tab.md#attr-tabname), no fallback approach will be used as those attributes (with [Tab.ID](Tab.md#attr-tabid) having priority) are each alone considered to definitively locate it.

Otherwise, the following options are available:

*   `"title"` use the title as an identifier
*   `"index"` use the index of the tab in the tabset as an identifier

If unset, and the locator has no specified ID or name, default behavior is to identify by title (if available), otherwise by index.

### Groups

- autoTest

### See Also

- [LocatorStrategy](../reference_2.md#type-locatorstrategy)

**Flags**: IRWA

---
## Attr: TabSet.closeTabIconSize

### Description
Size in pixels of the icon for closing tabs, displayed when [TabSet.canCloseTabs](#attr-tabsetcanclosetabs) is true.

**Flags**: IR

---
## Attr: TabSet.canCloseTabs

### Description
Should tabs in this tabSet show an icon allowing the user to dismiss the tab by clicking on it directly. May be overridden for individual tabs by setting [Tab.canClose](Tab.md#attr-tabcanclose).

The URL for this icon's image will be derived from [TabSet.closeTabIcon](#attr-tabsetclosetabicon) by default, but may be overridden by explicitly specifying [Tab.closeIcon](Tab.md#attr-tabcloseicon).

**Note**: Currently, tabs can only show a single icon, so a closable tab will show the close icon only even if [Tab.icon](Tab.md#attr-tabicon) is set. To work around this, add the icon as an HTML `<img>` tag to the [Tab.title](Tab.md#attr-tabtitle) property, for example:

```
    title : "<span>" + isc.Canvas.imgHTML("path/to/icon.png") + " Tab Title</span>"
 
```

### Groups

- tabBar

### See Also

- [TabSet.closeClick](#method-tabsetcloseclick)

**Flags**: IRW

---
## Attr: TabSet.moreTabPaneDefaults

### Description
Default properties for the "more" tab's pane.

Currently constructs a VLayout with a [NavigationBar](NavigationBar.md#class-navigationbar) and [TableView](TableView.md#class-tableview).

**Flags**: IR

---
## Attr: TabSet.pickerButtonSrc

### Description
If [TabSet.showTabPicker](#attr-tabsetshowtabpicker) is true, this property governs the base URL for the picker button image, when [TabSet.symmetricPickerButton](#attr-tabsetsymmetricpickerbutton) is set to false

Note that if `symmetricPickerButton` is true, the [TabSet.pickerButtonHSrc](#attr-tabsetpickerbuttonhsrc) and [TabSet.pickerButtonVSrc](#attr-tabsetpickerbuttonvsrc) properties will be used instead.

To get the path to the image to display, this base URL will be modified as follows:

*   If appropriate a state suffix of `"Down"` or `"Disabled"` will be appended.
*   The [tabBarPosition](#attr-tabsettabbarposition) for this tabSet will be appended.

### Groups

- tabBarScrolling

### See Also

- [TabSet.symmetricPickerButton](#attr-tabsetsymmetricpickerbutton)

**Flags**: IR

---
## Attr: TabSet.showPaneContainerEdges

### Description
Should the paneContainer for this tabset show [edges](Canvas.md#attr-canvasshowedges).

**Flags**: IRWA

---
## Attr: TabSet.moreTabProperties

### Description
Properties to apply to the "more" tab created by this TabSet.

**Flags**: IR

---
## Method: TabSet.tabIconClick

### Description
Method fired when the user clicks the icon for a tab, as specified via [Tab.icon](Tab.md#attr-tabicon).

Default behavior will fire `icon.click()` if specified, with two parameters `tab` (a pointer to the tab object and `tabSet` a pointer to the tabSet instance.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [Tab](#type-tab) | false | — | with click handler being fired |

---
## Method: TabSet.setPaneContainerOverflow

### Description
Update [TabSet.paneContainerOverflow](#attr-tabsetpanecontaineroverflow) after creation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newOverflow | [Overflow](../reference.md#type-overflow) | false | — | new overflow setting |

---
## Method: TabSet.tabDeselected

### Description
Optional handler to fire when a tab is deselected. Returning false will cancel the new selection, leaving tab `ID` selected. As with [TabSet.tabSelected](#method-tabsettabselected) this method only fires when the tabset is drawn.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tabNum | [Integer](../reference_2.md#type-integer) | false | — | the index of the deselected tab |
| tabPane | [Canvas](#type-canvas) | false | — | the deselected tab's pane if set |
| ID | [GlobalId](../reference.md#type-globalid) | false | — | the ID of the deselected tab |
| tab | [Tab](#type-tab) | false | — | the deselected tab object (not tab button instance) |
| newTab | [Tab](#type-tab) | false | — | the tab object being selected |
| name | [TabName](../reference.md#type-tabname) | false | — | the name of the deselected tab |

### Returns

`[boolean](../reference.md#type-boolean)` — return false to cancel the tab deselection

---
## Method: TabSet.getTabObject

### Description
Get the tab Object originally passed to [TabSet.tabs](#attr-tabsettabs), by index, name or ID. If passed a tab Object, just returns it.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [int](../reference.md#type-int)|[GlobalId](../reference.md#type-globalid)|[TabName](../reference.md#type-tabname)|[Tab](#type-tab) | false | — | — |

### Returns

`[Tab](#type-tab)` — the tab, or null if not found

---
## Method: TabSet.setCanCloseTabs

### Description
Changes this TabSet's [canCloseTabs](#attr-tabsetcanclosetabs) property.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canCloseTabs | [boolean](../reference.md#type-boolean) | false | — | the new value for canCloseTabs. |

---
## Method: TabSet.addTab

### Description
Add a tab

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [Tab](#type-tab) | false | — | new tab |
| position | [number](#type-number) | true | — | position where tab should be added |

### See Also

- [TabSet.addTabs](#method-tabsetaddtabs)

**Flags**: A

---
## Method: TabSet.cancelTabTitleEditing

### Description
If the user is currently editing a tab title (see [TabSet.canEditTabTitles](#attr-tabsetcanedittabtitles)), dismiss the editor and discard the edit value entered by the user.

---
## Method: TabSet.hideTab

### Description
Hide a tab in this tabset at runtime. If the tab is selected, it will be deselected and the tab button will be hidden from the user.

Note that this does not remove a tab from the tabset entirely (see [TabSet.removeTab](#method-tabsetremovetab)) The tab will no longer be visible to the user or selectable by the user, but the configuration will still existing in the [tabs array](#attr-tabsettabs) for this tabSet. Developers should particularly be aware of this when calling methods that refer to tabs by index - the index includes both hidden and visible tabs in the tabset.

Tabs may be marked as hidden at init-time via [Tab.hidden](Tab.md#attr-tabhidden).

To test whether a tab is currently visible, use [TabSet.tabIsVisible](#method-tabsettabisvisible)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [Number](#type-number)|[String](#type-string)|[Tab](#type-tab) | false | — | Tab to hide |

---
## Method: TabSet.removeTab

### Description
Remove a tab.

The pane associated with the removed tab is automatically destroyed when you call this method. To avoid this, call [TabSet.updateTab](#method-tabsetupdatetab) with `null` as the new pane immediately before removing the tab, or set [TabSet.destroyPanes](#attr-tabsetdestroypanes) to false.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tabs | [Tab](#type-tab)|[GlobalId](../reference.md#type-globalid)|[TabName](../reference.md#type-tabname)|[number](#type-number)|[Array of Tab](#type-array-of-tab) | false | — | list of tabs, tabIDs, or tab numbers |

### See Also

- [TabSet.removeTabs](#method-tabsetremovetabs)

**Flags**: A

---
## Method: TabSet.editTabTitle

### Description
Places an editor in the title of the parameter tab and allows the user to edit the title. Note that this programmatic method will **always** allow editing of the specified tab's title, regardless of the settings of [TabSet.canEditTabTitles](#attr-tabsetcanedittabtitles) or [Tab.canEditTitle](Tab.md#attr-tabcanedittitle).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [Tab](#type-tab)|[String](#type-string)|[Integer](../reference_2.md#type-integer) | false | — | The tab whose title should be edited (may be specified by ID or index) |

### See Also

- [TabSet.canEditTabTitles](#attr-tabsetcanedittabtitles)
- [Tab.canEditTitle](Tab.md#attr-tabcanedittitle)

---
## Method: TabSet.scrollBack

### Description
If there is not enough space to display all the tabs in this tabSet, this method will scroll the previous tab (that first tab that is clipped at the beginning of the tab-bar) into view.

---
## Method: TabSet.setTabPickerTitle

### Description
Changes the title of the picker menu item of a tab

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [Tab](#type-tab)|[number](#type-number)|[GlobalId](../reference.md#type-globalid)|[TabName](../reference.md#type-tabname) | false | — | — |
| pickerTitle | [HTMLString](../reference.md#type-htmlstring) | false | — | new title |

**Flags**: A

---
## Method: TabSet.showTabContextMenu

### Description
Notification fired when the user right-clicks on a tab. Event may be cancelled by returning false

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tabSet | [TabSet](#type-tabset) | false | — | This tabset |
| tab | [Tab](#type-tab) | false | — | the tab object that recieved the context click event |

### Returns

`[boolean](../reference.md#type-boolean)` — return false to cancel default right-click behavior

---
## Method: TabSet.getSelectedTab

### Description
Returns the currently selected tab object. This is the object literal used to configure the tab, rather than the tab button widget.

### Returns

`[Tab](#type-tab)` — the currently selected Tab object

**Flags**: A

---
## Method: TabSet.setTabIcon

### Description
Changes the icon for a tab

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [Tab](#type-tab)|[number](#type-number)|[GlobalId](../reference.md#type-globalid)|[TabName](../reference.md#type-tabname) | false | — | tab to update |
| icon | [SCImgURL](../reference.md#type-scimgurl) | false | — | new icon |

**Flags**: A

---
## Method: TabSet.titleChanged

### Description
This notification method fired when the user changes the title of a tab in this TabSet. This can happen either through user interaction with the UI if [canEditTabTitles](#attr-tabsetcanedittabtitles) is set, or programmatically if application code calls [editTabTitle](#method-tabsetedittabtitle).

Return false from this method to cancel the change.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newTitle | [String](#type-string) | false | — | the new title |
| oldTitle | [String](#type-string) | false | — | the old title |
| tab | [Tab](#type-tab) | false | — | the tab whose title has changed |

### Returns

`[boolean](../reference.md#type-boolean)` — return false to suppress the title change

---
## Method: TabSet.removeTabs

### Description
Remove one or more tabs. The pane(s) associated with the removed tab(s) is automatically destroyed when you call this method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tabs | [Tab](#type-tab)|[GlobalId](../reference.md#type-globalid)|[TabName](../reference.md#type-tabname)|[number](#type-number) | false | — | list of tabs, tabIDs, tab names, or tab numbers |

### See Also

- [TabSet.removeTab](#method-tabsetremovetab)

**Flags**: A

---
## Method: TabSet.closeClick

### Description
When [TabSet.canCloseTabs](#attr-tabsetcanclosetabs) is set, method fired when the user clicks the "close" icon for a tab.

Default implementation will remove the tab from the tabSet via [TabSet.removeTab](#method-tabsetremovetab).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [Tab](#type-tab) | false | — | tab to close |

---
## Method: TabSet.tabsReordered

### Description
Notification method executed when one or more tabs in the TabSet are reordered.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tabCanvas | [StatefulCanvas](#type-statefulcanvas) | false | — | the live Canvas representing the tab that was moved |
| tabIndex | [Integer](../reference_2.md#type-integer) | false | — | the new index of the tab in the tabSet |

---
## Method: TabSet.getSelectedTabNumber

### Description
Returns the index of the currently selected tab object.

### Returns

`[number](#type-number)` — the index of the currently selected tab object

**Flags**: A

---
## Method: TabSet.getTabNumber

### Description
Get the index of a tab, from the tab, tab ID or tab name. If passed a number, just returns it. Note that the index returned will include [hidden tabs](Tab.md#attr-tabhidden) as well as visible tabs.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [number](#type-number)|[GlobalId](../reference.md#type-globalid)|[TabName](../reference.md#type-tabname)|[Tab](#type-tab) | false | — | — |

### Returns

`[number](#type-number)` — the index of the tab, or -1 if not found

---
## Method: TabSet.disableTab

### Description
If the specified tab is enabled, disable it now.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [Tab](#type-tab)|[number](#type-number)|[GlobalId](../reference.md#type-globalid)|[TabName](../reference.md#type-tabname) | false | — | — |

### See Also

- [Tab.disabled](Tab.md#attr-tabdisabled)

---
## Method: TabSet.setCanCloseTab

### Description
Sets the given tab's [canClose](Tab.md#attr-tabcanclose) property to the boolean parameter canClose. If canClose is null, this will have the effect of causing the tab to fall back on [TabSet.canCloseTabs](#attr-tabsetcanclosetabs).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [Tab](#type-tab)|[GlobalId](../reference.md#type-globalid)|[TabName](../reference.md#type-tabname)|[number](#type-number) | false | — | tab to change |
| canClose | [boolean](../reference.md#type-boolean) | false | — | new value for the tab's canClose property, or null to clear it |

---
## Method: TabSet.setTabTitle

### Description
Changes the title of a tab

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [Tab](#type-tab)|[number](#type-number)|[GlobalId](../reference.md#type-globalid)|[TabName](../reference.md#type-tabname) | false | — | — |
| title | [HTMLString](../reference.md#type-htmlstring) | false | — | new title |

**Flags**: A

---
## Method: TabSet.getPaneContainerEdges

### Description
If the paneContainer for this tab set is showing [edges](Canvas.md#attr-canvasshowedges), this method can be used to specify (dynamically) which [customEdges](Canvas.md#attr-canvascustomedges) to show. Called when the pane creator is created.

Default implementation will return null unless [showPartialEdges](#attr-tabsetshowpartialedges) is true, in which case it will return the three edges opposite the [tabBarPosition](#attr-tabsettabbarposition).

### Returns

`[Array](#type-array)` — array of custom edges to show

**Flags**: A

---
## Method: TabSet.getTabPane

### Description
Returns the pane for a given tab.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [Object](../reference.md#type-object)|[number](#type-number)|[GlobalId](../reference.md#type-globalid)|[TabName](../reference.md#type-tabname)|[Tab](#type-tab) | false | — | — |

### Returns

`[Canvas](#type-canvas)` — the tab pane

---
## Method: TabSet.revealChild

### Description
Reveals the child Canvas passed in by selecting the tab containing that child if it is not already selected. If no tab in this TabSet contains the passed-in Canvas, this method has no effect

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| child | [GlobalId](../reference.md#type-globalid)|[Canvas](#type-canvas) | false | — | the child Canvas to reveal, or its global ID |

---
## Method: TabSet.showTab

### Description
Show a [hidden tab](Tab.md#attr-tabhidden) at runtime.

To test whether a tab is currently visible, use [TabSet.tabIsVisible](#method-tabsettabisvisible)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [Number](#type-number)|[String](#type-string)|[Tab](#type-tab) | false | — | Tab to hide |

---
## Method: TabSet.setTabProperties

### Description
Apply properties to an existing tab in a tabSet.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [Tab](#type-tab)|[number](#type-number)|[GlobalId](../reference.md#type-globalid)|[TabName](../reference.md#type-tabname) | false | — | Identifier for the tab to be modified |
| properties | [Object](../reference.md#type-object) | false | — | Javascript object containing the set of properties to be applied to the tab. |

**Flags**: A

---
## Method: TabSet.removeLastTab

### Description
Removes the last tab in the TabSet, excluding the [TabSet.moreTab](#attr-tabsetmoretab) if present.

---
## Method: TabSet.setTabPane

### Description
Apply a new [pane](Tab.md#attr-tabpane) to an existing tab in this tabSet

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [number](#type-number)|[String](#type-string)|[Tab](#type-tab) | false | — | Tab to update (may be referenced by ID or index) |
| pane | [Canvas](#type-canvas) | false | — | new Pane for the tab |

---
## Method: TabSet.reorderTab

### Description
Move a tab to another location in the tabset.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [Tab](#type-tab)|[GlobalId](../reference.md#type-globalid)|[TabName](../reference.md#type-tabname)|[number](#type-number) | false | — | tab to move |
| moveToPosition | [number](#type-number) | true | — | the index to move the tab to - defaults to the end of the tabset if not passed |

---
## Method: TabSet.enableTab

### Description
If the specified tab is disabled, enable it now.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [Tab](#type-tab)|[number](#type-number)|[GlobalId](../reference.md#type-globalid)|[TabName](../reference.md#type-tabname) | false | — | — |

### See Also

- [Tab.disabled](Tab.md#attr-tabdisabled)

---
## Method: TabSet.tabForPane

### Description
Search for a tab that contains a pane.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pane | [Canvas](#type-canvas) | false | — | pane to show |

### Returns

`[Tab](#type-tab)` — tab that contains passed pane

---
## Method: TabSet.addTabClicked

### Description
Click handler applied to the [TabSet.addTabButton](#attr-tabsetaddtabbutton).

The default implementation will invoke [TabSet.addTabClick](#method-tabsetaddtabclick)

**Deprecated**

---
## Method: TabSet.addTabs

### Description
Add one or more tabs

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tabs | [Tab](#type-tab)|[Array of Tab](#type-array-of-tab) | false | — | new tab or tabs |
| position | [number](#type-number) | false | — | position where tab should be added (or array of positions) |

### See Also

- [TabSet.addTab](#method-tabsetaddtab)

**Flags**: A

---
## Method: TabSet.scrollForward

### Description
If there is not enough space to display all the tabs in this tabSet, this method will scroll the next tab (that first tab that is clipped at the end of the tab-bar) into view.

---
## Method: TabSet.getTab

### Description
Get the live Canvas representing a tab by index, ID, reference, or name. If passed a tab Canvas, just returns it.

Note that live Tab instances are not available until [draw()](Canvas.md#method-canvasdraw).

The returned Tab is considered an internal component of the TabSet. In order to maximize forward compatibility, manipulate tabs through APIs such as a [TabSet.setTabTitle](#method-tabsetsettabtitle) instead. Also note that a super-lightweight TabSet implementation may not use a separate Canvas per Tab, and code that accesses and manipulates Tabs as Canvases won't be compatible with that implementation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [int](../reference.md#type-int)|[GlobalId](../reference.md#type-globalid)|[TabName](../reference.md#type-tabname)|[Canvas](#type-canvas) | false | — | identifier for the tab or tab button |

### Returns

`[StatefulCanvas](#type-statefulcanvas)` — the tab Canvas, or null if not found or TabSet not drawn yet

---
## Method: TabSet.updateTab

### Description
Set the pane for a tab.

Pass in the index of a tab (or a tab object), and a new pane.

NOTE: the old pane for the tab is not destroy()d

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [number](#type-number)|[GlobalId](../reference.md#type-globalid)|[TabName](../reference.md#type-tabname)|[Tab](#type-tab) | false | — | tab to update |
| pane | [Canvas](#type-canvas)|[ID](#type-id) | false | — | new pane for the tab |

---
## Method: TabSet.tabSelected

### Description
Notification fired when a tab is selected. Note that this will only fire if this tabSet is drawn. If a tab is selected before [draw()](Canvas.md#method-canvasdraw) is called, the `tabSelected()` notification will fire on `draw()`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tabNum | [Integer](../reference_2.md#type-integer) | false | — | the index of the newly selected tab |
| tabPane | [Canvas](#type-canvas) | false | — | the newly selected tab's pane if set |
| ID | [GlobalId](../reference.md#type-globalid) | false | — | the ID of the newly selected tab |
| tab | [Tab](#type-tab) | false | — | the tab object (not tab button instance) |
| name | [TabName](../reference.md#type-tabname) | false | — | the name of the newly selected tab |

---
## Method: TabSet.addTabClick

### Description
Notification method fired when the user clicks the [TabSet.addTabButton](#attr-tabsetaddtabbutton).

No default implementation.

---
## Method: TabSet.tabIsVisible

### Description
Is the tab [hidden or visible](Tab.md#attr-tabhidden)?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [Number](#type-number)|[String](#type-string)|[Tab](#type-tab) | false | — | Tab to test |

### Returns

`[boolean](../reference.md#type-boolean)` — returns true if the tab has not been hidden.

---
## Method: TabSet.saveTabTitle

### Description
If the user is currently editing a tab title (see [TabSet.canEditTabTitles](#attr-tabsetcanedittabtitles)), save the edited tab title and hide the editor.

---
## Method: TabSet.selectTab

### Description
Select a tab. Note that this method will have no effect if the tab is [hidden](Tab.md#attr-tabhidden).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tab | [number](#type-number)|[GlobalId](../reference.md#type-globalid)|[TabName](../reference.md#type-tabname)|[Tab](#type-tab) | false | — | tab to select |

---
