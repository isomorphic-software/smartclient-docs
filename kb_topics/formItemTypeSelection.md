# FormItem classes for databound component fields

[← Back to API Index](../reference.md)

---

## KB Topic: FormItem classes for databound component fields

### Description
[DynamicForms](../classes/DynamicForm.md#class-dynamicform) and subclasses are responsible for choosing the appropriate [FormItem](../classes/FormItem.md#class-formitem) type (or subclass) for their fields. This is true for standalone instances of `DynamicForm` or `SearchForm` and embedded forms used by editable components such as the [ListGrid](../classes/ListGrid_1.md#class-listgrid).

The [DynamicForm.getEditorType](../classes/DynamicForm.md#method-dynamicformgeteditortype) method is responsible for determining what form item class to create for any field. This may be overridden by subclasses such as [SearchForm](../classes/SearchForm.md#class-searchform), or by custom logic in dataBoundComponents with an editable view such as the ListGrid which provides [ListGrid.getEditorType](../classes/ListGrid_2.md#method-listgridgeteditortype) and [ListGrid.getFilterEditorType](../classes/ListGrid_2.md#method-listgridgetfiltereditortype).

At the component field level, the item type may be specified via an explicit `editorType` or `filterEditorType` property. For non-filter components such as standard DynamicForms or editable ListGrids, `field.editorType` may be used to specify the desired editor type for the field.  
For filter components, including [SearchForm](../classes/SearchForm.md#class-searchform) and [ListGrid filter editors](../classes/ListGrid_1.md#attr-listgridshowfiltereditor) `filterEditorType` is used. If `filterEditorType` is unset but `editorType` is set, filter components will use `editorType`.

The default formItem class can also be specified at the [DataSourceField](../reference_2.md#object-datasourcefield) level or the [SimpleType](../classes/SimpleType.md#class-simpletype) level for custom data types. See the `editorType`, `filterEditorType` and `readOnlyEditorType` attributes for those classes of objects.

If no explicit FormItem type was specified, the default formItem for a field will vary by data type and other properties. The following overview outlines most of the cases you'll encounter. This is intended as an orientation only, not a definitive list of every default FormItem-subclass for every combination of field settings.

In general, if a named "data-type item" exists it will be used by default for the data type. So fields of type `"text"` (which is also the default for fields with no explicit type) render in a [TextItem](../classes/TextItem.md#class-textitem) by default, fields of type "integer" render in an [IntegerItem](../reference.md#class-integeritem), and so on. This is described in the [FormItemType](../reference_2.md#type-formitemtype) overview. However there are many exceptions to this rule of thumb.

Fields with a [valueMap](../classes/DataSourceField.md#attr-datasourcefieldvaluemap) will render as a [SelectItem](../classes/SelectItem.md#class-selectitem) in editing interfaces - [DynamicForm](../classes/DynamicForm.md#class-dynamicform) or [editable ListGrid](../classes/ListGrid_1.md#attr-listgridcanedit) - by default.  
In filtering interfaces - [SearchForm](../classes/SearchForm.md#class-searchform), [ListGrid filterEditor](../classes/ListGrid_1.md#attr-listgridshowfiltereditor) - they will render as a [multi-select](../classes/SelectItem.md#attr-selectitemmultiple) for small sets of options, or the specified [DynamicForm.largeValueMapFilterEditorType](../classes/DynamicForm.md#attr-dynamicformlargevaluemapfiltereditortype) for [large sets of options](../classes/DynamicForm.md#attr-dynamicformlargevaluemapfiltereditorthreshold). This is the [SetFilterItem](../classes/SetFilterItem.md#class-setfilteritem) by default, with intelligent logic in place to back off to the default SelectItem if the target dataSource does not support `"inSet"` criterion operators.

Fields which derive their options from an optionDataSource will behave like large valueMaps, rendering as a SelectItem in editing interfaces and a SetFilterItem in filtering interfaces. This includes fields with a [foreignKey relationship](../classes/DataSourceField.md#attr-datasourcefieldforeignkey), with the exception of multi-FK relationships (fields with `multiple:true` representing one-to-many relationships as described in [the relations overview](dataSourceRelations.md#kb-topic-relations)). These fields will render a [MultiPickerItem](../classes/MultiPickerItem.md#class-multipickeritem) in editing interfaces by default.

Text fields with [DataSourceField.length](../classes/DataSourceField.md#attr-datasourcefieldlength) greater than [DynamicForm.longTextEditorThreshold](../classes/DynamicForm.md#attr-dynamicformlongtexteditorthreshold) will render in a TextAreaItem by default. See [DynamicForm.longTextEditorType](../classes/DynamicForm.md#attr-dynamicformlongtexteditortype). Note that for [editable ListGrids](../classes/ListGrid_1.md#attr-listgridcanedit) long text fields will render a pop-up with a text-area in it for better presentation to the user.

Fields of type `date` and `datetime` will render in editing interfaces using the DateItem and DateTimeItem by default. In filtering interfaces they will render as [DateRangeItem](../classes/DateRangeItem.md#class-daterangeitem) in a standalone SearchForm, or [MiniDateRangeItem](../classes/MiniDateRangeItem.md#class-minidaterangeitem) within ListGrid filterEditors.

Most binary fields in DynamicForms are rendered as [FileItem](../classes/FileItem.md#class-fileitem) or the [FileDropZone-based](../classes/FileDropZone.md#class-filedropzone) [FileUploadItem](../classes/FileUploadItem.md#class-fileuploaditem) depending on the value of [DynamicForm.useFileUploadItem](../classes/DynamicForm.md#attr-dynamicformusefileuploaditem).  
See the [upload](upload.md#kb-topic-uploading-files) and [binaryFields](binaryFields.md#kb-topic-binary-fields) overviews for more information about binary fields in SmartClient.

---
