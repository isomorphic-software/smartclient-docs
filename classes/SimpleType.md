# SimpleType Documentation

[← Back to API Index](../reference.md)

---

## Class: SimpleType

### Description
An atomic type such as a string or number, that is generally stored, displayed and manipulated as a single value.

SimpleTypes can be created at any time, and subsequently referred to as a [field type](DataSourceField.md#attr-datasourcefieldtype) in [DataSources](DataSource.md#class-datasource) and [DataBoundComponents](../reference.md#interface-databoundcomponent). This allows you to define [validation](#attr-simpletypevalidators), [formatting](#method-simpletypenormaldisplayformatter) and [editing](#attr-simpletypeeditortype) behaviors for a type to be reused across all [DataBoundComponents](../reference.md#interface-databoundcomponent).

The SimpleType class also allows data to be stored in some opaque format but treated as simple atomic values as far as SmartClient components are concerned by implementing [SimpleType.getAtomicValue](#method-simpletypegetatomicvalue) and [SimpleType.updateAtomicValue](#method-simpletypeupdateatomicvalue) methods. For example, if some record has a field value set to a javascript object with the following properties:

```
 { stringValue:"A String", length: 9 }
 
```
this value could be treated as a simple string by defining a SimpleType with [SimpleType.inheritsFrom](#attr-simpletypeinheritsfrom) set to `"text"` and a custom `getAtomicValue()` method that simply extracted the _"stringValue"_ attribute from the data object. DataBoundComponents would then display the string value, and use it for sorting and other standard databinding features.

Note that the term "simpleType" is used in the same sense as in [http://www.w3.org/TR/xmlschema-0/](XML Schema), and [XMLTools.loadXMLSchema](XMLTools.md#classmethod-xmltoolsloadxmlschema) will create new SimpleType definitions.

When using the SmartClient Server, SimpleTypes can be defined server-side, and should be defined server-side if validators are going to be declared so that the server will enforce validation. To define server-side SimpleTypes using Component XML you should create file {typeName}.type.xml in the following format:

```
   <SimpleType name="{typeName}" inheritsFrom="{otherSimpleType}" 
                  editorType="{FormItemClassName}">
     <validators>
       <!-- validator definition just like DataSourceField -->
     </validators>
   </SimpleType>
 
```
.. and place this file alongside your DataSource files (.ds.xml) files - in any of folders listed in `project.datasources` property in [server.properties](../reference.md#kb-topic-serverproperties-file).

SimpleTypes can be loaded via DataSourceLoader or [loadDS JSP tags](../kb_topics/loadDSTag.md#kb-topic-isomorphicloadds) and should be loaded **before** the definitions of any DataSources that use them (so generally put all SimpleType definitions first).

Define validators in the server-side type definition, for example:

```
   <SimpleType name="countryCodeType" inheritsFrom="text">
     <validators>
       <validator type="lengthRange" min="2" max="2"
         errorMessage="Length of country code should be equal to 2." />
       <validator type="regexp" expression="[A-Z][A-Z]"
         errorMessage="CountryCode should have only uppercase letters." />
     </validators>
   </SimpleType>
 
```

For client-side formatters, add these to the type definition after loading it from the server, for example:

```
     isc.SimpleType.getType("independenceDateType").addProperties({
         normalDisplayFormatter : function (value) {
             if (value == null) return "";
             return "<i>" + (value.getYear() + 1900) + "</i>";
         }
     });
   
```
Note that formatters must be added to the SimpleType definition **before** any DataBoundComponent binds to a DataSource that uses the SimpleType.

An example is *here*.

---
## Attr: SimpleType.groupingModes

### Description
A set of key-value pairs that represent the names and titles of the grouping modes available to values of this type, for use in components that support grouping.

Some types provide a set of builtin groupingModes, as covered [here](../kb_topics/builtinGroupingModes.md#kb-topic-builtingroupingmodes).

Use [SimpleType.getGroupValue](#method-simpletypegetgroupvalue) and [SimpleType.getGroupTitle](#method-simpletypegetgrouptitle) to implement custom grouping logic for each of the grouping modes you provide.

**Flags**: IRW

---
## Attr: SimpleType.inheritsFrom

### Description
Name of another SimpleType from which this type should inherit.

Validators, if any, will be combined. All other SimpleType properties default to the inherited type's value.

**Flags**: IR

---
## Attr: SimpleType.defaultGroupingMode

### Description
In components that support grouping, the default mode from the available [groupingModes](#attr-simpletypegroupingmodes) to use when grouping values of this type.

**Flags**: IRW

---
## Attr: SimpleType.name

### Description
Name of the type, used to refer to the type from [field.type](DataSourceField.md#attr-datasourcefieldtype).

**Flags**: IR

---
## Attr: SimpleType.validOperators

### Description
Set of search operators valid for this type.

If not specified, the [inherited](#attr-simpletypeinheritsfrom) type's operators will be used, finally defaulting to the default operators for the basic types (eg, integer).

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: SimpleType.exportFormat

### Description
[FormatString](../reference.md#type-formatstring) used during exports for numeric or date formatting. See [DataSourceField.exportFormat](DataSourceField.md#attr-datasourcefieldexportformat).

### Groups

- exportFormatting

**Flags**: IR

---
## Attr: SimpleType.readOnlyEditorType

### Description
Classname of the FormItem that should be used to display values of this type when a field is marked as [canEdit false](DataSourceField.md#attr-datasourcefieldcanedit) and the field is displayed in an editor type component like a DynamicForm.

May be overridden by [DataSourceField.readOnlyEditorType](DataSourceField.md#attr-datasourcefieldreadonlyeditortype).

**Flags**: IR

---
## Attr: SimpleType.filterEditorType

### Description
Classname of the FormItem that should be used to edit values of this type if it appears in a filter row.

May be overridden by [DataSourceField.filterEditorType](DataSourceField.md#attr-datasourcefieldfiltereditortype).

**Flags**: IR

---
## Attr: SimpleType.fieldProperties

### Description
These are properties that are essentially copied onto any DataSourceField where the property is applied. The supported properties are only client-side properties.

**Flags**: IR

---
## Attr: SimpleType.defaultOperator

### Description
The default search-operator for this data-type.

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: SimpleType.format

### Description
[FormatString](../reference.md#type-formatstring) for numeric or date formatting. See [DataSourceField.format](DataSourceField.md#attr-datasourcefieldformat).

### Groups

- exportFormatting

**Flags**: IR

---
## Attr: SimpleType.editorType

### Description
Classname of the FormItem that should be the default for editing values of this type (eg "SelectItem").

You can create a simple custom FormItem by adding default [FormItem.icons](FormItem.md#attr-formitemicons) that launch custom value picking dialogs (an example is in the _QuickStart Guide_, Chapter 9, _Extending SmartClient_). By setting simpleType.editorType to the name of your custom FormItem, forms will automatically use the custom FormItem, as will grids performing [inline editing](ListGrid_1.md#attr-listgridcanedit).

**Flags**: IR

---
## Attr: SimpleType.validators

### Description
Validators to apply to value of this type.

### Groups

- validation

**Flags**: IR

---
## Attr: SimpleType.valueMap

### Description
List of legal values for this type, like [DataSourceField.valueMap](DataSourceField.md#attr-datasourcefieldvaluemap).

### Groups

- dataType

**Flags**: IR

---
## ClassMethod: SimpleType.setDefaultSummaryFunction

### Description
Set up a default summary function for some field type.

Note that the following default summary functions are set up when SmartClient initializes:  
\- `"integer"` defaults to `"sum"`  
\- `"float"` defaults to `"sum"`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| typeName | [String](#type-string) | false | — | type name |
| summaryFunction | [SummaryFunction](../reference.md#type-summaryfunction) | false | — | summary function to set as the default for this data type. |

---
## ClassMethod: SimpleType.registerSummaryFunction

### Description
Registers a new [SummaryFunction](../reference.md#type-summaryfunction) by name. After calling this method, developers may specify the name passed in as a standard summaryFunction (for example in [ListGridField.summaryFunction](ListGridField.md#attr-listgridfieldsummaryfunction)).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| functionName | [String](#type-string) | false | — | name for the newly registered summaryFunction |
| method | [Function](#type-function) | false | — | New summary function. This function should take 2 parameters

*   `records`: an array of records for which a summary must be generated
*   `field`: a field definition
*   `summaryConfig`: summary configuration (see [SummaryConfiguration](../reference.md#object-summaryconfiguration))

and return a summary value for the field across the records. |

---
## ClassMethod: SimpleType.getType

### Description
Retrieve a simpleType definition by type name

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| typeName | [String](#type-string) | false | — | the `name` of the simpleType to return |

### Returns

`[SimpleType](#type-simpletype)` — simple type object

---
## ClassMethod: SimpleType.getDefaultSummaryFunction

### Description
Retrieves the default summary function for some field type.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| typeName | [String](#type-string) | false | — | type name |

### Returns

`[SummaryFunction](../reference.md#type-summaryfunction)` — default summary function for this data type.

---
## ClassMethod: SimpleType.applySummaryFunction

### Description
Applies a [SummaryFunction](../reference.md#type-summaryfunction) to an array of records

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of Objects](#type-array-of-objects) | false | — | set of records to retrieve a summary value for |
| field | [DataSourceField](#type-datasourcefield) | false | — | field for which we're picking up a summary value |
| summaryFunction | [SummaryFunction](../reference.md#type-summaryfunction) | false | — | SummaryFunction to apply to the records in order to retrieve the summary value. May be specified as an explicit function or string of script to execute, or a SummaryFunction identifier |
| summaryConfig | [SummaryConfiguration](#type-summaryconfiguration) | false | — | config that affects summary calculation |

### Returns

`[Any](#type-any)` — summary value generated from the applied SummaryFunction

---
## Method: SimpleType.getGroupValue

### Description
Returns a group value appropriate for the passed record, field and value, in the passed component.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | the record value to return a group value for |
| record | [Record](#type-record) | false | — | the record containing the passed value |
| field | [Object](../reference_2.md#type-object) | false | — | the field relating to the value to be processed |
| fieldName | [String](#type-string) | false | — | the name of the field relating to the value to be processed |
| component | [Canvas](#type-canvas) | false | — | the component, usually a [ListGrid](ListGrid_1.md#class-listgrid), containing the passed record |

### Returns

`[Any](#type-any)` — the group value for the passed parameters

---
## Method: SimpleType.parseInput

### Description
Parser to convert some user-edited value to an underlying data value of this type. This parser is called when storing out values edited in a freeform editor such as a [TextItem](TextItem.md#class-textitem). Typically this will convert from the format produced by [SimpleType.editFormatter](#method-simpletypeeditformatter) back to a data value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [String](#type-string) | false | — | edited value provided by the user |
| field | [FormItem](#type-formitem) | true | — | Editor for this field |
| form | [DynamicForm](#type-dynamicform) | true | — | DynamicForm containing this editor |
| record | [Record](#type-record) | true | — | Current edit values for this record, as displayed in the edit component. |

### Returns

`[Any](#type-any)` — data value derived from display string passed in.

---
## Method: SimpleType.updateAtomicValue

### Description
Optional method to update a live data value with an edited atomic value (such as a string or number). If defined this method will be called when the user edits data in a field of this type, allowing the developer to convert from the atomic type to a raw data value for storage.

Note that if the user is editing a field which did not previously have a value, the 'currentValue' will be null. This method should handle this (creating a new data value).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| atomicValue | [Any](#type-any) | false | — | New atomic value. This should match the underlying atomic type specified by the [SimpleType.inheritsFrom](#attr-simpletypeinheritsfrom) attribute. |
| currentValue | [Any](#type-any) | false | — | Existing data value to be updated. |
| reason | [String](#type-string) | false | — | The reason your updateAtomicValue() method is being called. See [SimpleType.getAtomicValue](#method-simpletypegetatomicvalue) for the reason strings used by the framework |

### Returns

`[Any](#type-any)` — Updated data value.

---
## Method: SimpleType.getGroupTitle

### Description
Returns a string value appropriate for the title of the group containing the passed value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | the record value to return a group title for |
| record | [Record](#type-record) | false | — | the record containing the passed group value |
| field | [Object](../reference_2.md#type-object) | false | — | the field relating to the value to be processed |
| fieldName | [String](#type-string) | false | — | the name of the field relating to the value to be processed |
| component | [Canvas](#type-canvas) | false | — | the component, usually a [ListGrid](ListGrid_1.md#class-listgrid), containing the passed record |

### Returns

`[String](#type-string)` — the group title for the passed parameters

---
## Method: SimpleType.shortDisplayFormatter

### Description
Formatter for values of this type when compact display is required, for example, in a [ListGrid](ListGrid_1.md#class-listgrid) or [TreeGrid](TreeGrid.md#class-treegrid).

When this formatter is called, the SimpleType object is available as "this".

A formatter can make itself configurable on a per-component or per-field basis by checking properties on the component or field. For example, a formatter for account IDs may want to omit a prefix in views where it is redundant, and could check a flag listGridField.omitAccountIdPrefix for this purpose.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | value to be formatted |
| field | [Field](#type-field) | true | — | field descriptor from the component calling the formatter, if applicable. Depending on the calling component, this could be a [ListGridField](../reference.md#object-listgridfield), [TreeGridField](../reference.md#object-treegridfield), etc |
| component | [DataBoundComponent](#type-databoundcomponent) | true | — | component calling this formatter, if applicable |
| record | [Object](../reference_2.md#type-object) | true | — | Full record, if applicable |

---
## Method: SimpleType.editFormatter

### Description
Formatter for values of this type when displayed in a freeform text editor, such as a [TextItem](TextItem.md#class-textitem).

See also [SimpleType.parseInput](#method-simpletypeparseinput) for parsing an edited text value back to a data value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | value to be formatted |
| field | [FormItem](#type-formitem) | true | — | Editor for this field |
| form | [DynamicForm](#type-dynamicform) | true | — | DynamicForm containing this editor |
| record | [Record](#type-record) | true | — | Current edit values for this record, as displayed in the edit component. |

### Returns

`[String](#type-string)` — formatted value

---
## Method: SimpleType.getAtomicValue

### Description
Optional method to extract an atomic value (such as a string or number) from some arbitrary live data value. If defined, this method will be called for every field value of the specified type in order to convert from the raw data value to an atomic type to be used for standard DataBinding features such as sorting and editing.

The "reason" parameter is passed by the framework to indicate why it is asking for the atomic value. Your method can use this value to affect the atomic value that is returned - for example, if the reason is "sort" you could return the atomic value converted to upper-case, to impose case-insensitive sorting. Reason strings used by the framework are:

*   "edit" Retrieving the edit value of the field in a [DynamicForm](DynamicForm.md#class-dynamicform) or [ListGrid](ListGrid_1.md#class-listgrid)
*   "format" Retrieving the value to format it for display
*   "mask" Retrieving the value to present it for masked input
*   "filter" Retrieving the value for use in a filter comparison
*   "sort" Retrieving the value for use in a sort comparison
*   "group" Retrieving the value for use in a group comparison
*   "formula" Retrieving the value for use in a formula calculation
*   "vm\_getValue" Retrieving the value from [ValuesManager.getValue](ValuesManager.md#method-valuesmanagergetvalue)
*   "validate" Retrieving the value for validation, or setting the value if validation caused it to change
*   "compare" Retrieving the "old" or "new" value from [ListGrid.cellHasChanges](ListGrid_1.md#method-listgridcellhaschanges)
*   "getRawValue" Retrieving the raw value of a [ListGrid](ListGrid_1.md#class-listgrid) cell
*   "criteria" Setting the value from [DynamicForm.setValuesAsCriteria](DynamicForm.md#method-dynamicformsetvaluesascriteria)
*   "updateValue" Setting the value from internal methods of [DynamicForm](DynamicForm.md#class-dynamicform) or [ValuesManager](ValuesManager.md#class-valuesmanager)
*   "setRawValue" Setting the raw value of a [ListGrid](ListGrid_1.md#class-listgrid) cell
*   "saveLocally" Setting the value from [ListGrid.saveLocally](ListGrid_1.md#attr-listgridsavelocally)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | Raw data value to convert. Typically this would be a field value for some record. |
| reason | [String](#type-string) | false | — | The reason your getAtomicValue() method is being called |

### Returns

`[Any](#type-any)` — Atomic value. This should match the underlying atomic type specified by the [SimpleType.inheritsFrom](#attr-simpletypeinheritsfrom) attribute.

---
## Method: SimpleType.compareValues

### Description
Optional method to allow you to write a custom comparator for this SimpleType. If implemented, this method will be used by the framework when it needs to compare two values of a field for equality - for example, when considering if an edited field value has changed. If you do not implement this method, values will be compared using standard techniques, so you should only provide an implementation if you have some unusual requirement.

Implementations of this method should return the following:

*   0 if the two values are equal
*   \-1 if the first value is greater than the second
*   1 if the second value is greater than the first

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value1 | [Any](#type-any) | false | — | First value for comparison |
| value2 | [Any](#type-any) | false | — | Second value for comparison |
| field | [DataSourceField](#type-datasourcefield)|[ListGridField](#type-listgridfield)|[DetailViewerField](#type-detailviewerfield)|[FormItem](#type-formitem) | false | — | Field definition from a dataSource or dataBoundComponent. |

### Returns

`[Integer](../reference_2.md#type-integer)` — Result of comparison, -1, 0 or 1, as described above

---
## Method: SimpleType.getGroupingModes

### Description
Returns the set of [grouping modes](#attr-simpletypegroupingmodes) available for values of this type in components that support grouping.

### Returns

`[ValueMap](../reference.md#type-valuemap)` — the set of grouping modes available for this type

---
## Method: SimpleType.normalDisplayFormatter

### Description
Normal formatter for values of this type used in a [StaticTextItem](StaticTextItem.md#class-statictextitem) or [DetailViewer](DetailViewer.md#class-detailviewer).

When this formatter is called, the SimpleType object is available as "this".

A formatter can make itself configurable on a per-component or per-field basis by checking properties on the component or field. For example, a formatter for account IDs may want to omit a prefix in views where it is redundant, and could check a flag detailViewer.omitAccountIdPrefix for this purpose.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | value to be formatted |
| field | [Field](#type-field) | true | — | field descriptor from the component calling the formatter, if applicable. Depending on the calling component, this could be a [FormItem](FormItem.md#class-formitem), [DetailViewerField](../reference.md#object-detailviewerfield), etc |
| component | [DataBoundComponent](#type-databoundcomponent) | true | — | component calling this formatter, if applicable |
| record | [Object](../reference_2.md#type-object) | true | — | Full record, if applicable |

---
