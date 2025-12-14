# Timer Documentation

[← Back to API Index](../reference.md)

---

## Class: Timer

### Description
The Timer class provides a predictable cross-browser system for creating timed events.

---
## ClassMethod: Timer.setTimeout

### Description
Execute an action in a given amount of time. This method wraps the native setTimeout() method, correcting for browser-specific memory leaks.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| action | [String Expression](#type-string-expression)|[Function](#type-function) | false | — | Function to be called when delay has elapsed. Can also be a string representation of an expression. Passing a string is preferred. |
| delay | [number](#type-number) | false | — | Time until action is executed (in milliseconds). If not specified, the default is 100 milliseconds. |

### Returns

`[TimerEvent](#type-timerevent)` — Reference to the timerEvent created. Note that this reference is provided only so that it can be used as an argument for Timer.clear().

### See Also

- [Timer.clear](#classmethod-timerclear)

---
## ClassMethod: Timer.clear

### Description
Cancels the processing of a timerEvent if it has not already fired.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| timerEvent | [Object](../reference.md#type-object) | false | — | timerEvent object previously returned from Timer.setTimeout() |

---
