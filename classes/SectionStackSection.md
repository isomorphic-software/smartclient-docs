# SectionStackSection Documentation

[← Back to API Index](../reference.md)

---

## Attr: SectionStackSection.resizeable

### Description
If set to false, then the items in this section will not be resized by sectionHeader repositioning. You may also set this flag directly on any of the items in any section to cause that item to not be resizeable.

**Flags**: I

---
## Attr: SectionStackSection.canClose

### Description
Is this section closeable?

Closeable sections show a [SectionStack.closeSectionButton](SectionStack.md#attr-sectionstackclosesectionbutton) which will invoke [SectionStack.closeSection](SectionStack.md#method-sectionstackclosesection) when clicked.

This property overrides the default [SectionStack.canCloseSections](SectionStack.md#attr-sectionstackcanclosesections) setting.

**Flags**: IR

---
## Attr: SectionStackSection.expanded

### Description
Sections default to the collapsed state unless [SectionStackSection.showHeader](#attr-sectionstacksectionshowheader) is set to `false` in which case they default to the expanded state. This attribute allows you to explicitly control the expand/collapse state of the section by overriding the above default behavior.

**Flags**: I

---
## Attr: SectionStackSection.destroyOnRemove

### Description
Should the [SectionStackSection.items](#attr-sectionstacksectionitems) be [destroyed](Canvas.md#method-canvasdestroy) if this section is [removed](SectionStack.md#method-sectionstackremovesection)? The section header itself and any controls will always be destroyed.

**Flags**: I

---
## Attr: SectionStackSection.headerProperties

### Description
Allows properties for the header (a [SectionHeader](SectionHeader.md#class-sectionheader) or [ImgSectionHeader](ImgSectionHeader.md#class-imgsectionheader) subclass) to be set on the section before it's added to the [SectionStack](SectionStack.md#class-sectionstack).

### See Also

- [SectionStack.sectionHeaderClass](SectionStack.md#attr-sectionstacksectionheaderclass)

**Flags**: IR

---
## Attr: SectionStackSection.showHeader

### Description
If true, a header will be shown for this section. If false, no header will be shown.

**Flags**: I

---
## Attr: SectionStackSection.canTabToHeader

### Description
If true, the header for this Section will be included in the page's tab order for accessibility. May also be set at the [SectionStack](SectionStack.md#class-sectionstack) level via [SectionStack.canTabToHeaders](SectionStack.md#attr-sectionstackcantabtoheaders).

See [accessibility](../kb_topics/accessibility.md#kb-topic-accessibility--section-508-compliance).

**Flags**: IR

---
## Attr: SectionStackSection.icon

### Description
Base filename of the icon that represents open and closed states. The default settings also change the icon for disabled sections, so a total of four images are required (opened, closed, Disabled\_opened, Disabled\_closed).

Not shown if [SectionStackSection.canCollapse](#attr-sectionstacksectioncancollapse) is false.

**Flags**: IR

---
## Attr: SectionStackSection.ID

### Description
Optional ID for the section. If [SectionStack.useGlobalSectionIDs](SectionStack.md#attr-sectionstackuseglobalsectionids) is true, this property will be applied to the generated SectionStackHeader widget as a standard widget ID, meaning it should be unique within a page.

**Backcompat Note**: Section stack sections may be uniquely identified within a stack via the [SectionStackSection.name](#attr-sectionstacksectionname) attribute (introduced in Jan 2010). Prior to this, the section ID attribute was used in this way (and would not be applied to the section header as a widget ID). For backwards compatibility this is still supported: If `section.name` is unspecified for a section but `section.ID` is set, the ID will be used as a default name attribute for the section. For backwards compatibility we also disable the standard behavior of having the `section.ID` being applied to the generated section header (thereby avoiding the page-level uniqueness requirement) by defaulting [SectionStack.useGlobalSectionIDs](SectionStack.md#attr-sectionstackuseglobalsectionids) to false.

**Flags**: IR

---
## Attr: SectionStackSection.clipTitle

### Description
If the title for this section header is too large for the available space, should the title be clipped?

This feature is supported only in browsers that support the CSS UI text-overflow property (IE6+, Firefox 7+, Safari, Chrome, Opera 9+).

**Flags**: IR

---
## Attr: SectionStackSection.canDropBefore

### Description
When explicitly set to false, disallows drop before this member in the Layout.

### Groups

- layoutMember

### See Also

- [Layout](Layout.md#class-layout)

**Flags**: I

---
## Attr: SectionStackSection.hidden

### Description
Sections default to the visible state. This attribute allows you to explicitly control the visible/hidden state of the section by overriding the above default behavior.

**Flags**: I

---
## Attr: SectionStackSection.showClippedTitleOnHover

### Description
If true and the title is clipped, then a hover containing the full title of this section header is enabled.

### Groups

- hovers

**Flags**: IRW

---
## Attr: SectionStackSection.closeIcon

### Description
Icon src for the [close button](SectionStack.md#attr-sectionstackclosesectionbutton) if [canClose](#attr-sectionstacksectioncanclose) is true.

If specified this takes precedence over [SectionStack.closeSectionIcon](SectionStack.md#attr-sectionstackclosesectionicon).

**Flags**: IR

---
## Attr: SectionStackSection.name

### Description
Identifier for the section. This can be used later in calls to [SectionStack](SectionStack.md#class-sectionstack) APIs such as [SectionStack.expandSection](SectionStack.md#method-sectionstackexpandsection) and [SectionStack.collapseSection](SectionStack.md#method-sectionstackcollapsesection). Note that if no name is specified for the section, one will be auto-generated when the section is created. This property should be a string which may be used as a valid JavaScript identifier (should start with a letter and not contain space or special characters such as "\*").

**Flags**: IR

---
## Attr: SectionStackSection.canCollapse

### Description
This attribute controls whether or not the expand/collapse UI control is shown on the header of this section. Any section can still be expanded/collapsed programmatically, regardless of this setting.

**Flags**: I

---
## Attr: SectionStackSection.controls

### Description
Custom controls to be shown on top of this section header.

These controls are shown in the [SectionHeader.controlsLayout](SectionHeader.md#attr-sectionheadercontrolslayout).

Note that this is an init-time property. If you need to dynamically change what controls are displayed to the user, we would recommend embedding the controls in a Layout or similar container. This will allow you to show/hide or add/remove members at runtime by manipulating the existing control(s) set up at init time.

For [canClose:true](#attr-sectionstacksectioncanclose) sections, a [close icon](SectionStack.md#attr-sectionstackclosesectionbutton) will be added to the section controls automatically.

**Flags**: IR

---
## Attr: SectionStackSection.closeIconSize

### Description
Pixel width/height for this sections [SectionStackSection.closeIcon](#attr-sectionstacksectioncloseicon).  
If unset [SectionStack.closeSectionIconSize](SectionStack.md#attr-sectionstackclosesectioniconsize) will be used.

**Flags**: IR

---
## Attr: SectionStackSection.title

### Description
Title to show for the section

**Flags**: IR

---
## Attr: SectionStackSection.canReorder

### Description
If set to false, then this sectionHeader will not be able to be dragged to perform a drag reorder, if [SectionStack.canReorderSections](SectionStack.md#attr-sectionstackcanreordersections) is true. You can also disable dropping other sections before this one by setting [canDropBefore](Canvas.md#attr-canvascandropbefore) to false.

**Flags**: I

---
## Attr: SectionStackSection.items

### Description
List of Canvases that constitute the section. These Canvases will be shown and hidden together.

Along with live Canvases, you may also pass special string autochild shortcuts of the form "autoChild:_autoChildName_" as discussed at the bottom of help topic [autoChildren](../kb_topics/autoChildren.md#kb-topic-autochildren).

**Flags**: I

---
