# Tab Documentation

[← Back to API Index](../main.md)

---

## Attr: Tab.pane

### Description
Specifies the pane associated with this tab. You have three options for the value of the pane attribute:

*   **ID** - The global ID of an already created Canvas (or subclass).
*   **Canvas** - A live instance of a Canvas (or subclass).
*   **AutoChildShortcut** - String with format "autoChild:_autoChildName_"

You can change the pane associated with a given tab after the TabSet has been created by calling [TabSet.updateTab](TabSet.md#method-tabsetupdatetab).

### See Also

- [autoChildren](../kb_topics/autoChildren.md#kb-topic-autochildren)
- [TabSet.updateTab](TabSet.md#method-tabsetupdatetab)

**Flags**: IR

---
## Attr: Tab.prompt

### Description
Specifies the prompt to be displayed when the mouse hovers over the tab.

After the TabSet has been created, you can change a tab's `prompt` property by calling [TabSet.setTabProperties](TabSet.md#method-tabsetsettabproperties).

**Flags**: IR

---
## Attr: Tab.visibleWhen

### Description
Criteria to be evaluated to determine whether this Tab should be visible.

A basic criteria uses textMatchStyle:"exact". When specified in [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml) this property allows [shorthand formats](../kb_topics/xmlCriteriaShorthand.md#kb-topic-xmlcriteriashorthand) for defining criteria.

### Groups

- ruleCriteria

**Flags**: IR

---
## Attr: Tab.canClose

### Description
Determines whether this tab should show a close icon allowing the user to dismiss the tab by clicking on the close icon directly. The URL for the close icon's image will be derived from [TabSet.closeTabIcon](TabSet.md#attr-tabsetclosetabicon) by default, but may be overridden by explicitly specifying [Tab.closeIcon](#attr-tabcloseicon).

If unset or null, this property is derived from [TabSet.canCloseTabs](TabSet.md#attr-tabsetcanclosetabs).

Note that setting `canClose` means that [Tab.icon](#attr-tabicon) cannot be used, because it's used for the [closeIcon](#attr-tabcloseicon) - see [TabSet.canCloseTabs](TabSet.md#attr-tabsetcanclosetabs) for a workaround.

After the TabSet has been created, you can change a tab's `canClose` property by calling [TabSet.setCanCloseTab](TabSet.md#method-tabsetsetcanclosetab).

### See Also

- [TabSet.closeClick](TabSet.md#method-tabsetcloseclick)

**Flags**: IR

---
## Attr: Tab.paneMargin

### Description
Space to leave around the pane within this Tab. If specified, this property takes precedence over [TabSet.paneMargin](TabSet.md#attr-tabsetpanemargin)

**Flags**: IR

---
## Attr: Tab.ID

### Description
Optional ID for the tab, which can later be used to reference the tab. APIs requiring a reference to a tab will accept the tab's ID \[including [TabSet.selectTab](TabSet.md#method-tabsetselecttab), [TabSet.updateTab](TabSet.md#method-tabsetupdatetab), [TabSet.removeTab](TabSet.md#method-tabsetremovetab)\].  
The ID will also be passed to the [TabSet.tabSelected](TabSet.md#method-tabsettabselected) and [TabSet.tabDeselected](TabSet.md#method-tabsettabdeselected) handler functions, if specified.

Note that if you provide an ID, it must be globally unique. If you do not want a globally unique identifier, set [Tab.name](#attr-tabname) instead.

**Flags**: IR

---
## Attr: Tab.iconHeight

### Description
If [Tab.icon](#attr-tabicon) is specified, this property may be used to specify a height for the icon.

After the TabSet has been created, you can change a tab's `iconHeight` property by calling [TabSet.setTabProperties](TabSet.md#method-tabsetsettabproperties).

**Flags**: IR

---
## Attr: Tab.iconWidth

### Description
If [Tab.icon](#attr-tabicon) is specified, this property may be used to specify a width for the icon.

After the TabSet has been created, you can change a tab's `iconWidth` property by calling [TabSet.setTabProperties](TabSet.md#method-tabsetsettabproperties).

**Flags**: IR

---
## Attr: Tab.hidden

### Description
If specified this tab will be hidden by default. To show and hide tabs at runtime use [TabSet.showTab](TabSet.md#method-tabsetshowtab) and [TabSet.hideTab](TabSet.md#method-tabsethidetab)

**Flags**: IRW

---
## Attr: Tab.canAdaptWidth

### Description
If enabled, the tab will collapse to show just its icon when showing the title would cause overflow of a containing [TabBar](TabBar.md#class-tabbar). While collapsed, the tab will show its title on hover, unless an explicit hover has been specified such as by [Tab.prompt](#attr-tabprompt).

### See Also

- [Button.canAdaptWidth](Button.md#attr-buttoncanadaptwidth)
- [Canvas.canAdaptWidth](Canvas.md#attr-canvascanadaptwidth)

**Flags**: IR

---
## Attr: Tab.disabled

### Description
If specified, this tab will initially be rendered in a disabled state. To enable or disable tabs on the fly use the [TabSet.enableTab](TabSet.md#method-tabsetenabletab), and [TabSet.disableTab](TabSet.md#method-tabsetdisabletab). methods.

**Flags**: IR

---
## Attr: Tab.icon

### Description
If specified, this tab will show an icon next to the tab title.

**NOTE:** if you enable [closeable tabs](TabSet.md#attr-tabsetcanclosetabs), `tab.icon` is used for the close icon. [TabSet.canCloseTabs](TabSet.md#attr-tabsetcanclosetabs) describes a workaround to enable both a `closeIcon` and a second icon to be shown.

Use [TabSet.tabIconClick](TabSet.md#method-tabsettabiconclick) to add an event handler specifically for clicks on the icon.

If a tab [becomes disabled](#attr-tabdisabled), a different icon will be loaded by adding a suffix to the image name (see [Button.icon](Button.md#attr-buttonicon)).

You should specify a size for the icon via [Tab.iconSize](#attr-tabiconsize) or [Tab.iconWidth](#attr-tabiconwidth) and [Tab.iconHeight](#attr-tabiconheight). Without an explicitly specified size, tabs may be drawn overlapping or with gaps the first time a page is loaded, because the icon is not cached and therefore its size isn't known.

After the TabSet has been created, you can change a tab's `icon` property by calling [TabSet.setTabIcon](TabSet.md#method-tabsetsettabicon).

### See Also

- [TabSet.tabIconClick](TabSet.md#method-tabsettabiconclick)

**Flags**: IR

---
## Attr: Tab.iconSize

### Description
If [Tab.icon](#attr-tabicon) is specified, this property may be used to specify a size for the icon. Per side sizing may be specified instead via [Tab.iconWidth](#attr-tabiconwidth) and [Tab.iconHeight](#attr-tabiconheight).

After the TabSet has been created, you can change a tab's `iconSize` property by calling [TabSet.setTabProperties](TabSet.md#method-tabsetsettabproperties).

**Flags**: IR

---
## Attr: Tab.pickerTitle

### Description
If [TabSet.showTabPicker](TabSet.md#attr-tabsetshowtabpicker) is true for this TabSet, if set this property will determine the title of the picker menu item for this tab. If unset, [Tab.title](#attr-tabtitle) will be used instead.

After the TabSet has been created, you can change a tab's `pickerTitle` property by calling [TabSet.setTabProperties](TabSet.md#method-tabsetsettabproperties).

### Groups

- tabBarControls

### See Also

- [TabSet.showTabPicker](TabSet.md#attr-tabsetshowtabpicker)
- [Tab.title](#attr-tabtitle)

**Flags**: IR

---
## Attr: Tab.canEditTitle

### Description
If specified, overrides the [TabSet.canEditTabTitles](TabSet.md#attr-tabsetcanedittabtitles) setting, for this one tab only.

Note that the TabSet's [titleEditEvent](TabSet.md#attr-tabsettitleeditevent) must be set to a supported [TabTitleEditEvent](../main.md#type-tabtitleeditevent) in order for users to be able to edit this tab's title.

After the TabSet has been created, you can change a tab's `canEditTtile` property by calling [TabSet.setTabProperties](TabSet.md#method-tabsetsettabproperties).

### See Also

- [TabSet.canEditTabTitles](TabSet.md#attr-tabsetcanedittabtitles)

**Flags**: IR

---
## Attr: Tab.name

### Description
Optional name for the tab, which can later be used to reference the tab. APIs requiring a reference to a tab will accept the tab's name \[including [TabSet.selectTab](TabSet.md#method-tabsetselecttab), [TabSet.updateTab](TabSet.md#method-tabsetupdatetab), [TabSet.removeTab](TabSet.md#method-tabsetremovetab)\].  
This name will also be passed to the [TabSet.tabSelected](TabSet.md#method-tabsettabselected) and [TabSet.tabDeselected](TabSet.md#method-tabsettabdeselected) handler functions, if specified.

This identifier is requred to be locally unique to the TabSet and cannot be used to get a global reference to the Tab. If you want a global reference, set [Tab.ID](#attr-tabid) instead.

**Flags**: IR

---
## Attr: Tab.canReorder

### Description
If [TabSet.canReorderTabs](TabSet.md#attr-tabsetcanreordertabs) is set to `true`, setting `canReorder` explicitly to `false` for some tab will disallow drag-reordering of this tab. Has no effect if `canReorderTabs` is not true at the tabSet level.

Note that this setting also disallows a reorder of another tab into the slot before or following this tab. This means for tabs located at the beginning or end of the tab-bar, users cannot changing the index of the tab by dropping another before or after it. However if you have a _`canReorder:false`_ tab which is not at the beginning or end of the tab bar, users can drag reorder other tabs around it which may ultimately change its position.

### See Also

- [TabSet.canReorderTabs](TabSet.md#attr-tabsetcanreordertabs)

**Flags**: IR

---
## Attr: Tab.title

### Description
Specifies the title of the this tab. To change the title after the TabSet has been created, call [TabSet.setTabTitle](TabSet.md#method-tabsetsettabtitle).

### See Also

- [TabSet.setTabTitle](TabSet.md#method-tabsetsettabtitle)

**Flags**: IR

---
## Attr: Tab.closeIconSize

### Description
Size of the [Tab.closeIcon](#attr-tabcloseicon) for this tab. If unspecified the icon will be sized according to [TabSet.closeTabIconSize](TabSet.md#attr-tabsetclosetabiconsize)

**Flags**: IR

---
## Attr: Tab.closeIcon

### Description
Custom src for the close icon for this tab to display if it is closeable. See [Tab.canClose](#attr-tabcanclose) and [TabSet.canCloseTabs](TabSet.md#attr-tabsetcanclosetabs).

**Flags**: IR

---
## Attr: Tab.width

### Description
You can specify an explicit width for the tab using this property. Note that tabs automatically size to make room for the full title, but if you want to e.g. specify a uniform width for all tabs in a TabSet, this property enables you to do so.

After the TabSet has been created, you can change a tab's `width` property by calling [TabSet.setTabProperties](TabSet.md#method-tabsetsettabproperties).

**Flags**: IR

---
## Attr: Tab.enableWhen

### Description
Criteria to be evaluated to determine whether this Tab should be enabled.

A basic criteria uses textMatchStyle:"exact". When specified in [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml) this property allows [shorthand formats](../kb_topics/xmlCriteriaShorthand.md#kb-topic-xmlcriteriashorthand) for defining criteria.

### Groups

- ruleCriteria

**Flags**: IR

---
## Method: Tab.tabDeselected

### Description
Optional handler to fire when a tab is deselected. Returning false will cancel the new selection, leaving this tab selected. As with [TabSet.tabSelected](TabSet.md#method-tabsettabselected) this method only fires when the tabset is drawn.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tabSet | [TabSet](#type-tabset) | false | — | the tabSet containing the tab. |
| tabNum | [Integer](../main_2.md#type-integer) | false | — | the index of the deselected tab |
| tabPane | [Canvas](#type-canvas) | false | — | the deselected tab's pane if set |
| ID | [GlobalId](../main.md#type-globalid) | false | — | the ID of the deselected tab |
| tab | [Tab](#type-tab) | false | — | the deselected tab object (not tab button instance) |
| newTab | [Tab](#type-tab) | false | — | the tab object being selected |
| name | [TabName](../main.md#type-tabname) | false | — | the name of the deselected tab |

### Returns

`[boolean](../main.md#type-boolean)` — return `false` to cancel the tab selection

### See Also

- [Tab.tabSelected](#method-tabtabselected)

---
## Method: Tab.tabSelected

### Description
Optional handler to fire when a tab is selected. As with [TabSet.tabSelected](TabSet.md#method-tabsettabselected) this method only fires when the tabset is drawn.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tabSet | [TabSet](#type-tabset) | false | — | the tabSet containing the tab. |
| tabNum | [Integer](../main_2.md#type-integer) | false | — | the index of the newly selected tab |
| tabPane | [Canvas](#type-canvas) | false | — | the newly selected tab's pane if set |
| ID | [GlobalId](../main.md#type-globalid) | false | — | the ID of the newly selected tab |
| tab | [Tab](#type-tab) | false | — | the tab object (not tab button instance) |
| name | [TabName](../main.md#type-tabname) | false | — | the name of the newly selected tab |

### See Also

- [Tab.tabDeselected](#method-tabtabdeselected)

---
