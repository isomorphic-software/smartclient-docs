# QualityIndicatedLocator Documentation

[← Back to API Index](../main.md)

---

## Attr: QualityIndicatedLocator.locator

### Description
The [AutoTestLocator](../main_2.md#type-autotestlocator) associated with some DOM element in a SmartClient application page.

**Flags**: IR

---
## Attr: QualityIndicatedLocator.globalID

### Description
The ID of the component within the locator segments that has an auto-generated global ID.

**Flags**: IR

---
## Attr: QualityIndicatedLocator.containsGlobalId

### Description
True if the returned [locator](#attr-qualityindicatedlocatorlocator) includes a reference using an auto-generated global ID.

**Flags**: IR

---
## Attr: QualityIndicatedLocator.firstParentOfIndex

### Description
The ID of the first parent within the locator segments that has a child referenced by index. Note that a child component with an explicit [locatorName](Canvas.md#attr-canvaslocatorname) will be excluded since the name is a reliable means to locate the component.

**Flags**: IR

---
## Attr: QualityIndicatedLocator.containsIndices

### Description
True if the returned [locator](#attr-qualityindicatedlocatorlocator) includes references using index positions.

**Flags**: IR

---
