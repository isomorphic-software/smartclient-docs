# DataView Documentation

[← Back to API Index](../reference.md)

---

## Class: DataView

*Inherits from:* [VLayout](../reference.md#class-vlayout)

### Description
A DataView coordinates the asynchronous loading of WSDL WebService and XML Schema definitions in applications created by Reify.

For applications that do not use WSDL Web Services and were not created by Reify, DataView is equivalent to it's superclass [VLayout](../reference.md#class-vlayout).

---
## Attr: DataView.minMemberLength

### Description
Minimum size, in pixels, below which flexible-sized members should never be shrunk, even if this requires the Layout to overflow. Note that this property only applies along the _length_ axis of the Layout, and has no affect on _breadth_.

Does not apply to members given a fixed size in pixels - such members will never be shrunk below their specified size in general.

### Groups

- layoutPolicy

### See Also

- [Canvas.minWidth](Canvas.md#attr-canvasminwidth)

**Flags**: IRW

---
## Method: DataView.dataViewLoaded

### Description
Executed when the dataView has loaded all dependencies (such as DataSources or WebServices). No default implementation.

**Flags**: A

---
