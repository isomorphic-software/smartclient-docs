# QuartzManager Documentation

[← Back to API Index](../reference.md)

---

## Class: QuartzManager

### Description
A simple user interface for managing scheduled jobs via [Quartz DataSource](../kb_topics/quartzAdapters.md#kb-topic-quartz-datasources) adapters, as seen in the Scheduler tab of the [Admin Console](../kb_topics/adminConsole.md#kb-topic-admin-console). Exercise caution when exposing any such feature to end users.

---
## Attr: QuartzManager.readOnlyJobGroups

### Description
Job groups whose jobs and triggers are listed but cannot be changed here: their buttons are disabled, their triggers cannot be edited and [QuartzManager.readOnlyJobNote](#attr-quartzmanagerreadonlyjobnote) explains why. The server refuses such changes as well. The `reportDelivery` group holds the jobs of [scheduled report delivery](../kb_topics/scheduledDelivery.md#kb-topic-report-delivery-and-scheduling), which are managed from the report itself.

**Flags**: IR

---
## Attr: QuartzManager.readOnlyJobNote

### Description
Shown under the jobs grid while a job in one of the [QuartzManager.readOnlyJobGroups](#attr-quartzmanagerreadonlyjobgroups) is selected.

**Flags**: R

---
## Attr: QuartzManager.readOnlyJobMessage

### Description
Text of the [QuartzManager.readOnlyJobNote](#attr-quartzmanagerreadonlyjobnote).

### Groups

- i18nMessages

**Flags**: IR

---
## Method: QuartzManager.isReadOnlyJob

### Description
Whether jobs and triggers of the given job group are read-only here ([QuartzManager.readOnlyJobGroups](#attr-quartzmanagerreadonlyjobgroups)).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| jobGroup | [String](#type-string) | false | — | group of a job, or the `jobGroup` of a trigger |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the job cannot be changed here

---
