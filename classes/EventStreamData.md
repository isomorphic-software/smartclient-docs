# EventStreamData Documentation

[← Back to API Index](../reference.md)

---

## Attr: EventStreamData.nEvents

### Description
The total number of events captured by the stream since capturing [started](EventStream.md#method-eventstreamstart). This value may exceed the length of the reported [EventStreamData.events](#attr-eventstreamdataevents), which only contains the most recent events.

**Flags**: R

---
## Attr: EventStreamData.events

### Description
An array of the captured [event records](../reference.md#object-eventstreamevent) retained by the stream. Only the last [EventStream.maxSize](EventStream.md#attr-eventstreammaxsize) event records will be present, though more events may have been captured since capturing [started](EventStream.md#method-eventstreamstart).

Note that [EventStreamData](../reference.md#object-eventstreamdata) reported via an [error callback](Callbacks.md#method-callbackseventerrorcallback) will only contain events that have occurred after the last callback, for efficiency.

### See Also

- [EventStreamData.nEvents](#attr-eventstreamdatanevents)

**Flags**: R

---
## Attr: EventStreamData.startTime

### Description
A string representation of the `DateTime` when capturing for the stream [started](EventStream.md#method-eventstreamstart).

### See Also

- [EventStreamData.endTime](#attr-eventstreamdataendtime)

**Flags**: R

---
## Attr: EventStreamData.endTime

### Description
A string representation of the `DateTime` when capturing for the stream was [completed](EventStream.md#method-eventstreamend).

### See Also

- [EventStreamData.startTime](#attr-eventstreamdatastarttime)

**Flags**: R

---
