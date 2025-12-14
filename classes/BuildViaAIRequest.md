# BuildViaAIRequest Documentation

[← Back to API Index](../reference.md)

---

## Attr: BuildViaAIRequest.userCanCancel

### Description
Whether the user can cancel the build-request. If [BuildViaAIRequest.showProgressDialog](#attr-buildviaairequestshowprogressdialog) is `true`, then the progress dialog will have a cancel button if `userCanCancel` is set.

Other user cancellation mechanisms may be added in the future, but `userCanCancel` will be respected.

**Flags**: IR

---
## Attr: BuildViaAIRequest.userAIRequest

### Description
The user's request to AI in the context of this build-via-AI operation.

**Flags**: IR

---
## Attr: BuildViaAIRequest.showProgressDialog

### Description
Whether to show a progress dialog to inform the user about the processing of the build-request.

**Flags**: IR

---
## Attr: BuildViaAIRequest.maxRetries

### Description
The maximum number of retries of any one particular request to an AI engine.

Note that multiple AI requests may be involved in processing the build request. This limit is the maximum number of retries of any one request. For example, if there are 2 requests made to AI, then each one would be submitted at most `1 + maxRetries` number of times for up to `2 * (1 + maxRetries)` total requests.

**Flags**: IR

---
## Attr: BuildViaAIRequest.progressCallback

### Description
A callback to call with information about progress on an ongoing build-via-AI operation.

**Flags**: IR

---
## Attr: BuildViaAIRequest.progressDialogProperties

### Description
When [showing a progress dialog](#attr-buildviaairequestshowprogressdialog), the [BuildViaAIProgressDialog](../reference.md#class-buildviaaiprogressdialog) properties to apply.

**Flags**: IRA

---
