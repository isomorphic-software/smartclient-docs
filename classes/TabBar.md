# TabBar Documentation

[← Back to API Index](../reference.md)

---

## Class: TabBar

*Inherits from:* [Toolbar](Toolbar.md#class-toolbar)

### Description
Shows a set of Tabs. TabBars are automatically created by TabSets and shouldn't be used directly. The TabBar is documented for skinning purposes.

---
## Attr: TabBar.moreTab

### Description
Tab to show as the "more" tab when [TabBar.showMoreTab](#attr-tabbarshowmoretab) is enabled and the number of tabs to show exceeds [TabBar.moreTabCount](#attr-tabbarmoretabcount).

**Flags**: IR

---
## Attr: TabBar.baseLineCapSize

### Description
Set [StretchImg.capSize](StretchImg.md#attr-stretchimgcapsize) for the [baseLine](../reference.md#kb-topic-baseline) stretchImg.

### Groups

- baseLine

**Flags**: IR

---
## Attr: TabBar.moreTabCount

### Description
This property defines the number tab buttons that should be shown before automatically adding a "more" button to handle the remaining tabs. This property is only used when [TabBar.showMoreTab](#attr-tabbarshowmoretab) is enabled.

**Flags**: IR

---
## Attr: TabBar.baseLineSrc

### Description
Sets [StretchImg.src](StretchImg.md#attr-stretchimgsrc) for the [baseLine](../reference.md#kb-topic-baseline) StretchImg.

### Groups

- baseLine

**Flags**: IR

---
## Attr: TabBar.breadth

### Description
Breadth of the tabBar (including baseline breadth)

**Flags**: IRW

---
## Attr: TabBar.tabs

### Description
Tab for this TabBar.

**Flags**: IR

---
## Attr: TabBar.showMoreTab

### Description
Should tabs exceeding [TabBar.moreTabCount](#attr-tabbarmoretabcount) be shown on a "more" tab?

This setting is used to emulate an iPhone-style tab bar "more" button.

**Flags**: IR

---
## Attr: TabBar.buttonConstructor

### Description
SmartClient component used for the tabs of the tabBar. Must be Button or Button subclass.

**Flags**: AIRW

---
## Attr: TabBar.defaultTabSize

### Description
Default size (length) in pixels for tabs within this tabBar

**Flags**: IR

---
## Attr: TabBar.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: TabBar.closeTabKeys

### Description
An array of shortcut keyboard commands which will close the currently selected tab, if the currently selected tab is closeable. Either this `TabBar` or the currently selected tab must have keyboard focus.

By default, this is an array of two `KeyIdentifier`s: `Alt+Delete`, which is the keyboard command recommended by [WAI-ARIA Authoring Practices](http://www.w3.org/WAI/PF/aria-practices/#tabpanel) and [DHTML Style Guide Working Group](http://access.aol.com/dhtml-style-guide-working-group/#tabpanel), and `Ctrl+W`. Notes:

*   On Mac, the `Alt+Delete` keyboard command is accomplished via `Fn-Option-Delete`.
*   `Alt+Delete` is a [JAWS Keystroke](http://doccenter.freedomscientific.com/doccenter/archives/training/jawskeystrokes.htm) to "Say Active Cursor". If using JAWS, pressing `Alt+Shift+Delete` will close the tab.
*   In Chrome, Firefox, and Internet Explorer on Windows, `Ctrl+W` will also close the browser tab/window if focus is not within a `TabBar`. If `Ctrl+W` will be used frequently by the application's users, it may be useful to [register this key](Page.md#classmethod-pageregisterkey) to cancel it by default:
    ```
    isc.Page.registerKey({ctrlKey: true, keyName: "W"}, "return false");
    ```

**Flags**: IRA

---
## Attr: TabBar.baseLineThickness

### Description
Thickness of the baseLine, in pixels. This should be set to match the media specified by [TabBar.baseLineSrc](#attr-tabbarbaselinesrc). The baseLineThickness also determines the degree of overlap with the TabSet's paneContainer when using decorative edges - see [TabSet.paneContainer](TabSet.md#attr-tabsetpanecontainer) for details.

### Groups

- baseLine

**Flags**: IR

---
## Method: TabBar.selectTab

### Description
Select a tab

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tabNum | [number](#type-number) | false | — | index of tab to select |

---
