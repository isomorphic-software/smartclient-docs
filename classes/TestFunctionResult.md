# TestFunctionResult Documentation

[← Back to API Index](../reference.md)

---

## Attr: TestFunctionResult.record

### Description
Set to the record that was used when testing the generated function. This is the record selected by [FormulaBuilder.getTestRecord](FormulaBuilder.md#method-formulabuildergettestrecord).

### Groups

- formulaFields

**Flags**: IRW

---
## Attr: TestFunctionResult.result

### Description
When a formula or summary format is valid, _result_ contains the result returned by the generated function when it was executed.

### Groups

- formulaFields

**Flags**: IRW

---
## Attr: TestFunctionResult.errorText

### Description
If the formula or summary format caused a JavaScript error, this contains the JavaScript error text.

### Groups

- formulaFields

**Flags**: IRW

---
## Attr: TestFunctionResult.failedGeneration

### Description
Set to true if there is a syntax error in the formula or summary being checked.

When set to true, [TestFunctionResult.errorText](#attr-testfunctionresulterrortext) contains the exception message.

### Groups

- formulaFields

**Flags**: IRW

---
## Attr: TestFunctionResult.emptyTestValue

### Description
Set to true if the formula or summary definition passed in was empty.

### Groups

- formulaFields

**Flags**: IRW

---
## Attr: TestFunctionResult.failedExecution

### Description
Set to true if calling the formula or summary format resulted in a JavaScript Error. This would generally indicate a reference to non-existent data values. See [TestFunctionResult.failedGeneration](#attr-testfunctionresultfailedgeneration) for other types of failure.

When set to true, [TestFunctionResult.errorText](#attr-testfunctionresulterrortext) contains the exception message.

### Groups

- formulaFields

**Flags**: IRW

---
