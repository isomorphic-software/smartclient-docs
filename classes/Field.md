# Field Documentation

[← Back to API Index](../reference.md)

---

## Attr: Field.escapeHTML

### Description
If set to `true`, then values for the field will be HTML-escaped.

**Flags**: IRW

---
## Attr: Field.title

### Description
An [HTMLString](../reference.md#type-htmlstring) to use as the displayable title for this field outside the context of a field container.

Within a [DataBoundComponent](../reference.md#interface-databoundcomponent):

*   A field's title may be set with [DataBoundComponent.setFieldTitle](#method-databoundcomponentsetfieldtitle).
*   Always call the [DataBoundComponent.getFieldTitle](#method-databoundcomponentgetfieldtitle) method to obtain the field's title.

### See Also

- [Field.exportTitle](#attr-fieldexporttitle)

**Flags**: IRW

---
## Attr: Field.canEdit

### Description
If set to `true`, then values for the field are considered editable. If set to `false`, then values for the field cannot be edited. If `null`, then the determination is left to the field container.

**Flags**: IR

---
## Attr: Field.exportTitle

### Description
Optional title HTML to use for the field in exports.

**Flags**: IR

---
## Attr: Field.primaryKey

### Description
If set to `true`, indicates that the value for this field (together with the values of any other fields that are also primaryKey:`true`) uniquely identify a record.

Note: the case where multiple fields are primary key fields—called "composite" or "multipart" keys—is not recommended by Isomorphic. See [DataSourceField.primaryKey](DataSourceField.md#attr-datasourcefieldprimarykey) for more information.

**Flags**: IR

---
## Attr: Field.name

### Description
Name of the field.

**Flags**: IR

---
## Attr: Field.type

### Description
Type of the field. This may be a built-in [FieldType](../reference_2.md#type-fieldtype), the [name](SimpleType.md#attr-simpletypename) of a [SimpleType](SimpleType.md#class-simpletype), or the [ID](DataSource.md#attr-datasourceid) of a [DataSource](DataSource.md#class-datasource).

**Flags**: IR

---
## Attr: Field.canExport

### Description
If set to `true`, then values for the field are considered exportable. If set to `false`, then values for the field will not be exported. If `null`, then the determination is left to the field container.

**Flags**: IR

---
## Attr: Field.valueMap

### Description
If set, specifies the set of legal values for the field.

**Flags**: IR

---
## Attr: Field.required

### Description
If set to `true`, then a value for this field is required to pass validation.

**Flags**: IR

---
## Attr: Field.multiple

### Description
If set to `true`, then the field is array-valued.

**Flags**: IR

---
## Attr: Field.sortByField

### Description
If set to a field name, causes the field to be sorted by the values in the specified field, for both client- and server-side sorting.

**Flags**: IR

---
