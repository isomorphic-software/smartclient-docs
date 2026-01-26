# FormulaBuilder Documentation

[← Back to API Index](../reference.md)

---

## Class: FormulaBuilder

*Inherits from:* [VLayout](../reference.md#class-vlayout)

### Description
Shows an interface allowing a user to enter simple formulas by typing them into a text field.

Available values for the formula are determined by the DataSource fields, and are given simple single-letter aliases (such as "A", "B", ...) similar to column names in Excel. The set of available values is shown in the [FormulaBuilder.fieldKey](#attr-formulabuilderfieldkey) as a simple mapping between the [field title](DataSourceField.md#attr-datasourcefieldtitle) and its short name.

If [FormulaBuilder.targetRuleScope](#attr-formulabuildertargetrulescope) is specified the formula will use full field path names instead of single-letter aliases and the resulting formula will not include the formulaVars property.

By default, available math functions are shown in a hover from the [helpIcon](#attr-formulabuilderhelpicon) that appears after the formula field.

### Groups

- formulaFields

---
## Attr: FormulaBuilder.titleField

### Description
TextItem that allows users to set the title for this field.

### Groups

- formulaFields

**Flags**: IR

---
## Attr: FormulaBuilder.sampleHeaderTitle

### Description
The default title for the "Sample" panel, which displays a sample result for the formula.

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: FormulaBuilder.invalidBlankPrompt

### Description
When [testFunction](#method-formulabuildertestfunction) reports an empty formula, this attribute provides the error-text to display in the [message-label](#attr-formulabuildermessagelabel).

This is a dynamic string - text within `${...}` are dynamic variables and will be evaluated as JS code when the message is displayed.

Only one dynamic variable, builderType, is available and represents the type of this builder, either Formula or Summary.

The default output is:

`_Invalid blank [Formula/Summary]_`

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: FormulaBuilder.defaultNewFieldTitle

### Description
The default value for new Formula and Summary fields.

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: FormulaBuilder.helpIcon

### Description
Icon that appears after the [FormulaBuilder.formulaField](#attr-formulabuilderformulafield), showing help on hover.

### Groups

- formulaFields

**Flags**: IRA

---
## Attr: FormulaBuilder.validBuilderPrompt

### Description
When [testFunction](#method-formulabuildertestfunction) reports a valid formula and no other errors, this attribute provides the error-text to display in the [message-label](#attr-formulabuildermessagelabel).

This is a dynamic string - text within `${...}` are dynamic variables and will be evaluated as JS code when the message is displayed.

Only one dynamic variable, builderType, is available and represents the type of this builder, either Formula or Summary.

The default output is:

`_Valid [Formula/Summary]_`

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: FormulaBuilder.fieldKey

### Description
ListGrid displaying the list of available fields and their corresponding formula keys.

### Groups

- formulaFields

**Flags**: IR

---
## Attr: FormulaBuilder.builderTypeText

### Description
Indicates whether to use "formula" or some other keyword in various captions and text

### Groups

- i18nMessages
- i18nMessages

**Flags**: IR

---
## Attr: FormulaBuilder.autoHideCheckBox

### Description
CheckBox that, when selected, hides columns in the component that are used in this formula.

### Groups

- formulaFields

**Flags**: IR

---
## Attr: FormulaBuilder.warnDuplicateTitles

### Description
Should the user be showed a warning when the entered Title value already exists?

**Flags**: IRWA

---
## Attr: FormulaBuilder.field

### Description
The Field object representing the field being created or edited.

### Groups

- formulaFields

**Flags**: IR

---
## Attr: FormulaBuilder.testButton

### Description
Button to Test the formula by generating its function and executing it

### Groups

- formulaFields

**Flags**: IR

---
## Attr: FormulaBuilder.titleFieldTitle

### Description
The [TextItem.title](FormItem.md#attr-formitemtitle) of the [FormulaBuilder.titleField](#attr-formulabuildertitlefield).

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: FormulaBuilder.saveConfirmationPrompt

### Description
The text to display in the dialog that opens when there are unsaved changes and the user cancels the builder.

This is a dynamic string - text within `${...}` are dynamic variables and will be evaluated as JS code when the message is displayed.

Only one dynamic variable, builderType, is available and represents the type of this builder, either Formula or Summary.

The default output is:

`_Save changes to this [Formula/Summary]?_`

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: FormulaBuilder.anotherTestRequestedCancellationReason

### Description
Cancellation reason (see [CancellationController.cancellationReason](CancellationController.md#attr-cancellationcontrollercancellationreason)) used when another test is requested while the result for a previous test or save is still pending.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: FormulaBuilder.currentComponentFieldPrompt

### Description
The prompt to show when mouse hovers over a field supplied by the current component through [FormulaBuilder.targetRuleScope](#attr-formulabuildertargetrulescope).

The prompt is a dynamic string and is formatted like [Label.dynamicContents](Label.md#attr-labeldynamiccontents) where the following variables are available:

*   fieldName
*   componentName

### Groups

- i18nMessages

### See Also

- [FormulaBuilder.nearbyComponentFieldPrompt](#attr-formulabuildernearbycomponentfieldprompt)
- [FormulaBuilder.dataSourceFieldPrompt](#attr-formulabuilderdatasourcefieldprompt)

**Flags**: IR

---
## Attr: FormulaBuilder.warnDuplicateTitlesMessage

### Description
The message to display when warnDuplicateTitles is true This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed.

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: FormulaBuilder.cancelled

### Description
Was the builder operation cancelled? Set to true when the user cancels with the cancel button or the dialog's close-button.

### Groups

- formulaFields

**Flags**: R

---
## Attr: FormulaBuilder.cancelButtonTitle

### Description
The default title for the "Cancel" button.

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: FormulaBuilder.instructions

### Description
Form displaying the instruction text (see [FormulaBuilder.instructionsTextStart](#attr-formulabuilderinstructionstextstart)) above the fieldKey grid.

**Flags**: IR

---
## Attr: FormulaBuilder.dataSource

### Description
DataSource providing the available fields for the formulaBuilder.

By default the formulaBuilder will include **only** fields of numeric type or derived from a numeric type. Set [FormulaBuilder.fields](#attr-formulabuilderfields) to override this.

### Groups

- formulaFields

**Flags**: IRW

---
## Attr: FormulaBuilder.samplePrompt

### Description
This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed.

Default value returns

`_For Record: + the value of the rows title-field   Output: + the result of he generated function   _`

### Groups

- i18nMessages

### See Also

- [FormulaBuilder.ruleContextTitle](#attr-formulabuilderrulecontexttitle)

**Flags**: IRWA

---
## Attr: FormulaBuilder.defaultErrorText

### Description
If an invalid builder prompt is displayed, but no explicit error message was returned when attempting to evaluate the formula, this string will be used as a default.

### Groups

- i18nMessages

### See Also

- [FormulaBuilder.invalidBuilderPrompt](#attr-formulabuilderinvalidbuilderprompt)

**Flags**: IRW

---
## Attr: FormulaBuilder.autoHideCheckBoxLabel

### Description
Text label for the checkbox that allows the user to automatically hide the fields used in the formula.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: FormulaBuilder.testRecord

### Description
Record to use when testing the formula dynamically (if [FormulaBuilder.autoTest](#attr-formulabuilderautotest) is enabled) or when showing samples of formula output.

If not specified, the selected record in the component that launched the FormulaBuilder will be used, or if there's no selection, the first visible row, or with no component, a dummy data row derived automatically from the provided DataSource.

### Groups

- formulaFields

**Flags**: IRA

---
## Attr: FormulaBuilder.instructionsTextStart

### Description
The text to display as a preamble to the instruction text that appears in the [instructions](#attr-formulabuilderinstructions).

This is a dynamic string - text within `${...}` are dynamic variables and will be evaluated as JS code when the message is displayed.

Only one dynamic variable, builderType, is available and represents the type of this builder - either Formula or Summary.

Default value returns

`_The following fields are available for use in this [Formula/Summary]_`

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: FormulaBuilder.helpWindowTitle

### Description
The title for the window that opens when the [Help icon](#attr-formulabuilderhelpicon) is clicked.

This is a dynamic string - text within `${...}` are dynamic variables and will be evaluated as JS code when the message is displayed.

Only one dynamic variable, builderType, is available and represents the type of this builder, either Formula or Summary.

The default output is:

`_[Formula/Summary] Help_`

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: FormulaBuilder.invalidGeneratedFunctionPrompt

### Description
When [testFunction](#method-formulabuildertestfunction) reports an attempt to generate a function from an invalid formula, this is the text to display in the [message-label](#attr-formulabuildermessagelabel).

This is a dynamic string - text within `${...}` are dynamic variables and will be evaluated as JS code when the message is displayed.

Only one dynamic variable, builderType, is available and represents the type of this builder, either Formula or Summary.

The default output is:

`_The generated function is invalid - Check your [Formula/Summary] and retry._`

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: FormulaBuilder.showHelpIcon

### Description
Whether to show the help icon that appears after the [FormulaBuilder.formulaField](#attr-formulabuilderformulafield).

### Groups

- formulaFields

**Flags**: IR

---
## Attr: FormulaBuilder.fields

### Description
Set this to override the underlying set of available fields.

### Groups

- formulaFields

**Flags**: IRW

---
## Attr: FormulaBuilder.ruleContextTitle

### Description
A string to display in the [FormulaBuilder.samplePrompt](#attr-formulabuildersampleprompt) as the `${title}` when the formula or summary is being evaluated against the values in the [FormulaBuilder.targetRuleScope](#attr-formulabuildertargetrulescope).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: FormulaBuilder.userSavedCancellationReason

### Description
Cancellation reason (see [CancellationController.cancellationReason](CancellationController.md#attr-cancellationcontrollercancellationreason)) used when the user clicks the [FormulaBuilder.saveButton](#attr-formulabuildersavebutton), signaling that they are no longer interested in any pending result(s).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: FormulaBuilder.testButtonHoverContents

### Description
Hover contents to display for the [FormulaBuilder.testButton](#attr-formulabuildertestbutton).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: FormulaBuilder.dataSourceFieldPrompt

### Description
The prompt to show when mouse hovers over a field supplied by a DataSource through [FormulaBuilder.targetRuleScope](#attr-formulabuildertargetrulescope).

The prompt is a dynamic string and is formatted like [Label.dynamicContents](Label.md#attr-labeldynamiccontents) where the following variables are available:

*   fieldName
*   dataSource

### Groups

- i18nMessages

### See Also

- [FormulaBuilder.currentComponentFieldPrompt](#attr-formulabuildercurrentcomponentfieldprompt)
- [FormulaBuilder.nearbyComponentFieldPrompt](#attr-formulabuildernearbycomponentfieldprompt)

**Flags**: IR

---
## Attr: FormulaBuilder.cancelButton

### Description
Button to Cancel this FormulaBuilder. The formula is not tested, formulaBuilder.cancelled is set to true and formulaBuilder.fireOnClose is fired.

### Groups

- formulaFields

**Flags**: IR

---
## Attr: FormulaBuilder.mathFunctions

### Description
The list of math functions available in this FormulaBuilder, as an array of [MathFunction](#mathfunction) names.

The following function list is supported in FormulaBuilders by default: min(), max(), round(), ceil(), floor(), abs(), pow(), sin(), cos(), tan(), ln() and log().

### Groups

- formulaFields

**Flags**: IR

---
## Attr: FormulaBuilder.editMode

### Description
Are we editing an existing field?

### Groups

- formulaFields

**Flags**: IR

---
## Attr: FormulaBuilder.nearbyComponentFieldPrompt

### Description
The prompt to show when mouse hovers over a field supplied by a nearby component through [FormulaBuilder.targetRuleScope](#attr-formulabuildertargetrulescope).

The prompt is a dynamic string and is formatted like [Label.dynamicContents](Label.md#attr-labeldynamiccontents) where the following variables are available:

*   fieldName
*   componentName

### Groups

- i18nMessages

### See Also

- [FormulaBuilder.currentComponentFieldPrompt](#attr-formulabuildercurrentcomponentfieldprompt)
- [FormulaBuilder.dataSourceFieldPrompt](#attr-formulabuilderdatasourcefieldprompt)

**Flags**: IR

---
## Attr: FormulaBuilder.saveAddAnotherButtonTitle

### Description
The default title for the "Save & Add Another" button.

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: FormulaBuilder.saveAddAnotherButton

### Description
Button to Save the formula, by generating its function, testing it and firing formulaBuilder.fireOnClose, and then start editing another, new one.

### Groups

- formulaFields

**Flags**: IR

---
## Attr: FormulaBuilder.autoTestDelay

### Description
When [FormulaBuilder.autoTest](#attr-formulabuilderautotest) is true, this property indicates the delay in milliseconds between a user pausing and [testFunction()](#method-formulabuildertestfunction) being called.

The default is 200 milliseconds.

### Groups

- formulaFields

**Flags**: IRWA

---
## Attr: FormulaBuilder.valueSuffix

### Description
The suffix to apply to the variable that is inserted in response to a record click in the grid that shows the list of available fields.

### Groups

- formulaFields

**Flags**: IR

---
## Attr: FormulaBuilder.testButtonTitle

### Description
The default title for the "Test" button.

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: FormulaBuilder.autoTest

### Description
When set to true, automatically tests the formula by calling [testFunction()](#method-formulabuildertestfunction) whenever typing into the [formulaField](#attr-formulabuilderformulafield) pauses.

The default is true.

### Groups

- formulaFields

**Flags**: IRWA

---
## Attr: FormulaBuilder.showAutoHideCheckBox

### Description
Whether to show a checkbox offering the user the ability to automatically hide any fields involved in the formula.

### Groups

- formulaFields

**Flags**: IR

---
## Attr: FormulaBuilder.targetRuleScope

### Description
[Canvas.ruleScope](Canvas.md#attr-canvasrulescope) providing the list of available fields for the formulaBuilder.

By default the formulaBuilder will include **only** fields of numeric type or derived from a numeric type. Set [FormulaBuilder.fields](#attr-formulabuilderfields) to override this.

**Flags**: IRA

---
## Attr: FormulaBuilder.saveButtonTitle

### Description
The default title for the "Save" button.

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: FormulaBuilder.keyColumnTitle

### Description
The default title for the "Key" column in [FormulaBuilder.fields](#attr-formulabuilderfields).

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: FormulaBuilder.testButtonHoverContents_cantTest

### Description
Hover contents to display for the [FormulaBuilder.testButton](#attr-formulabuildertestbutton) when this `FormulaBuilder` is unable to run a test.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: FormulaBuilder.sourceFieldColumnTitle

### Description
The default title for the "Source Field" column in in [FormulaBuilder.fields](#attr-formulabuilderfields).

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: FormulaBuilder.valuePrefix

### Description
The prefix to apply to the variable that is inserted in response to a record click in the grid that shows the list of available fields.

### Groups

- formulaFields

**Flags**: IR

---
## Attr: FormulaBuilder.useSingleLetterKey

### Description
Whether to use the legacy approach in the builder of assigning each field used in the formula or summary a key from the sequence A, B, C, ... Z, AA, AB, .... This approach will almost guarantee no collisions with registered math functions, but requires that the [formula key map](UserFormula.md#attr-userformulaformulavars) or [summary key map](UserSummary.md#attr-usersummarysummaryvars) be populated with a key for every field used.

If unset, field names can be used directly in the formula or summary and aren't required to be in the key map. The builder will add key map bindings only for collisions between field names and math functions (or reserved words like "record"). For collisions, field name keys will be created as `<fieldName>`Field\[`<k>`\]. That is, the field name will be suffixed with "Field", and then an integer optionally added if there's still a collision. So, for example, a field named "foo" might be bound to the key "fooField" or "fooField5".

**Flags**: IR

---
## Attr: FormulaBuilder.formulaField

### Description
TextItem that users type into when entering a formula.

### Groups

- formulaFields

**Flags**: IR

---
## Attr: FormulaBuilder.invalidBuilderPrompt

### Description
When [testFunction](#method-formulabuildertestfunction) reports an invalid formula, this attribute provides the error-text to display in the [message-label](#attr-formulabuildermessagelabel).

This is a dynamic string - text within `${...}` are dynamic variables and will be evaluated as JS code when the message is displayed.

The dynamic variables in this case, builderType and errorText, represent the type of this builder, either Formula or Summary, and the description of the error, respectively.

The default output is:

`_Invalid [Formula/Summary]: + the description of the error detected_`

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: FormulaBuilder.messageLabel

### Description
Label used for displaying messages related to the validity of the current formula.

### Groups

- formulaFields

**Flags**: IR

---
## Attr: FormulaBuilder.saveButton

### Description
Button to Save the formula, by generating its function, testing it and firing formulaBuilder.fireOnClose

### Groups

- formulaFields

**Flags**: IR

---
## Method: FormulaBuilder.getSamplePrompt

### Description
Evaluates and returns the dynamic [FormulaBuilder.samplePrompt](#attr-formulabuildersampleprompt) string which is displayed beneath the formulaField and updated when typing pauses.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| result | [TestFunctionResult](#type-testfunctionresult) | false | — | The return value from a call to testFunction(). |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — Caption displaying dynamic row-title and the result of the formula

### Groups

- i18nMessages

---
## Method: FormulaBuilder.getUpdatedFieldObject

### Description
Returns the entire property-set for the updated field, including title and formula-related properties

### Returns

`[Field](#type-field)` — The original field along with the updated title and formula

### Groups

- formulaFields

---
## Method: FormulaBuilder.save

### Description
Call to finish working, test the formula and call [fireOnClose()](#method-formulabuilderfireonclose). Called automatically when the Save button is clicked.

### Groups

- formulaFields

---
## Method: FormulaBuilder.testFunction

### Description
Test the formula by generating its function and trying to run it.

### Returns

`[String](#type-string)` — result of the function

### Groups

- formulaFields

---
## Method: FormulaBuilder.getHelpText

### Description
Call to retrieve the text the FormulaBuilder would show by default for help, or override to provide alternate help text.

### Returns

`[String](#type-string)` — The results of getHoverText()

### Groups

- formulaFields

---
## Method: FormulaBuilder.getTestRecord

### Description
Gets the [test record](#attr-formulabuildertestrecord) for this formula.

### Returns

`[Record](#type-record)` — the [testRecord](#attr-formulabuildertestrecord) for this formula

### Groups

- formulaFields

---
## Method: FormulaBuilder.saveAddAnother

### Description
Call to finish working, test the formula and call [fireOnClose()](#method-formulabuilderfireonclose). If the formula saves ok, don't close the builder but instead reset it, ready to add a new formula-field.

### Groups

- formulaFields

---
## Method: FormulaBuilder.fireOnClose

### Description
Override to execute a callback function when the Formula is Cancelled or Saved.

### Groups

- formulaFields

**Flags**: A

---
## Method: FormulaBuilder.setFormula

### Description
Call to set the formula-string in this FormulaBuilder.

Note that calling setFormula() will update the UI, generate the formula's function and test it automatically.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | The new formula-string for this builder |

### Groups

- formulaFields

---
