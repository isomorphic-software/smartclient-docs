# UnexpectedErrorTask Documentation

[← Back to API Index](../reference.md)

---

## Class: UnexpectedErrorTask

*Inherits from:* [Task](Task.md#class-task)

### Description
Default [Process-level error task](Process.md#attr-processerrortask) - reached when a task fails with no [failureElement](DSRequestTask.md#attr-dsrequesttaskfailureelement) of its own and its owning Process resolves an effective error task (see [Process.getEffectiveErrorTask](Process.md#method-processgeteffectiveerrortask)), which by default happens automatically because [Process.defaultErrorHandlingEnabled](Process.md#classattr-processdefaulterrorhandlingenabled) is `true`.

Default behavior: build an [ErrorContext](#type-errorcontext) from whatever the framework knows about the failure, classify it via [Process.classifyError](Process.md#classmethod-processclassifyerror), show the standard centralized error dialog for an "unexpected" classification (skipped for "expected"), then call [Process.fail](Process.md#method-processfail) so [Process.failed](Process.md#method-processfailed) fires - giving the Process a real, distinguishable "did not complete successfully" signal instead of silently reaching [finished()](Process.md#method-processfinished) with empty output.

Subclass to change what happens before/after the default handling - for example, logging every failure to an audit DataSource, reclassifying which errors count as "expected" for your application (see [Process.classifyError](Process.md#classmethod-processclassifyerror)), or retrying a bounded number of times before falling through to the default. [UnexpectedErrorTask.handleUnexpectedError](#method-unexpectederrortaskhandleunexpectederror) is the reusable entry point for the classify-dialog-fail sequence; override [executeElement()](ProcessElement.md#method-processelementexecuteelement) to add behavior around it, or replace [Process.getDefaultErrorTask](Process.md#classmethod-processgetdefaulterrortask) to install a different default framework-wide.

### Groups

- serverProcess

---
## Method: UnexpectedErrorTask.handleUnexpectedError

### Description
Builds an [ErrorContext](#type-errorcontext), classifies it via [Process.classifyError](Process.md#classmethod-processclassifyerror), conditionally shows the standard centralized error dialog, and calls [Process.fail](Process.md#method-processfail). Exposed as a separate method (rather than folded directly into [executeElement()](ProcessElement.md#method-processelementexecuteelement)) so a subclass that needs to do asynchronous work first (for example, adding an audit-log record) can call this from its own completion callback instead of duplicating the sequence.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| process | [Process](#type-process) | false | — | the Process handling the failure |

---
