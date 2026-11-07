# Dual Input Mode

[← Back to API Index](../reference.md)

---

## KB Topic: Dual Input Mode

### Description
"Dual input mode" is how SmartClient handles hardware where both a mouse (or touchpad) and a touch screen deliver events to the same page: Microsoft Surface and other Windows touch-screen machines, Chromebooks with touch screens, and Linux tablets or touch-screen laptops. In this mode native mouse events and native touch events are both accepted, and only the duplicate mouse events that browsers synthesize from each touch are discarded, so a tap, a click and a drag all work whichever device produced them. Components take their touch-oriented defaults (a wider scrollbar grab area, larger drag thresholds, no rollover highlighting until the mouse moves) and show custom scrollbars rather than relying on native touch scrolling.

The other two input modes are "mouse only", the default for a desktop browser, and "touch only", the default on phones and tablets running a mobile OS, where native mouse events are ignored entirely because they are always synthesized from touches.

#### When dual input mode is used
[Browser.supportsDualInput](../classes/Browser.md#classattr-browsersupportsdualinput) reports whether the platform qualifies and [Browser.hasDualInput](../classes/Browser.md#classattr-browserhasdualinput) whether the mode is currently active. How the mode turns on depends on the operating system:

*   On **Windows 8+** and **Chrome OS** the page starts in mouse-only mode and switches to dual input mode when the first native touch event arrives, because a browser on these systems can report a touch screen that is never actually used.
*   On **desktop Linux** ([Browser.isDesktopLinux](../classes/Browser.md#classattr-browserisdesktoplinux)) the page starts in dual input mode whenever the browser reports a touch screen via `navigator.maxTouchPoints`, so the mode is settled before any component is drawn. Android Chrome with "request desktop site" enabled identifies itself as desktop Linux and is handled the same way.

Supported browsers are Chrome (including other Chromium-based browsers) and Firefox on every platform listed, plus IE11 and legacy Edge on Windows.

#### The `isc_useDualInput` global
To override the automatic behavior, set `window.isc_useDualInput` in a ``<script>`` block _before_ the SmartClient modules are loaded:

*   `true` turns dual input mode on from page load instead of waiting for the first touch event. Use this on hardware SmartClient does not recognize where taps are accepted but mouse clicks are ignored, or the reverse. The browser must still report a touch screen; the global does not add touch handling where none was detected.
*   `false` disables dual input mode entirely: [Browser.supportsDualInput](../classes/Browser.md#classattr-browsersupportsdualinput) becomes `false` and the page uses mouse-only or touch-only handling according to [Browser.isTouch](../classes/Browser.md#classattr-browseristouch).

The global is read once as the modules load, so it cannot be changed at runtime.

Dragging in a grid that also touch-scrolls is covered by [ListGrid.showDragHandles](../classes/ListGrid_2.md#method-listgridshowdraghandles).

---
