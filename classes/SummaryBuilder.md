# SummaryBuilder Documentation

[← Back to API Index](../main.md)

---

## Class: SummaryBuilder

*Inherits from:* [FormulaBuilder](FormulaBuilder.md#class-formulabuilder)

### Description
Shows an interface allowing a user to create or edit fields by typing simple format-strings into a text field. The format-strings can include the values of other fields and additional text as required.

Available values for the format-string are determined by the DataSource fields, and are given simple single-letter aliases (such as "A", "B", ...) similar to column names in Excel. The set of available values is shown in the [FormulaBuilder.fieldKey](FormulaBuilder.md#attr-formulabuilderfieldkey) as a simple mapping between the [field title](DataSourceField.md#attr-datasourcefieldtitle) and its short name.

To include a field in the format-string, prefix it with a hash sign (#).

### Groups

- summaryFields

---
## Attr: SummaryBuilder.testButtonHoverContents_cantTest

### Description
Hover contents to display for the [testButton](FormulaBuilder.md#attr-formulabuildertestbutton) when this `SummaryBuilder` is unable to run a test.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: SummaryBuilder.showHelpIcon

### Description
Whether to show the help icon that appears after the [SummaryBuilder.formulaField](#attr-summarybuilderformulafield).

### Groups

- summaryFields

**Flags**: IR

---
## Attr: SummaryBuilder.testButtonHoverContents

### Description
Hover contents to display for the [testButton](FormulaBuilder.md#attr-formulabuildertestbutton).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: SummaryBuilder.fields

### Description
DataSource providing the available fields for the SummaryBuilder.

By default the SummaryBuilder will include all fields. Set [SummaryBuilder.fields](#attr-summarybuilderfields) to override this.

### Groups

- summaryFields

**Flags**: IRW

---
## Attr: SummaryBuilder.builderTypeText

### Description
Indicates whether to use "summary" or some other keyword in various captions and text

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: SummaryBuilder.formulaField

### Description
TextItem that users type into when entering a formula.

### Groups

- summaryFields

**Flags**: IR

---
## Attr: SummaryBuilder.helpIcon

### Description
Icon that appears after the [SummaryBuilder.formulaField](#attr-summarybuilderformulafield), showing help on hover.

### Groups

- summaryFields

**Flags**: IRA

---
## Attr: SummaryBuilder.editMode

### Description
Are we editing an existing field?

### Groups

- summaryFields

**Flags**: IR

---
## Attr: SummaryBuilder.dataSource

### Description
DataSource providing the available fields for the formulaBuilder.

By default the formulaBuilder will include **only** fields of numeric type or derived from a numeric type. Set [FormulaBuilder.fields](FormulaBuilder.md#attr-formulabuilderfields) to override this.

### Groups

- summaryFields

**Flags**: IRW

---
## Attr: SummaryBuilder.helpTextIntro

### Description
Text that appears in the hover from the [SummaryBuilder.helpIcon](#attr-summarybuilderhelpicon), as a pre-amble to the list of available format-tokens.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: SummaryBuilder.autoHideCheckBoxLabel

### Description
Text label for the checkbox that allows the user to automatically hide the fields used in the summary format.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: SummaryBuilder.field

### Description
The Field object representing the field being created or edited.

### Groups

- summaryFields

**Flags**: IR

---
## Attr: SummaryBuilder.showAutoHideCheckBox

### Description
Whether to show a checkbox offering the user the ability to automatically hide any fields involved in the formula.

### Groups

- summaryFields

**Flags**: IR

---
## Attr: SummaryBuilder.autoHideCheckBox

### Description
CheckBox that, when selected, hides columns in the component that are used in this formula.

### Groups

- summaryFields

**Flags**: IR

---
## Attr: SummaryBuilder.titleField

### Description
TextItem that allows users to set the title for this field.

### Groups

- summaryFields

**Flags**: IR

---
## Attr: SummaryBuilder.testRecord

### Description
Record to use when showing sample output for the format string.

If not specified, the selected record in the component that launched the SummaryBuilder will be used, or if there's no selection, the first visible row, or with no component, a dummy data row derived automatically from the provided DataSource.

### Groups

- formulaFields

**Flags**: IRA

---
## Method: SummaryBuilder.fireOnClose

### Description
Override to execute a callback function when the Format is Cancelled or Saved.

### Groups

- summaryFields

**Flags**: A

---
## Method: SummaryBuilder.setSummary

### Description
Call to set the format-string in this SummaryBuilder.

Note that calling setSummary() will update the UI, generate the summary's function and test it automatically.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | The new format-string for the summary |

### Groups

- formulaFields

---
## Method: SummaryBuilder.getHelpText

### Description
Call to retrieve the text the SummaryBuilder would show by default for help, or override to provide alternate help text.

### Returns

`[String](#type-string)` — By default, the results of getHoverText()

### Groups

- summaryFields

---
## Method: SummaryBuilder.save

### Description
Call to finish working, test the formula and call [fireOnClose()](FormulaBuilder.md#method-formulabuilderfireonclose). Called automatically when the Save button is clicked.

### Groups

- formulaFields

---
