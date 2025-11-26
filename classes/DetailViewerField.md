# DetailViewerField Documentation

[← Back to API Index](../reference.md)

---

## Attr: DetailViewerField.imageHeight

### Description
Height of image shown for fieldTypes image in this field.

If set to a String, assumed to be a property on each record that specifies the image height. For example, if `field.imageHeight` is "logoHeight", `record.logoHeight` will control the height of the image.

### Groups

- imageColumns

### See Also

- [DetailViewerField.imageSize](#attr-detailviewerfieldimagesize)
- [DetailViewerField.imageWidth](#attr-detailviewerfieldimagewidth)

**Flags**: IRW

---
## Attr: DetailViewerField.displayField

### Description
If `displayField` is defined for the field then the DetailViewer will display the `displayField` attribute of records instead of the attribute given by the [DetailViewerField.name](#attr-detailviewerfieldname) of the field.

**Flags**: IR

---
## Attr: DetailViewerField.valueMap

### Description
A property list (or an expression that evaluates to a property list) specifying a mapping of internal values to display values for the field (row).

**Flags**: IR

---
## Attr: DetailViewerField.imageURLSuffix

### Description
If this field has type set to `"image"`, the value of this property will be appended to the end of the URL for the icon displayed.

### Groups

- imageColumns

**Flags**: IRWA

---
## Attr: DetailViewerField.target

### Description
By default, clicking a link rendered by this item opens it in a new browser window. You can alter this behavior by setting this property. The value of this property will be passed as the value to the `target` attribute of the anchor tag used to render the link. `target` is applicable only if the field type is set to "link".

### See Also

- [DetailViewerField.type](#attr-detailviewerfieldtype)

**Flags**: IRW

---
## Attr: DetailViewerField.cellStyle

### Description
If specified, cells in this field will be rendered using this css className rather than [DetailViewer.cellStyle](DetailViewer.md#attr-detailviewercellstyle)

**Flags**: IRW

---
## Attr: DetailViewerField.canExport

### Description
Dictates whether the data in this field be exported. Explicitly set this to false to prevent exporting. Has no effect if the underlying [dataSourceField](DataSourceField.md#attr-datasourcefieldcanexport) is explicitly set to canExport: false.

**Flags**: IR

---
## Attr: DetailViewerField.includeFrom

### Description
Indicates this field's values come from another, related DataSource. The individual field will inherit settings such as [field.type](#attr-detailviewerfieldtype) and [field.title](#attr-detailviewerfieldtitle) from the related DataSource just like fields from the primary DataSource.

**Flags**: IR

---
## Attr: DetailViewerField.decimalPad

### Description
Applies only to fields of type "float" and enforces a minimum number of digits shown after the decimal point.

For example, a field value of 343.1, 343.104 and 343.09872677 would all be shown as 343.10 if decimalPad is 2.

The original unpadded value is always shown when the value is edited.

### Groups

- appearance

**Flags**: IRW

---
## Attr: DetailViewerField.linkURLPrefix

### Description
If this field has type set to `"link"`, setting this property will apply a standard prefix to the link URL when displaying values of this field.

### See Also

- [DetailViewerField.type](#attr-detailviewerfieldtype)

**Flags**: IRWA

---
## Attr: DetailViewerField.type

### Description
Specifies the type of this DetailViewerField. By default (value is `null`) the field shows a field title on the left and the field value on the right. There are four special values for this attribute:

*   "header" - If you specify type "header", the field spans both the field name and field value columns and contains text defined in the [DetailViewerField.value](#attr-detailviewerfieldvalue) attribute with the style specified by [DetailViewer.headerStyle](DetailViewer.md#attr-detailviewerheaderstyle). You can use this field type as a titled separator.
*   "separator" - If you specify type "separator", the field spans both the field name and the field value columns with no text, and is styled using the style specified via [DetailViewer.separatorStyle](DetailViewer.md#attr-detailviewerseparatorstyle). The height of the separator field can be controlled via [DetailViewerField.height](#attr-detailviewerfieldheight).
*   "image" For viewing, a thumbnail image is rendered in the field. The URL of the image is the value of the field, and should be absolute. The size of the image is controlled by [DetailViewerField.imageSize](#attr-detailviewerfieldimagesize), [DetailViewerField.imageWidth](#attr-detailviewerfieldimagewidth), [DetailViewerField.imageHeight](#attr-detailviewerfieldimageheight)
*   "link" For viewing, a clickable html link (using an HTML anchor tag: `<A>`) is rendered in the field. The target URL is the value of the field, which is also the default display value. You can override the display value by setting [DetailViewerRecord.linkText](../reference.md#attr-detailviewerrecordlinktext) or [DetailViewerField.linkText](#attr-detailviewerfieldlinktext).
    
    Clicking the link opens the URL in a new window by default. To change this behavior, you can set `field.target`, which works identically to the "target" attribute on an HTML anchor (`<A>`) tag. See [DetailViewerField.target](#attr-detailviewerfieldtarget) for more information.

**Flags**: IR

---
## Attr: DetailViewerField.showFileInline

### Description
For a field of type:"imageFile", indicates whether to stream the image and display it inline or to display the View and Download icons.

**Flags**: IR

---
## Attr: DetailViewerField.imageURLPrefix

### Description
If this field has type set to `"image"` and the URL for the image displayed is not absolute, the path of the URL will be relative to this string.

### Groups

- imageColumns

**Flags**: IRWA

---
## Attr: DetailViewerField.format

### Description
[FormatString](../reference.md#type-formatstring) for numeric or date formatting. See [DataSourceField.format](DataSourceField.md#attr-datasourcefieldformat).

### Groups

- exportFormatting

**Flags**: IR

---
## Attr: DetailViewerField.exportFormat

### Description
[FormatString](../reference.md#type-formatstring) used during exports for numeric or date formatting. See [DataSourceField.exportFormat](DataSourceField.md#attr-datasourcefieldexportformat).

### Groups

- exportFormatting

**Flags**: IR

---
## Attr: DetailViewerField.dataPath

### Description
dataPath property allows this field to display detail from nested data structures

**Flags**: IRA

---
## Attr: DetailViewerField.linkURLSuffix

### Description
If this field has type set to `"link"`, setting this property will apply a standard suffix to the link URL when displaying values of this field.

### See Also

- [DetailViewerField.type](#attr-detailviewerfieldtype)

**Flags**: IRWA

---
## Attr: DetailViewerField.hiliteIconWidth

### Description
Width for hilite icons for this field. Overrides [DetailViewer.hiliteIconSize](DetailViewer.md#attr-detailviewerhiliteiconsize), [DetailViewer.hiliteIconWidth](DetailViewer.md#attr-detailviewerhiliteiconwidth), and [DetailViewerField.hiliteIconSize](#attr-detailviewerfieldhiliteiconsize).

### Groups

- hiliting

**Flags**: IRW

---
## Attr: DetailViewerField.userFormula

### Description
Formula definition for this field.

**Flags**: IR

---
## Attr: DetailViewerField.userSummary

### Description
Summary definition for this field.

**Flags**: IR

---
## Attr: DetailViewerField.name

### Description
Name property used to identify the field, and determines which attribute from records will be displayed in this field.

Must be unique within the DetailViewer as well as a valid JavaScript identifier - see [FieldName](../reference.md#type-fieldname) for details and how to check for validity.

The attribute of the records to display in this field may also be set by [DetailViewerField.displayField](#attr-detailviewerfielddisplayfield).

**Flags**: IR

---
## Attr: DetailViewerField.canHilite

### Description
Determines whether this field can be hilited. Set to false to prevent this field from appearing in HiliteEditor.

### Groups

- hiliting

**Flags**: IRW

---
## Attr: DetailViewerField.value

### Description
When a field specifies its [DetailViewerField.type](#attr-detailviewerfieldtype) to be "header", the value of this attribute specifies the header text.

**Flags**: IR

---
## Attr: DetailViewerField.title

### Description
The title of the field as displayed on the left-hand side. If left unspecified, the title of the field is the [DetailViewerField.name](#attr-detailviewerfieldname) of the field.

**Flags**: IR

---
## Attr: DetailViewerField.decimalPrecision

### Description
Applies only to fields of type "float" and affects how many significant digits are shown.

For example, with decimalPrecision 3, if the field value is 343.672677, 343.673 is shown.

If the value is 125.2, 125.2 is shown - decimalPrecision will not cause extra zeros to be added. Use [DataSourceField.decimalPad](DataSourceField.md#attr-datasourcefielddecimalpad) for this.

A number is always shown with its original precision when edited.

### Groups

- appearance

**Flags**: IRW

---
## Attr: DetailViewerField.exportRawValues

### Description
Dictates whether the data in this field should be exported raw by [exportClientData()](DetailViewer.md#method-detailviewerexportclientdata). If set to true for a field, the values in the field-formatters will not be executed for data in this field.

**Flags**: IR

---
## Attr: DetailViewerField.hiliteIconLeftPadding

### Description
How much padding should there be on the left of [hilite icons](DetailViewer.md#attr-detailviewerhiliteicons) for this field? Overrides [DetailViewer.hiliteIconLeftPadding](DetailViewer.md#attr-detailviewerhiliteiconleftpadding)

### Groups

- hiliting

**Flags**: IRW

---
## Attr: DetailViewerField.imageWidth

### Description
Width of images shown for fieldTypes image in this field.

If set to a String, assumed to be a property on each record that specifies the image width. For example, if `field.imageWidth` is "logoWidth", `record.logoWidth` will control the width of the image.

### Groups

- imageColumns

### See Also

- [DetailViewerField.imageSize](#attr-detailviewerfieldimagesize)
- [DetailViewerField.imageHeight](#attr-detailviewerfieldimageheight)

**Flags**: IRW

---
## Attr: DetailViewerField.linkText

### Description
The HTML to display for values of this field if the field type is set to "link".

This property sets linkText that will be the same for all records. You can set linkText on a per-record basis via [DetailViewerRecord.linkText](../reference.md#attr-detailviewerrecordlinktext).

### See Also

- [DetailViewerField.type](#attr-detailviewerfieldtype)
- [DetailViewerRecord.linkText](../reference.md#attr-detailviewerrecordlinktext)
- [DetailViewer.linkTextProperty](DetailViewer.md#attr-detailviewerlinktextproperty)
- [DetailViewerField.linkTextProperty](#attr-detailviewerfieldlinktextproperty)

**Flags**: IRW

---
## Attr: DetailViewerField.timeFormatter

### Description
Time-format to apply to date type values within this field. If specified, any dates displayed in this field will be formatted as times using the appropriate format. This is most commonly only applied to fields specified as type `"time"` though if no explicit [DetailViewerField.dateFormatter](#attr-detailviewerfielddateformatter) is specified it will be respected for other fields as well.

If unspecified, a timeFormatter may be defined [at the component level](DetailViewer.md#attr-detailviewertimeformatter) and will be respected by fields of type `"time"`.

### Groups

- appearance

**Flags**: IRWA

---
## Attr: DetailViewerField.printCellStyle

### Description
If specified, when generating print HTML for this detailViewer, cells in this field will be rendered using this css className rather than [DetailViewer.printCellStyle](DetailViewer.md#attr-detailviewerprintcellstyle)

**Flags**: IRW

---
## Attr: DetailViewerField.escapeHTML

### Description
By default HTML values in DetailViewer cells will be interpreted by the browser. Setting this flag to true will causes HTML characters to be escaped, meaning the raw value of the field (for example `"`<b>`AAA`</b>`"`) is displayed to the user rather than the interpreted HTML (for example `"**AAA**"`)

**Flags**: IR

---
## Attr: DetailViewerField.dateFormatter

### Description
Display format to use for date type values within this field.

The [DetailViewerField.timeFormatter](#attr-detailviewerfieldtimeformatter) may also be used to format underlying Date values as times (omitting the date part entirely). If both `dateFormatter` and `timeFormatter` are specified on a field, for fields specified as [type "time"](#attr-detailviewerfieldtype) the `timeFormatter` will be used, otherwise the `dateFormatter`

If `field.dateFormatter` and `field.timeFormatter` is unspecified, date display format may be defined at the component level via [DetailViewer.dateFormatter](DetailViewer.md#attr-detailviewerdateformatter), or for fields of type `"datetime"` [DetailViewer.datetimeFormatter](DetailViewer.md#attr-detailviewerdatetimeformatter). Otherwise the default is to use the system-wide default normal date format, configured via [DateUtil.setNormalDisplayFormat](DateUtil.md#classmethod-dateutilsetnormaldisplayformat). Specify any valid [DateDisplayFormat](../reference.md#type-datedisplayformat) to change the format used by this item.

### See Also

- [ListGrid.dateFormatter](ListGrid_1.md#attr-listgriddateformatter)
- [ListGrid.datetimeFormatter](ListGrid_1.md#attr-listgriddatetimeformatter)
- [ListGridField.timeFormatter](ListGridField.md#attr-listgridfieldtimeformatter)

**Flags**: IRW

---
## Attr: DetailViewerField.height

### Description
For [DetailViewerField.type](#attr-detailviewerfieldtype): `"separator"`, this attribute specifies the height of the separator.

**Flags**: IR

---
## Attr: DetailViewerField.hiliteIconSize

### Description
Default width and height of [hilite icons](DetailViewer.md#attr-detailviewerhiliteicons) in this field. Takes precedence over hiliteIconWidth, hiliteIconHeight and hiliteIconSize specified at the component level. Can be overridden via [hiliteIconWidth](#attr-detailviewerfieldhiliteiconwidth) and [hiliteIconHeight](#attr-detailviewerfieldhiliteiconheight)

### Groups

- hiliting

### See Also

- [DetailViewer.hiliteIconSize](DetailViewer.md#attr-detailviewerhiliteiconsize)
- [DetailViewerField.hiliteIconWidth](#attr-detailviewerfieldhiliteiconwidth)
- [DetailViewerField.hiliteIconHeight](#attr-detailviewerfieldhiliteiconheight)

**Flags**: IRW

---
## Attr: DetailViewerField.hiliteIconHeight

### Description
Height for hilite icons for this field. Overrides [DetailViewer.hiliteIconSize](DetailViewer.md#attr-detailviewerhiliteiconsize), [DetailViewer.hiliteIconHeight](DetailViewer.md#attr-detailviewerhiliteiconheight), and [DetailViewerField.hiliteIconSize](#attr-detailviewerfieldhiliteiconsize).

### Groups

- hiliting

**Flags**: IRW

---
## Attr: DetailViewerField.imageSize

### Description
Size of images shown for fieldTypes image in this field.

If set to a String, assumed to be a property on each record that specifies the image height. For example, if `field.imageSize` is "logoSize", `record.logoSize` will control the size of the image.

### Groups

- imageColumns

### See Also

- [DetailViewerField.imageWidth](#attr-detailviewerfieldimagewidth)
- [DetailViewerField.imageHeight](#attr-detailviewerfieldimageheight)

**Flags**: IRW

---
## Attr: DetailViewerField.linkTextProperty

### Description
Name of the property in a DetailViewerRecord that holds the HTML to display for values of this field if the field type is set to "link".

### See Also

- [DetailViewerField.type](#attr-detailviewerfieldtype)
- [DetailViewerRecord.linkText](../reference.md#attr-detailviewerrecordlinktext)
- [DetailViewerField.linkText](#attr-detailviewerfieldlinktext)
- [DetailViewer.linkTextProperty](DetailViewer.md#attr-detailviewerlinktextproperty)

**Flags**: IRW

---
## Attr: DetailViewerField.emptyCellValue

### Description
The value to display for a cell whose value is null or the empty string after applying formatCellValue and valueMap (if any).

This is the field-specific attribute. You may also set the emptyCellValue at the viewer level to define the emptyCellValue for all empty fields in the viewer.

### Groups

- appearance

### See Also

- [DetailViewer.emptyCellValue](DetailViewer.md#attr-detailvieweremptycellvalue)

**Flags**: IR

---
## Attr: DetailViewerField.hiliteIconPosition

### Description
When [DetailViewer.hiliteIcons](DetailViewer.md#attr-detailviewerhiliteicons) are present, where the hilite icon will be placed relative to the field value. See [HiliteIconPosition](../reference_2.md#type-hiliteiconposition). Overrides [DetailViewer.hiliteIconPosition](DetailViewer.md#attr-detailviewerhiliteiconposition)

### Groups

- hiliting

**Flags**: IR

---
## Attr: DetailViewerField.hiliteIconRightPadding

### Description
How much padding should there be on the right of [hilite icons](DetailViewer.md#attr-detailviewerhiliteicons) for this field? Overrides [DetailViewer.hiliteIconRightPadding](DetailViewer.md#attr-detailviewerhiliteiconrightpadding)

### Groups

- hiliting

**Flags**: IRW

---
## Method: DetailViewerField.showIf

### Description
If specified on a field, this method is evaluated at draw time to determine whether or not to show this particular field.

This method can be specified either as a function or a string that will be auto-converted to a function.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewer | [DetailViewer](#type-detailviewer) | false | — | The DetailViewer |
| valueList | [List of DetailViewerRecord](#type-list-of-detailviewerrecord) | false | — | — |

### Returns

`[boolean](../reference.md#type-boolean)` — true to show the field, false to not show it.

---
## Method: DetailViewerField.formatCellValue

### Description
Optional method to format the value to display for this field's cells. Takes precedence over [DetailViewer.formatCellValue](DetailViewer.md#method-detailviewerformatcellvalue) for cells in this field.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [String](#type-string) | false | — | the raw value of the cell |
| record | [DetailViewerRecord](#type-detailviewerrecord) | false | — | the record being displayed |
| field | [DetailViewerField](#type-detailviewerfield) | false | — | the field being displayed |
| viewer | [DetailViewer](#type-detailviewer) | false | — | the detailViewer containing this field |

---
## Method: DetailViewerField.getCellStyle

### Description
Optional method to return the CSS class for cells in this field. If specified, this method will be called from [DetailViewer.getCellStyle](DetailViewer.md#method-detailviewergetcellstyle), and should return a css class name.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [String](#type-string) | false | — | actual value of this cell |
| field | [Object](../reference.md#type-object) | false | — | field object for this cell |
| record | [Object](../reference.md#type-object) | false | — | record object for this cell |
| viewer | [DetailViewer](#type-detailviewer) | false | — | the viewer instance to which this cell belongs |

### Returns

`[CSSStyleName](../reference.md#type-cssstylename)` — CSS style for this cell

### Groups

- appearance

---
