# SelectionOutline Documentation

[← Back to API Index](../reference.md)

---

## Class: SelectionOutline

### Description
This static singleton class implements a component that can be used to highlight any other Canvas or FormItem by drawing a line around it and optional label. The selection outline moves, resizes and hides with the target object, and does not occlude any part of it. The outline is not a peer, child or member of the target object; the target object does not know about the outline.

NOTE: This class is for internal use only by EditContext.

---
## ClassAttr: SelectionOutline.labelBackgroundColor

### Description
The background color for the selection label. It corresponds to the CSS background-color attribute. You can set this property to an RGB value (e.g. #22AAFF) or a named color (e.g. red) from a list of browser supported color names.

**Flags**: RW

---
## ClassAttr: SelectionOutline.border

### Description
Set the CSS border of this component as a CSS string including border-width, border-style, and/or color (eg "1px dashed blue").

This property applies the same border to all four sides of this component.

**Flags**: RW

---
## ClassMethod: SelectionOutline.getLabelBackgroundColor

### Description
Returns the background color for the selection label.

---
## ClassMethod: SelectionOutline.setBorder

### Description
Set the CSS border of this component as a CSS string including border-width, border-style, and/or color (eg "1px dashed blue").

This property applies the same border to all four sides of this component.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| border | [String](#type-string) | false | "1px dashed #44ff44" | css border string |

---
## ClassMethod: SelectionOutline.getBorder

### Description
Returns the CSS border of this component.

---
## ClassMethod: SelectionOutline.setLabelBackgroundColor

### Description
Set the background color for the selection label. It corresponds to the CSS background-color attribute. You can set this property to an RGB value (e.g. #22AAFF) or a named color (e.g. red) from a list of browser supported color names.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string) | false | "#44ff44" | css color |

---
