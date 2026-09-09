# WorkflowExplorationEntry Documentation

[← Back to API Index](../reference.md)

---

## Attr: WorkflowExplorationEntry.rowCount

### Description
Present only when [status](#attr-workflowexplorationentrystatus) is `"succeeded"` - the number of rows the exploratory fetch returned.

**Flags**: IR

---
## Attr: WorkflowExplorationEntry.sample

### Description
Present only on the most recent entry in the history array, and only when [status](#attr-workflowexplorationentrystatus) is `"succeeded"` - the real data returned by the exploratory fetch. Earlier entries are trimmed to [summary](#attr-workflowexplorationentrysummary) only, so history size stays bounded regardless of how large individual result samples are.

**Flags**: IR

---
## Attr: WorkflowExplorationEntry.status

### Description
One of `"succeeded"`, `"failed"`, or `"refused"` (the candidate step did not qualify for exploration - see [explorationSettings](WorkflowBuilderCoTParams.md#attr-workflowbuildercotparamsexplorationsettings)).

**Flags**: IR

---
## Attr: WorkflowExplorationEntry.dataSourceID

### Description
The DataSource the explored candidate step targeted.

**Flags**: IR

---
## Attr: WorkflowExplorationEntry.taskType

### Description
The Task class of the explored candidate step.

**Flags**: IR

---
## Attr: WorkflowExplorationEntry.reason

### Description
Present only when [status](#attr-workflowexplorationentrystatus) is `"refused"` - why the candidate step did not qualify for exploration.

**Flags**: IR

---
## Attr: WorkflowExplorationEntry.summary

### Description
A one-line text summary of this entry - see +link{WorkflowBuilderCoTProcess. summarizeExploration()}. Always present.

**Flags**: IR

---
