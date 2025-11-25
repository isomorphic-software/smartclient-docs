# AnswerEngineOperation Documentation

[← Back to API Index](../main.md)

---

## Class: AnswerEngineOperation

*Inherits from:* [PausableAsyncOperation](#class-pausableasyncoperation)

### Description
Represents an Answer Engine operation.

### Groups

- answerEngine

---
## ClassAttr: AnswerEngineOperation.allDashboardComponentTypes

### Description
—

**Flags**: R

---
## Attr: AnswerEngineOperation.dataQuestion

### Description
The data question that is the subject of this Answer Engine operation. This is required to be non-`null`.

**Flags**: IR

---
## Attr: AnswerEngineOperation.autoShowResult

### Description
Whether the result should be automatically shown to the user.

**Flags**: IR

---
## Attr: AnswerEngineOperation.showNotify

### Description
Whether to show a notify for this Answer Engine operation.

If [AnswerEngineOperation.autoShowResult](#attr-answerengineoperationautoshowresult) is also enabled, the notify will be dismissed when the result is shown.

**Flags**: IR

---
## Attr: AnswerEngineOperation.dataSources

### Description
The array of available data sources.

**Flags**: IR

---
## Attr: AnswerEngineOperation.maxRecordsPerQuery

### Description
The maximum number of records that may be requested per query. Must be a positive integer.

**Flags**: IR

---
## Attr: AnswerEngineOperation.notifyMessageId

### Description
If [AnswerEngineOperation.showNotify](#attr-answerengineoperationshownotify) is `true` and a notify is shown, its message ID.

**Flags**: R

---
