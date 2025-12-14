# SectionHeader Documentation

[← Back to API Index](../reference.md)

---

## Class: SectionHeader

*Inherits from:* [Label](Label.md#class-label)

### Description
Simple SectionHeader class based on a Label with an icon, skinnable via CSS.

---
## Attr: SectionHeader.baseStyle

### Description
CSS class for the section header.

**Flags**: IRA

---
## Attr: SectionHeader.showClippedTitleOnHover

### Description
If true and the title is clipped, then a hover containing the full title of this section header is enabled.

### Groups

- hovers

**Flags**: IRW

---
## Attr: SectionHeader.noDoubleClicks

### Description
By default doubleClicks are disabled for SectionHeaders. All mouse click events will be handled as single clicks. Set this property to `false` to enable standard double-click handling.

**Flags**: IRA

---
## Attr: SectionHeader.icon

### Description
Base filename of the icon that represents open and closed states. The default settings also change the icon for disabled sections, so a total of four images are required (opened, closed, Disabled\_opened, Disabled\_closed).

Not shown if [SectionStackSection.canCollapse](SectionStackSection.md#attr-sectionstacksectioncancollapse) is false.

**Flags**: IRA

---
## Attr: SectionHeader.title

### Description
Title to show for the section

**Flags**: IRW

---
## Attr: SectionHeader.clipTitle

### Description
If the title for this section header is too large for the available space, should the title be clipped?

This feature is supported only in browsers that support the CSS UI text-overflow property (IE6+, Firefox 7+, Safari, Chrome, Opera 9+).

**Flags**: IR

---
## Attr: SectionHeader.controls

### Description
Custom controls to be shown on top of this section header.

These controls are shown in the [SectionHeader.controlsLayout](#attr-sectionheadercontrolslayout).

Note that this is an init-time property. If you need to dynamically change what controls are displayed to the user, we would recommend embedding the controls in a Layout or similar container. This will allow you to show/hide or add/remove members at runtime by manipulating the existing control(s) set up at init time.

**Flags**: IR

---
## Attr: SectionHeader.controlsLayout

### Description
A [Layout](Layout.md#class-layout) containing specified [SectionHeader.controls](#attr-sectionheadercontrols) if any. Sets [Layout.membersMargin](Layout.md#attr-layoutmembersmargin):5, [Layout.defaultLayoutAlign](Layout.md#attr-layoutdefaultlayoutalign):"center", and RTL-sensitive [Layout.align](Layout.md#attr-layoutalign) (right by default).

**Flags**: IR

---
## Attr: SectionHeader.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Method: SectionHeader.getSectionStack

### Description
For a SectionHeader embedded in a SectionStack, this method will return a pointer to the [SectionStack](SectionStack.md#class-sectionstack) in which this section header is embedded.

### Returns

`[SectionStack](#type-sectionstack)` — Section Stack containing this section header

---
## Method: SectionHeader.titleClipped

### Description
Is the title of this section header clipped by [section controls](#attr-sectionheadercontrols) or the edge of the header?

### Returns

`[boolean](../reference.md#type-boolean)` — whether the title is clipped.

### See Also

- [SectionHeader.clipTitle](#attr-sectionheadercliptitle)

**Flags**: A

---
## Method: SectionHeader.titleHover

### Description
Optional stringMethod to fire when the user hovers over this section header and the title is clipped. If [SectionHeader.showClippedTitleOnHover](#attr-sectionheadershowclippedtitleonhover) is true, the default behavior is to show a hover canvas containing the HTML returned by [SectionHeader.titleHoverHTML](#method-sectionheadertitlehoverhtml). Return false to suppress this default behavior.

### Returns

`[boolean](../reference.md#type-boolean)` — false to suppress the standard hover

### Groups

- hovers

### See Also

- [SectionHeader.clipTitle](#attr-sectionheadercliptitle)
- [SectionHeader.titleClipped](#method-sectionheadertitleclipped)

---
## Method: SectionHeader.titleHoverHTML

### Description
Returns the HTML that is displayed by the default [titleHover](#method-sectionheadertitlehover) handler. Return null or an empty string to cancel the hover.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| defaultHTML | [HTMLString](../reference.md#type-htmlstring) | false | — | the HTML that would have been displayed by default |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML to be displayed in the hover. If an empty string, then the hover is canceled. If null, then the default HTML is used.

---
