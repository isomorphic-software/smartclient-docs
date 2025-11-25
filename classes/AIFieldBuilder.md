# AIFieldBuilder Documentation

[← Back to API Index](../main.md)

---

## Class: AIFieldBuilder

*Inherits from:* [SummaryBuilder](SummaryBuilder.md#class-summarybuilder)

### Description
Shows an interface allowing a user to enter the description of a new component field to be populated via AI. The description of an existing AI field may also be edited.

---
## Attr: AIFieldBuilder.pendingSuggestTitleHint

### Description
The hint to display in the [titleField](SummaryBuilder.md#attr-summarybuildertitlefield) when a suggested title is being generated.

### Groups

- i18nMessages

### See Also

- [AIFieldBuilder.initialAutoSuggestTitleHint](#attr-aifieldbuilderinitialautosuggesttitlehint)

**Flags**: IR

---
## Attr: AIFieldBuilder.testButtonHoverContents_cantTestWithoutData

### Description
Hover contents to display for the [testButton](FormulaBuilder.md#attr-formulabuildertestbutton) when this `AIFieldBuilder` is unable to run a test because of a lack of data.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: AIFieldBuilder.nonSuccessfulSuggestTitleHint

### Description
The hint to display in the [titleField](SummaryBuilder.md#attr-summarybuildertitlefield) when a suggested title could not be generated.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: AIFieldBuilder.testButtonHoverContents

### Description
Hover contents to display for the [testButton](FormulaBuilder.md#attr-formulabuildertestbutton).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: AIFieldBuilder.testButtonHoverContents_cantTest

### Description
Hover contents to display for the [testButton](FormulaBuilder.md#attr-formulabuildertestbutton) when this `AIFieldBuilder` is unable to run a test.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: AIFieldBuilder.initialAutoSuggestTitleHint

### Description
When [AIFieldBuilder.autoSuggestTitle](#attr-aifieldbuilderautosuggesttitle) is active, the initial hint to display for the [titleField](SummaryBuilder.md#attr-summarybuildertitlefield).

### Groups

- i18nMessages

### See Also

- [AIFieldBuilder.pendingSuggestTitleHint](#attr-aifieldbuilderpendingsuggesttitlehint)
- [AIFieldBuilder.nonSuccessfulSuggestTitleHint](#attr-aifieldbuildernonsuccessfulsuggesttitlehint)
- [AIFieldBuilder.suggestedTitleHint](#attr-aifieldbuildersuggestedtitlehint)

**Flags**: IR

---
## Attr: AIFieldBuilder.suggestTitleThreshold

### Description
The threshold length of the description for suggesting a title.

### See Also

- [AIFieldBuilder.autoSuggestTitle](#attr-aifieldbuilderautosuggesttitle)

**Flags**: IR

---
## Attr: AIFieldBuilder.instructionsTextStart

### Description
Text providing instructions for using the `AIFieldBuilder`.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: AIFieldBuilder.autoSuggestTitleDelay

### Description
The delay in milliseconds to wait before AI is asked to suggest the title.

### See Also

- [AIFieldBuilder.autoSuggestTitle](#attr-aifieldbuilderautosuggesttitle)

**Flags**: IR

---
## Attr: AIFieldBuilder.anotherSuggestedTitleRequestedCancellationReason

### Description
Cancellation reason (see [CancellationController.cancellationReason](CancellationController.md#attr-cancellationcontrollercancellationreason)) used when another suggested title is requested while the result for a previous suggest-title-request is still pending.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: AIFieldBuilder.suggestedTitleHint

### Description
The hint to display in the [titleField](SummaryBuilder.md#attr-summarybuildertitlefield) with the AI-generated title.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: AIFieldBuilder.autoSuggestTitle

### Description
If not explicitly set to `false`, the user has not already typed a title, and the user's description is longer than [AIFieldBuilder.suggestTitleThreshold](#attr-aifieldbuildersuggesttitlethreshold), then AI will be asked to suggest the title for the AI-generated field.

### See Also

- [AIFieldBuilder.autoSuggestTitleDelay](#attr-aifieldbuilderautosuggesttitledelay)

**Flags**: IRW

---
## Method: AIFieldBuilder.setAutoSuggestTitle

### Description
Setter for [AIFieldBuilder.autoSuggestTitle](#attr-aifieldbuilderautosuggesttitle).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| autoSuggestTitle | [Boolean](#type-boolean) | false | — | New value for `this.autoSuggestTitle`. |

---
