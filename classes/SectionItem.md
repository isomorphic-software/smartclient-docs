# SectionItem Documentation

[← Back to API Index](../main.md)

---

## Class: SectionItem

*Inherits from:* [CanvasItem](CanvasItem.md#class-canvasitem)

### Description
Header item for a collapsible section in a [DynamicForm](DynamicForm.md#class-dynamicform). Each `SectionItem` is associated with a number of other `item`s in the form, which will be shown or hidden as a group when the section is expanded or collapsed. Clicking on a `SectionItem` will expand or collapse the section.

To make a form where only one section is expanded at a time, set [DynamicForm.sectionVisibilityMode](DynamicForm.md#attr-dynamicformsectionvisibilitymode) to "mutex".

### See Also

- [DynamicForm.sectionVisibilityMode](DynamicForm.md#attr-dynamicformsectionvisibilitymode)

---
## Attr: SectionItem.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: SectionItem.canCollapse

### Description
Whether this section header can be collapsed. If set false, suppresses open/close state icon

**Flags**: IR

---
## Attr: SectionItem.sectionExpanded

### Description
Whether this form section should be initially collapsed. Can be set programmatically via [SectionItem.expandSection](#method-sectionitemexpandsection) and [SectionItem.collapseSection](#method-sectionitemcollapsesection).

**Flags**: IR

---
## Attr: SectionItem.sectionHeaderClass

### Description
Name of the Canvas subclass to use as a header that labels the section and allows showing and hiding. The default class be skinned, or trivial subclasses created to allow different appearances for SectionItems in different forms. Very advanced developers can use the following information to create custom header classes.

**Flags**: IRA

---
## Attr: SectionItem.sectionVisible

### Description
Whether this form section should initially be visible.

**Deprecated**

**Flags**: IR

---
## Attr: SectionItem.defaultValue

### Description
Section items show their `value` as title text for the section. Therefore the simplest way to specify this text on the form item directly is via the `defaultValue` attribute.

**Flags**: IRW

---
## Attr: SectionItem.canTabToHeader

### Description
If true, the header for this Section will be included in the page's tab order for accessibility. May also be set at the [DynamicForm](DynamicForm.md#class-dynamicform) level via [DynamicForm.canTabToSectionHeaders](DynamicForm.md#attr-dynamicformcantabtosectionheaders).

See [accessibility](../kb_topics/accessibility.md#kb-topic-accessibility--section-508-compliance).

**Flags**: IR

---
## Attr: SectionItem.itemIds

### Description
[Names](FormItem.md#attr-formitemname) of the items that should be considered a member of this section.

**Flags**: IR

---
## Method: SectionItem.isExpanded

### Description
Returns a boolean indicating whether this SectionItem is expanded.

### Returns

`[Boolean](#type-boolean)` — true if the section is expanded false if not

---
## Method: SectionItem.collapseSection

### Description
Collapse a sectionItem, and hide all the items within the section (not including the header).

---
## Method: SectionItem.expandSection

### Description
Expands a section, showing all the items contained within the section.

---
