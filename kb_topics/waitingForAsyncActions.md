# Waiting for asynchronous actions

[← Back to API Index](../reference.md)

---

## KB Topic: Waiting for asynchronous actions

### Description
In SmartClient automated testing, certain actions may trigger asynchronous operations, such as DataSource requests, deferred UI updates, or queued redraws. Attempting to interact with application components before these operations complete can cause unstable or inconsistent test results.

The [AutoTest.waitForSystemDone](../classes/AutoTest.md#classmethod-autotestwaitforsystemdone) API ensures that all pending asynchronous SmartClient actions have completed before proceeding. This method relies on [AutoTest.isSystemDone](../classes/AutoTest.md#classmethod-autotestissystemdone) to determine when the system is ready for further input.

**Key considerations**

*   **System readiness:** Waiting for the framework to report that it is "system done" ensures that all queued SmartClient actions have been processed before continuing.
*   **Limitations:** [AutoTest.isSystemDone](../classes/AutoTest.md#classmethod-autotestissystemdone) only tracks asynchronous processes managed by SmartClient. Actions outside of SmartClient’s control (e.g., third-party widget rendering, non-SmartClient network requests) may require additional waits.
*   **Targeted waits:** In scenarios where only a specific component’s readiness matters, you can wait for a specific element using [AutoTest.waitForElement](../classes/AutoTest.md#classmethod-autotestwaitforelement) instead of waiting for the entire system.
*   **Timeout control:** Waiting methods support timeouts to avoid indefinite waits if a condition cannot be satisfied.

---
