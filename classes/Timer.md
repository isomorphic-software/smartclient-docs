# Timer Documentation

[← Back to API Index](../main.md)

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
## ClassMethod: Timer.getTimerTrace

### Description
Returns the stack trace showing where the current timer was originally set via [Timer.setTimeout](#classmethod-timersettimeout). This is useful for debugging and error reporting, as it allows you to trace back through nested setTimeout() calls to understand the chain of events that led to the current code execution.

This method only returns meaningful results when called from within a timer callback (a function passed to [Timer.setTimeout](#classmethod-timersettimeout)). It returns null if called outside of a timer callback, or if timer trace capture was not enabled.

Timer traces are automatically captured for most timers in development mode. In production, enable timer trace capture by setting the log priority for the "timerTrace" category to DEBUG:

```
   isc.Log.setPriority("timerTrace", "DEBUG");
 
```

See [prodErrorReport](../kb_topics/prodErrorReport.md#kb-topic-production-error-reporting) for more information on using this API as part of comprehensive error reporting.

### Returns

`[String](#type-string)` — Stack trace showing where the current timer was set, or null if not available

### Groups

- prodErrorReport

---
## ClassMethod: Timer.clear

### Description
Cancels the processing of a timerEvent if it has not already fired.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| timerEvent | [Object](../main.md#type-object) | false | — | timerEvent object previously returned from Timer.setTimeout() |

---
