# UnexpectedErrorTask Documentation

[← Back to API Index](../reference.md)

---

## Class: UnexpectedErrorTask

*Inherits from:* [Task](Task.md#class-task)

### Description
Default [Process-level error task](Process.md#attr-processerrortask) - reached when a task fails with no [failureElement](DSRequestTask.md#attr-dsrequesttaskfailureelement) of its own and its owning Process resolves an effective error task (see [Process.getEffectiveErrorTask](Process.md#method-processgeteffectiveerrortask)), which by default happens automatically because [Process.defaultErrorHandlingEnabled](Process.md#classattr-processdefaulterrorhandlingenabled) is `true`.

Default behavior: build an [ErrorContext](#type-errorcontext) from whatever the framework knows about the failure, classify it via [Process.classifyError](Process.md#classmethod-processclassifyerror), show the standard centralized error dialog for an "unexpected" classification (skipped for "expected"), then call [Process.fail](Process.md#method-processfail) so [Process.failed](Process.md#method-processfailed) fires - giving the Process a real, distinguishable "did not complete successfully" signal instead of silently reaching [finished()](Process.md#method-processfinished) with empty output.

Subclass to change what happens before/after the default handling - for example, logging every failure to an audit DataSource, reclassifying which errors count as "expected" for your application (see [Process.classifyError](Process.md#classmethod-processclassifyerror)), or retrying a bounded number of times before falling through to the default. [UnexpectedErrorTask.handleUnexpectedError](#method-unexpectederrortaskhandleunexpectederror) is the reusable entry point for the classify-dialog-fail sequence; override [executeElement()](ProcessElement.md#method-processelementexecuteelement) to add behavior around it, or replace [Process.getDefaultErrorTask](Process.md#classmethod-processgetdefaulterrortask) to install a different default framework-wide. To customize just the message passed to [Process.fail](Process.md#method-processfail) (the common case - see the Showcase "AI Workflow Builder" sample's "Task-Level & Unexpected-Error Examples"), override [UnexpectedErrorTask.getUnexpectedErrorMessage](#method-unexpectederrortaskgetunexpectederrormessage) instead of reimplementing [UnexpectedErrorTask.handleUnexpectedError](#method-unexpectederrortaskhandleunexpectederror) wholesale. If that custom message is ALSO going to be visibly surfaced some other way (a custom UI element, a [Process.failed](Process.md#method-processfailed) handler), override [UnexpectedErrorTask.shouldShowDefaultErrorPopup](#method-unexpectederrortaskshouldshowdefaulterrorpopup) to return `false` and skip the redundant raw system dialog too.

### Groups

- serverProcess

---
## Method: UnexpectedErrorTask.buildErrorContext

### Description
Gathers every signal available about the failure that routed here into an [ErrorContext](#type-errorcontext) - the last task's recorded failure (if raised via [Process.fail](Process.md#method-processfail) or propagated from a [SubProcessTask](SubProcessTask.md#class-subprocesstask)'s child), the owning Process, the [ProcessElement](ProcessElement.md#class-processelement) that actually failed, and (for a DataSource-operation failure) the underlying request/response. Exposed as a separate, overridable method so a subclass or instance override can inspect or extend the context - see [UnexpectedErrorTask.handleUnexpectedError](#method-unexpectederrortaskhandleunexpectederror) and [UnexpectedErrorTask.getUnexpectedErrorMessage](#method-unexpectederrortaskgetunexpectederrormessage), both of which call this rather than assembling a context of their own.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| process | [Process](#type-process) | false | — | the Process handling the failure |

### Returns

`[ErrorContext](#type-errorcontext)` — every signal available about the failure

---
## Method: UnexpectedErrorTask.handleUnexpectedError

### Description
Builds an [ErrorContext](#type-errorcontext), classifies it via [Process.classifyError](Process.md#classmethod-processclassifyerror), conditionally shows the standard centralized error dialog (see [UnexpectedErrorTask.shouldShowDefaultErrorPopup](#method-unexpectederrortaskshouldshowdefaulterrorpopup)), computes the message via [UnexpectedErrorTask.getUnexpectedErrorMessage](#method-unexpectederrortaskgetunexpectederrormessage), and calls [Process.fail](Process.md#method-processfail). Exposed as a separate method (rather than folded directly into [executeElement()](ProcessElement.md#method-processelementexecuteelement)) so a subclass that needs to do asynchronous work first (for example, adding an audit-log record) can call this from its own completion callback instead of duplicating the sequence.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| process | [Process](#type-process) | false | — | the Process handling the failure |

---
## Method: UnexpectedErrorTask.shouldShowDefaultErrorPopup

### Description
Returns whether [UnexpectedErrorTask.handleUnexpectedError](#method-unexpectederrortaskhandleunexpectederror) should show the standard centralized error dialog ([RPCManager.runDefaultErrorHandling](RPCManager.md#classmethod-rpcmanagerrundefaulterrorhandling)) for this failure. Default implementation shows it for every failure [classified](Process.md#classmethod-processclassifyerror) as "unexpected" - skipped entirely for "expected" failures (e.g. validation errors), matching [Process.suppressDefaultErrorPopupWhenHandled](Process.md#classattr-processsuppressdefaulterrorpopupwhenhandled)'s own "only surface genuinely unexpected problems" philosophy, just one step further down the chain (that classAttr's own doc covers the ORIGINATING task's popup, not this one).

Override - directly in a subclass, or on a single instance the same way as [UnexpectedErrorTask.getUnexpectedErrorMessage](#method-unexpectederrortaskgetunexpectederrormessage) - to return `false` when your own `getUnexpectedErrorMessage()` override means the failure will already be visibly surfaced some other way (a custom UI element, a [Process.failed](Process.md#method-processfailed) handler, etc.) and the raw system dialog would be redundant - see the Showcase "AI Workflow Builder" sample's "Task-Level & Unexpected-Error Examples" for exactly this pairing. Independent of [UnexpectedErrorTask.getUnexpectedErrorMessage](#method-unexpectederrortaskgetunexpectederrormessage): overriding one does not affect the other, so [Process.fail](Process.md#method-processfail) still receives a properly classified `code` and message regardless of this method's answer.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| context | [ErrorContext](#type-errorcontext) | false | — | as built by [UnexpectedErrorTask.buildErrorContext](#method-unexpectederrortaskbuilderrorcontext) |
| category | [ErrorCategory](../reference_2.md#type-errorcategory) | false | — | as returned by [Process.classifyError](Process.md#classmethod-processclassifyerror) |

### Returns

`[Boolean](#type-boolean)` — true to show the default error dialog

---
## Method: UnexpectedErrorTask.getUnexpectedErrorMessage

### Description
Returns the human-readable message [UnexpectedErrorTask.handleUnexpectedError](#method-unexpectederrortaskhandleunexpectederror) passes to [Process.fail](Process.md#method-processfail). Default implementation surfaces the failure's own message if it has one, else the standard RPC error message for a DataSource-operation failure. Override - directly in a subclass, or on a single instance (see the Showcase "AI Workflow Builder" sample's "Task-Level & Unexpected-Error Examples", which labels which mechanism produced the message) - to customize just the message while reusing handleUnexpectedError()'s classify/dialog logic unchanged; call [Class.Super](Class.md#method-classsuper) to build on the default message rather than replacing it outright.

For an instance override, use a plain property assignment on the still-plain [Process.errorTask](Process.md#attr-processerrortask) config object (before [Process._materializeErrorTask](#method-process_materializeerrortask) turns it into a real instance) rather than [Class.addProperties](Class.md#method-classaddproperties) - the config object has no such method yet, and a function property on it is exactly how [ClassFactory.newInstance](ClassFactory.md#classmethod-classfactorynewinstance) wires up a Super()-capable method override at create() time regardless.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| context | [ErrorContext](#type-errorcontext) | false | — | as built by [UnexpectedErrorTask.buildErrorContext](#method-unexpectederrortaskbuilderrorcontext) |
| category | [ErrorCategory](../reference_2.md#type-errorcategory) | false | — | as returned by [Process.classifyError](Process.md#classmethod-processclassifyerror) |
| code | [String](#type-string) | false | — | the ProcessFailure code that will be passed to process.fail() |

### Returns

`[String](#type-string)` — human-readable failure message

---
