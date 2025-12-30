# Browser Documentation

[← Back to API Index](../reference.md)

---

## Class: Browser

### Description
The `Browser` class contains various class attributes that indicate basic properties of the browser and whether certain features are enabled.

---
## ClassAttr: Browser.isSupported

### Description
Whether SmartClient supports the current browser.

Note that this flag will only be available on browsers that at least support basic JavaScript.

**Flags**: R

---
## ClassAttr: Browser.isTouch

### Description
Is the application running on a touch device (e.g. iPhone, iPad, Android device, etc.)?

SmartClient's auto-detected value for `isTouch` can be overridden via [Browser.setIsTouch](#classmethod-browsersetistouch).

**Flags**: RW

---
## ClassAttr: Browser.isTablet

### Description
Is the application running on a tablet device (e.g. iPad, Nexus 7)?

SmartClient can correctly determine whether the device is a tablet in most cases. On any uncommon device for which this variable is incorrect, you can define the `isc_isTablet` global with the correct value, and SmartClient will use `isc_isTablet` for `Browser.isTablet` instead of its own detection logic. Alternatively, you can use [Browser.setIsTablet](#classmethod-browsersetistablet) to change this global variable before any components are created.

The value of this variable is only meaningful on touch devices.

**Flags**: RW

---
## ClassAttr: Browser.supportsDualInput

### Description
Does the browser support both mouse and touch input?

**Flags**: RW

---
## ClassAttr: Browser.isDesktop

### Description
Is the application running in a desktop browser? This is true if [Browser.isTablet](#classattr-browseristablet) and [Browser.isHandset](#classattr-browserishandset) are both `false`.

**Flags**: RW

---
## ClassAttr: Browser.useCSS3

### Description
Whether the current browser supports CSS3 and whether SmartClient is configured to use CSS3 features (via the setting of window.isc\_css3Mode).

If isc\_css3Mode is "on" then useCSS3 is set to true. If isc\_css3Mode is set to "supported", "partialSupport", or is unset, then useCSS3 is set to true only if the browser is a WebKit-based browser, Firefox, IE 9 in standards mode, or IE 10+. If isc\_css3Mode is set to "off" then useCSS3 is set to false.

**Flags**: R

---
## ClassAttr: Browser.useHighPerformanceGridTimings

### Description
Controls how agressive components based on the [GridRenderer](GridRenderer.md#class-gridrenderer) are with respect to redraws and data fetches. Modern browsers can generally handle much more frequent redraws and most server configurations can handle fetching more data more frequently in order to reduce the lag the end user perceives when scrolling through databound grids. Starting with SmartClient 11.0/SmartGWT 6.0, this more aggressive redraw and fetch behavior us the default, but can be reverted to the old behavior if desired - see below.

This flag controls the defaults for several other properties (value on left is default for high performance mode, value on right is default when this mode is disabled.

*   [ListGrid.dataFetchDelay](ListGrid_1.md#attr-listgriddatafetchdelay) 1 -> 300
*   [ListGrid.drawAheadRatio](ListGrid_1.md#attr-listgriddrawaheadratio) 2.0 -> 1.3
*   [ListGrid.quickDrawAheadRatio](ListGrid_1.md#attr-listgridquickdrawaheadratio) 2.0 -> 1.3
*   [ListGrid.scrollRedrawDelay](ListGrid_1.md#attr-listgridscrollredrawdelay) 0 -> 75
*   [ListGrid.scrollWheelRedrawDelay](ListGrid_1.md#attr-listgridscrollwheelredrawdelay) 0 -> 250
*   [ListGrid.touchScrollRedrawDelay](ListGrid_1.md#attr-listgridtouchscrollredrawdelay) 0 -> 300

Note: since [TreeGrid](TreeGrid.md#class-treegrid) is a subclass of [ListGrid](ListGrid_1.md#class-listgrid), the above settings also apply to [TreeGrid](TreeGrid.md#class-treegrid)s.

*   [GridRenderer.drawAheadRatio](GridRenderer.md#attr-gridrendererdrawaheadratio) 2.0 -> 1.3
*   [GridRenderer.quickDrawAheadRatio](GridRenderer.md#attr-gridrendererquickdrawaheadratio) 2.0 -> 1.3
*   [GridRenderer.scrollRedrawDelay](GridRenderer.md#attr-gridrendererscrollredrawdelay) 0 -> 75
*   [GridRenderer.touchScrollRedrawDelay](GridRenderer.md#attr-gridrenderertouchscrollredrawdelay) 0 -> 300

By default, for all browsers except Android-based Chrome, this flag is set to true, but can be explicitly disabled by setting `isc_useHighPerformanceGridTimings=false` in a script block before loading SmartClient modules. Turning off high performance timings effectively enables the original SmartClient/SmartGWT behavior prior to the SmartClient 11.0/SmartGWT 6.0 release.

**Flags**: I

---
## ClassAttr: Browser.isHandset

### Description
Is the application running on a handset-sized device, with a typical screen width of around 3-4 inches?

This typically implies that the application will be working with only 300-400 pixels.

**Flags**: RW

---
## ClassMethod: Browser.setIsTablet

### Description
Setter for [Browser.isTablet](#classattr-browseristablet) to allow this global variable to be changed at runtime. This advanced method is provided to override SmartClient's detection of devices, since the framework can only detect devices that existed at the time the platform was released. Any changes to [Browser.isDesktop](#classattr-browserisdesktop), [Browser.isHandset](#classattr-browserishandset), or [Browser.isTablet](#classattr-browseristablet) must be made before any component is created; **it is an application error** to attempt to change `isDesktop`, `isHandset`, or `isTablet` after components have been created.

Note that setting `Browser.isTablet` might affect the values of [Browser.isDesktop](#classattr-browserisdesktop) and [Browser.isHandset](#classattr-browserishandset).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| isTablet | [boolean](../reference.md#type-boolean) | false | — | new setting for `Browser.isTablet`. |

**Flags**: A

---
## ClassMethod: Browser.setIsTouch

### Description
Setter for [Browser.isTouch](#classattr-browseristouch) to allow this global variable to be changed at runtime. This advanced method is provided to override SmartClient's auto-detection logic, since the framework can only detect touch devices that existed at the time the platform was released. Any change to [Browser.isTouch](#classattr-browseristouch) must be made before any component is created; **it is an application error** to attempt to change `isTouch` after components have been created.

Note that setting `Browser.isTouch` might affect the values of [Browser.isDesktop](#classattr-browserisdesktop), [Browser.isTablet](#classattr-browseristablet), and/or [Browser.isHandset](#classattr-browserishandset).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| isTouch | [boolean](../reference.md#type-boolean) | false | — | new setting for `Browser.isTablet`. |

**Flags**: A

---
## ClassMethod: Browser.setIsHandset

### Description
Setter for [Browser.isHandset](#classattr-browserishandset) to allow this global variable to be changed at runtime. This advanced method is provided to override SmartClient's detection of devices, since the framework can only detect devices that existed at the time the platform was released. Any changes to [Browser.isDesktop](#classattr-browserisdesktop), [Browser.isHandset](#classattr-browserishandset), or [Browser.isTablet](#classattr-browseristablet) must be made before any component is created; **it is an application error** to attempt to change `isDesktop`, `isHandset`, or `isTablet` after components have been created.

Note that setting `Browser.isHandset` might affect the values of [Browser.isDesktop](#classattr-browserisdesktop) and [Browser.isTablet](#classattr-browseristablet).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| isHandset | [boolean](../reference.md#type-boolean) | false | — | new setting for `Browser.isHandset`. |

**Flags**: A

---
## ClassMethod: Browser.setIsDesktop

### Description
Setter for [Browser.isDesktop](#classattr-browserisdesktop) to allow this global variable to be changed at runtime. This advanced method is provided to override SmartClient's detection of devices, since the framework can only detect devices that existed at the time the platform was released. Any changes to [Browser.isDesktop](#classattr-browserisdesktop), [Browser.isHandset](#classattr-browserishandset), or [Browser.isTablet](#classattr-browseristablet) must be made before any component is created; **it is an application error** to attempt to change `isDesktop`, `isHandset`, or `isTablet` after components have been created.

Note that setting `Browser.isDesktop` might affect the values of [Browser.isHandset](#classattr-browserishandset) and [Browser.isTablet](#classattr-browseristablet).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| isDesktop | [boolean](../reference.md#type-boolean) | false | — | new setting for `Browser.isDesktop`. |

**Flags**: A

---
