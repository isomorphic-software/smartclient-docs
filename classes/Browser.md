# Browser Documentation

[← Back to API Index](../reference.md)

---

## Class: Browser

### Description
The `Browser` class contains various class attributes that indicate basic properties of the browser and whether certain features are enabled.

These flags represent a "best effort" at browser detection based on the user agent string and other indicators. Browser detection is inherently imperfect - browsers may spoof their user agent, new browser versions may change behavior, and unusual browser configurations may not be detected correctly. These properties should not be considered a fully supported API for all edge cases - applications with unusual browser compatibility requirements may need to implement their own detection logic.

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
## ClassAttr: Browser.allowsSpeechRecognition

### Description
Whether this browser allows speech recognition sessions to be started using its SpeechRecognition implementation. Some browsers expose the API but prevent sessions from starting (for example, by blocking access to the vendor-operated speech-to-text service used by the implementation), typically surfacing as an immediate service or "network" error.

This flag is set on the first attempt to start speech recognition.

**Flags**: RA

---
## ClassAttr: Browser.supportsSpeechRecognition

### Description
Whether this browser exposes a SpeechRecognition implementation (API is present). This indicates that browser-provided speech-to-text \*may\* be available for features such as [VoiceAssist](VoiceAssist.md#class-voiceassist), but does not guarantee that recognition sessions can be started. See [Browser.allowsSpeechRecognition](#classattr-browserallowsspeechrecognition) for runtime viability.

**Flags**: RA

---
## ClassAttr: Browser.isGraalJS

### Description
True when running in a GraalJS environment (either JSR-223 ScriptEngine or Polyglot Context API). GraalJS provides full Java interop, allowing JavaScript code to instantiate Java classes and call Java methods directly via `Java.type()`.

To distinguish between JSR-223 and Polyglot modes, check [Browser.isPolyglot](#classattr-browserispolyglot). When `isGraalJS` is true, [Browser.isServerJS](#classattr-browserisserverjs) is also true.

See [serverScript](../kb_topics/serverScript.md#kb-topic-server-scripting) for documentation on using JavaScript in DataSource server scripts.

**Flags**: R

---
## ClassAttr: Browser.isDesktop

### Description
Is the application running in a desktop browser? This is true if [Browser.isTablet](#classattr-browseristablet) and [Browser.isHandset](#classattr-browserishandset) are both `false`.

**Flags**: RW

---
## ClassAttr: Browser.allowsNewFunction

### Description
Whether `new Function()` is allowed. This is true by default, but if the page has a CSP (Content Security Policy) header with a `script-src` directive that omits `'unsafe-eval'`, `new Function()` throws an EvalError.

CSP's `'unsafe-eval'` controls all string-to-code evaluation methods identically, so when this flag is false, `eval()`, `setTimeout(string)`, and `setInterval(string)` are also blocked.

**Flags**: RA

---
## ClassAttr: Browser.useCSS3

### Description
Whether the current browser supports CSS3 and whether SmartClient is configured to use CSS3 features (via the setting of window.isc\_css3Mode).

If isc\_css3Mode is "on" then useCSS3 is set to true. If isc\_css3Mode is set to "supported", "partialSupport", or is unset, then useCSS3 is set to true only if the browser is a WebKit-based browser, Firefox, IE 9 in standards mode, or IE 10+. If isc\_css3Mode is set to "off" then useCSS3 is set to false.

**Flags**: R

---
## ClassAttr: Browser.isIE

### Description
Are we in Internet Explorer?

**Flags**: R

---
## ClassAttr: Browser.isOpenFin

### Description
Are we in an [OpenFin](https://developers.openfin.co/of-docs/docs) environment? See class [OpenFin](../reference.md#class-openfin) for ways to call OpenFin methods from within SmartClient.

**Flags**: R

---
## ClassAttr: Browser.isNode

### Description
True when running in a Node.js environment. Node.js mode is used for standalone server-side processing such as batch operations and internal tooling (for example, Isomorphic uses Node.js to generate [TypeScript definitions](../kb_topics/typeScriptSupport.md#kb-topic-typescript-support) from SmartClient's JSDoc metadata).

When `isNode` is true, [Browser.isServerJS](#classattr-browserisserverjs) is also true.

**Flags**: R

---
## ClassAttr: Browser.isMultiWindow

### Description
Are the [MultiWindow](MultiWindow.md#class-multiwindow) APIs supported and cross-window optimizations enabled? By default this is true in the [main window](MultiWindow.md#classmethod-multiwindowismainwindow) if [OpenFin](#classattr-browserisopenfin) is loaded, false otherwise. In [child windows](MultiWindow.md#classmethod-multiwindowopen), this property is read-only, and assumes the value from the main window.

**Note:** [MultiWindow](MultiWindow.md#class-multiwindow) is currently an experimental feature and not supported except by special arrangement

**Flags**: RW

---
## ClassAttr: Browser.micPermission

### Description
The browser's current permission state for microphone access for the current site (origin). Possible values are "granted", "denied", or "prompt", consistent with the Permissions API.

"prompt" indicates that the user has not yet made a decision for this site and that the browser will request permission when microphone access is first attempted, typically in response to a user interaction.

Note that not all browsers support querying microphone permission state in advance; in such cases this value may remain null until an access attempt is made.

**Flags**: RA

---
## ClassAttr: Browser.hasNativeDrag

### Description
Does this browser support native HTML5 drag and drop? This is false on touch devices and on IE/Edge Legacy due to limitations in their native drag implementations.

**Flags**: R

---
## ClassAttr: Browser.version

### Description
Browser major version number (integer: 4, 5, etc).

**Flags**: R

---
## ClassAttr: Browser.supportsDualInput

### Description
Does the browser support both mouse and touch input?

**Flags**: RW

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
## ClassAttr: Browser.micAvailable

### Description
Whether at least one audio input device (microphone) is available to the browser. This reflects device presence only and does not imply that the site has [permission](#classattr-browsermicpermission) to access the microphone. In some browsers, microphone enumeration may be limited or partially obscured until permission is granted.

**Flags**: RA

---
## ClassAttr: Browser.isPolyglot

### Description
True when running in GraalJS via the Polyglot Context API (as opposed to JSR-223 ScriptEngine). The Polyglot API is typically used in standalone Java applications that embed SmartClient JavaScript processing, while JSR-223 is used for declarative server scripts in .ds.xml files.

When `isPolyglot` is true, [Browser.isGraalJS](#classattr-browserisgraaljs) and [Browser.isServerJS](#classattr-browserisserverjs) are also true.

See [graalPolyglotDMI](../kb_topics/graalPolyglotDMI.md#kb-topic-graaljs-polyglot-api-for-dmi) for documentation on using the Polyglot API from DMI.

**Flags**: R

---
## ClassAttr: Browser.isServerJS

### Description
True in any server-side JavaScript environment (Node.js or GraalJS). This is a unified flag for code that needs to behave differently on server vs browser without caring which specific server runtime is in use.

Use this flag when:

*   Skipping UI operations that aren't supported server-side
*   Using alternative logging (server-side doesn't have browser console)
*   Bypassing browser-specific APIs (DOM, timers, events)

To detect the specific server runtime, check [Browser.isNode](#classattr-browserisnode), [Browser.isGraalJS](#classattr-browserisgraaljs), or [Browser.isPolyglot](#classattr-browserispolyglot).

**Flags**: R

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
## ClassMethod: Browser.setIsMultiWindow

### Description
Sets a non-default value for [Browser.isMultiWindow](#classattr-browserismultiwindow), such as enabling it even if [OpenFin](#classattr-browserisopenfin) isn't present.

Note that this method may only be called from the [main window](MultiWindow.md#classmethod-multiwindowismainwindow), and only once.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| isMultiWindow | [boolean](../reference.md#type-boolean) | false | — | new setting for `Browser.isMultiWindow`. |

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
## ClassMethod: Browser.hasSessionStorage

### Description
Returns whether sessionStorage is accessible in the current environment. This method performs a one-time check and caches the result. In CSP sandbox environments without 'allow-same-origin', sessionStorage access throws a SecurityError.

### Returns

`[boolean](../reference.md#type-boolean)` — true if sessionStorage is accessible, false otherwise

---
## ClassMethod: Browser.hasLocalStorage

### Description
Returns whether localStorage is accessible in the current environment. This method performs a one-time check and caches the result. In CSP sandbox environments without 'allow-same-origin', localStorage access throws a SecurityError.

### Returns

`[boolean](../reference.md#type-boolean)` — true if localStorage is accessible, false otherwise

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
