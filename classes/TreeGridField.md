# TreeGridField Documentation

[← Back to API Index](../reference.md)

---

## Attr: TreeGridField.treeField

### Description
The field containing `treeField: true` will display the [Tree](Tree.md#class-tree). If no field specifies this property, if a field named after the [Tree.titleProperty](Tree.md#attr-treetitleproperty) of the Tree is present in [TreeGrid.fields](TreeGrid.md#attr-treegridfields), that field will show the tree. Note that when using a DataSource, you typically define the title field via [DataSource.titleField](DataSource.md#attr-datasourcetitlefield) and the generated [ResultTree](ResultTree.md#class-resulttree) automatically uses this field. If none of the above rules apply, the first field in [TreeGrid.fields](TreeGrid.md#attr-treegridfields) is assigned to display the [Tree](Tree.md#class-tree).

### Groups

- treeField

**Flags**: IRW

---
## Attr: TreeGridField.canExport

### Description
Dictates whether the data in this field be exported. Explicitly set this to false to prevent exporting. Has no effect if the underlying [dataSourceField](DataSourceField.md#attr-datasourcefieldcanexport) is explicitly set to canExport: false.

**Flags**: IR

---
