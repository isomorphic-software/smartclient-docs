# Page Documentation

[← Back to API Index](../reference.md)

---

## Class: Page

### Description
Provides information about the page you're loaded in. We define "page" here to be roughly equivalent to the browser window or frame the libraries have been loaded in.

---
## ClassAttr: Page.defaultUnsupportedBrowserURL

### Description
On a call to `Page.checkBrowserAndRedirect()`, if no explicit URL is passed in, and the browser is not supported by ISC, redirect to this URL.

### Groups

- files
- browserSupport

### See Also

- [Page.checkBrowserAndRedirect](#classmethod-pagecheckbrowserandredirect)

**Flags**: IRWA

---
## ClassAttr: Page.FIRE_ONCE

### Description
A declared value of the enum type [FireStyle](../reference_2.md#type-firestyle).

**Flags**: R

---
## ClassAttr: Page.protocolURLs

### Description
If a URL provided to various Page APIs begins with one of these Strings, it is treated as an absolute URL.

The default of protocols is:

```
     ["http://","https://","file://","mailto:", "app-resource:", "data:"]
 
```
.. and can be replaced via [Page.addClassProperties()](Class.md#classmethod-classaddclassproperties) or via setting the global variable isc\_protocolURLs before SmartClient loads.

### Groups

- files

### See Also

- [Page.getURL](#classmethod-pagegeturl)

**Flags**: IRW

---
## ClassAttr: Page.unsupportedBrowserAction

### Description
Action to take when [Page.checkBrowserAndRedirect](#classmethod-pagecheckbrowserandredirect) is called in a browser for which support is not guaranteed. Valid settings are:

*   `"continue"` Load the page without notifying the user of potential issues
*   `"confirm"` Notify the user via a standard confirm dialog that their browser is not supported. Provide options to continue anyway, or redirect to another page.
*   `"redirect"` Automatically redirect to the another URL

### Groups

- browserSupport

### See Also

- [Page.checkBrowserAndRedirect](#classmethod-pagecheckbrowserandredirect)
- [Page.defaultUnsupportedBrowserURL](#classattr-pagedefaultunsupportedbrowserurl)

**Deprecated**

**Flags**: IRA

---
## ClassAttr: Page.suppressBackspaceNavigation

### Description
By default most modern browsers will navigate back one page when the user hits the backspace key.

Setting this attribute to true will suppress this native behavior. Alternatively, developers can explicitly return `false` from the keyPress event (either via event handlers applied to specific widgets, or via [Page.registerKey](#classmethod-pageregisterkey) for example) to suppress the native navigation behavior.

**Flags**: IRWA

---
## ClassMethod: Page.setIsomorphicDir

### Description
Specify the root directory for Isomorphic-supplied files - the directory containing the `modules/` and `system/` subdirectories shipped as part of the SmartClient package.

Note that this property is commonly specified directly in the bootstrap HTML file by setting `window.isomorphicDir` before loading the SmartClient library files.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| URL | [String](#type-string) | true | — | New IsomorphicDir URL. |

### Groups

- files

---
## ClassMethod: Page.getIsomorphicDir

### Description
Return the root directory for Isomorphic-specific files.

### Returns

`[String](#type-string)` — IsomorphicDir URL.

### Groups

- files

---
## ClassMethod: Page.ignore

### Description
Clear an observation set up by [Page.observe](#classmethod-pageobserve).

This method is available as `isc.Page.ignore()` or just `isc.ignore()`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| observerID | [String](#type-string) | false | — | ID returned from [Page.observe](#classmethod-pageobserve) call we want to clear |

---
## ClassMethod: Page.isAddVersionToSkinCSS

### Description
Returns true if add version to skin CSS is currently turned on.

### Returns

`[Boolean](#type-boolean)` — true == add version to skin CSS is turned on

### Groups

- skins
- files

---
## ClassMethod: Page.setTitle

### Description
Set the title of the page, which is typically shown as part of the browser window title

---
## ClassMethod: Page.getAppFilesDir

### Description
Returns the directory for application-specific files (other than images).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| URL | [String](#type-string) | true | — | New app files URL. |

### Groups

- files
- images

---
## ClassMethod: Page.getSkinImgDir

### Description
Return the directory for a skin image.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| imgDir | [URL](../reference_2.md#type-url) | true | — | Partial URL (relative to Page.\_skinDir) where the image lives. If not supplied, will use "images/" |

### Returns

`[String](#type-string)` — URL for page-specific images.

### Groups

- files
- images

---
## ClassMethod: Page.setAppFilesDir

### Description
Specify the directory for miscellaneous app-specific files **other than** images, such as [HTML fragments](HTMLFlow.md#attr-htmlflowcontentsurl), [loadable views](ViewLoader.md#class-viewloader), XML or JSON flat data files, videos, etc.

This URL also becomes available via the prefix "\[APPFILES\]" for [RPCRequest.actionURL](RPCRequest.md#attr-rpcrequestactionurl).

Defaults to the value of [Page.getAppDir](#classmethod-pagegetappdir), that is, the current directory.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| URL | [String](#type-string) | true | — | New app files URL. |

### Groups

- files
- images

---
## ClassMethod: Page.getWidth

### Description
Get the width of the visible portion of the window, not including browser chrome or the scrollbar area.

See also [Page.getOrientation](#classmethod-pagegetorientation).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| wd | [Object](../reference.md#type-object) | true | — | the window object |

### Returns

`[number](#type-number)` — width of the page

### Groups

- sizing

---
## ClassMethod: Page.loadStyleSheet

### Description
Load a styleSheet for this application. The styleSheetURL parameter can use any special directories, eg:  
  `Page.loadStylesheet("[SKIN]/skin_styles.css")`  
or  
  `Page.loadStylesheet("[APP]/app_styles.css")`.

If you don't specify a special directory, the app directory will be assumed.

Note: If the document's ONLOAD handler has already fired, this will have no effect.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| styleSheetURL | [URL](../reference_2.md#type-url) | false | — | URL to the stylesheet. |

### Groups

- skins
- files
- images

---
## ClassMethod: Page.scrollTo

### Description
Scroll the window to a specified top and left coordinate.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [number](#type-number) | false | — | new left coordinate for window |
| top | [number](#type-number) | false | — | new top coordinate for window |

---
## ClassMethod: Page.unregisterKey

### Description
Clears an action registered to fire on a specific a keyPress event via the [Page.registerKey](#classmethod-pageregisterkey) method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| actionID | [KeyName](../reference.md#type-keyname) | false | — | Name of key to clear registry entries for. |
| target | [Object](../reference.md#type-object) | true | — | target specified when the action was registered for the key. |

### Groups

- KeyRegistry

### See Also

- [Page.registerKey](#classmethod-pageregisterkey)

---
## ClassMethod: Page.goBack

### Description
Go back in the browser's history.  
  
If the history is empty and the window.opener is set, we assume we're a child window and just close the window.

---
## ClassMethod: Page.getScrollWidth

### Description
Get the width of the window contents as they have been drawn. If the page scrolls, this may be larger than the [Page.getWidth](#classmethod-pagegetwidth).

### Returns

`[number](#type-number)` — width of the page as drawn

### Groups

- sizing

---
## ClassMethod: Page.isRTL

### Description
Return whether the page text direction is right to left. If you set "DIR=RTL" in the BODY tag of the page, then this method will return true. If you set "DIR=LTR" then this method will return false.

### Returns

`[Boolean](#type-boolean)` — true if Page text direction is RTL, false otherwise

### Groups

- textDirection
- appearance

---
## ClassMethod: Page.getOrientation

### Description
Is the current page wider than it is tall ("landscape" orientation) or the reverse ("portrait" orientation). Note that the [orientationChange page event](../reference_2.md#type-pageevent) will be fired whenever the page orientation changes.

This method is typically useful for apps developed for display on mobile devices, though it will also return a valid value when running against a desktop browser. See also [this discussion](../kb_topics/mobileDevelopment.md#kb-topic-mobile-application-development) on building applications for mobile devices

### Returns

`[PageOrientation](../reference.md#type-pageorientation)` — current page orientation

### Groups

- mobileDevelopment

---
## ClassMethod: Page.setAppImgDir

### Description
Specify the directory for app-specific images.

This becomes the default location where any SmartClient component will load images from unless the special "\[SKIN\]" prefix is used to indicate that an image is part of a skin.

Default is "\[APP\]images/"

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| URL | [String](#type-string) | true | — | New imgDir URL. |

### Groups

- files
- images

---
## ClassMethod: Page.moveTo

### Description
Move the window to a specified top and left in screen coordinates.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [number](#type-number) | false | — | new left coordinate for window |
| top | [number](#type-number) | false | — | new top coordinate for window |

---
## ClassMethod: Page.clearEvent

### Description
Clear event(s) under the given eventType.

To clear all events, omit the ID parameter. To clear a specific event, pass the ID that was returned by Page.setEvent().

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| eventType | [PageEvent](../reference_2.md#type-pageevent) | false | — | event type to clear |
| ID | [number](#type-number) | true | — | ID of the event to clear. If not specified, all events in eventType will be cleared. |

### Groups

- EventRegistry

### See Also

- [EventHandler](EventHandler.md#class-eventhandler)

---
## ClassMethod: Page.getSampleImgDir

### Description
Return the dir for Showcase-sample images which differ by skin.

### Returns

`[String](#type-string)` — the dir for Showcase-sample images in the current skin.

### Groups

- files

---
## ClassMethod: Page.waitFor

### Description
Wait for a method to fire on an object.

`waitFor` is similar [observation](Class.md#method-classobserve), but fires once only.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | any SmartClient object, eg, a ListGrid |
| methodName | [String](#type-string) | false | — | name of a method on that object |
| callback | [Function](#type-function) | false | — | Callback to fire when the observed method completes |
| timeout | [Number](#type-number) | true | — | Optional timeout period (in milliseconds). If you want a timeout, you must also provide a timeoutCallback |
| timeoutCallback | [Function](#type-function) | true | — | Callback to fire if the timeout period elapses before the observed method completes |

### Returns

`[boolean](../reference.md#type-boolean)` — whether observation succeeded. Observation may fail due to null object, non-existent method or similar bad parameters

---
## ClassMethod: Page.getURL

### Description
Return a full URL for a relative path that uses a special prefix such as "\[APPFILES\]" or "\[SKIN\]".

For images, use [Page.getImgURL](#classmethod-pagegetimgurl) instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fileName | [String](#type-string) | false | — | Local file name for the image. |

### Returns

`[String](#type-string)` — URL for the image.

### Groups

- files
- images

---
## ClassMethod: Page.getScreenHeight

### Description
Get the height of the user's screen, in pixels.

### Returns

`[number](#type-number)` — height of the user's screen

---
## ClassMethod: Page.getSampleThumbnailDir

### Description
Return the dir for skin-specific sample-thumbnails in the product Showcase.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| URL | [String](#type-string) | true | — | New URL for Showcase sample-thumbnails |

### Returns

`[String](#type-string)` — URL for root directory of sample-thumbnails.

### Groups

- files

---
## ClassMethod: Page.isLoaded

### Description
Has the page finished loading?

### Returns

`[Boolean](#type-boolean)` — true == page is done loading

---
## ClassMethod: Page.getImgURL

### Description
Return the full URL for app-specific or skin image.

To use a skin image, start the URL with "\[SKIN\]". Any other relative URL is assumed relative to the [appImgDir](#classmethod-pagegetappimgdir).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| src | [SCImgURL](../reference.md#type-scimgurl) | false | — | Local file name for the image. |
| imgDir | [String](#type-string) | true | — | User-specified image directory, local to |

### Returns

`[String](#type-string)` — URL for the image.

### Groups

- files
- images

---
## ClassMethod: Page.getIsomorphicToolsDir

### Description
Return the root directory for Isomorphic-supplied tools dir.

### Returns

`[String](#type-string)` — IsomorphicToolsDir URL.

### Groups

- files

---
## ClassMethod: Page.getDevicePixelRatio

### Description
Returns the current ratio of the resolution in physical pixels to the resolution in CSS pixels in the browser, known as the [device pixel ratio](https://developer.mozilla.org/en-US/docs/Web/API/Window/devicePixelRatio). The ratio reflects the combination of OS-level zoom, browser-level zoom, and device/OS defaults.

When this value isn't 1, some browser bugs manifest, so it can be useful to check it as an indicator that certain issues may be present and, in turn, whether workarounds fom them must run. However, note that on Safari it's not useful as the value is identically 1.

A specific application of this function is to check whether any zoom is present after a resize event so that the user can be informed that a page reload might be required for proper rendering.To do this, first store its value after the page is loaded, then in a resize handler check for the ratio transitioning away from 1:

```
isc.Page.setEvent("load", function () {
    isc.Page._ratio = isc.Page.getDevicePixelRatio();
});
isc.Page.setEvent("resize", function () {
    var ratio = isc.Page.getDevicePixelRatio();
    if (ratio != 1 && isc.Page._ratio == 1) {
        isc.notify("Browser content is now zoomed.  " + 
            "A page reload may be needed for proper display.");
    }
    isc.Page._ratio = ratio;
});
```

### See Also

- [browserZoom](../kb_topics/browserZoom.md#kb-topic-native-browser-zoom-support)

---
## ClassMethod: Page.getAppImgDir

### Description
Return the directory for app-specific images.

### Returns

`[String](#type-string)` — URL for page-specific images.

### Groups

- files
- images

---
## ClassMethod: Page.getSamplePhotoDir

### Description
Return the dir for skin-specific sample-photos in the product Showcase.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| URL | [String](#type-string) | true | — | New URL for Showcase sample-photos |

### Returns

`[String](#type-string)` — URL for root directory of sample-photos.

### Groups

- files

---
## ClassMethod: Page.registerKey

### Description
Fire some action when the Page receives a keyPress event from a certain key.  
Note that if a widget has keyboard focus, this action will fire only after any widget-level keyPress handlers have fired and bubbled the event up to the top of their ancestor chain.  
Multiple actions can be registered to fire on a single keyPress using this method, and can be associated with different `target` objects (which will then be available as a parameter when the action is fired).  
This differs from calling [Page.setEvent](#classmethod-pagesetevent) with the `"keyPress"` events registered via `setEvent()` will fire _before_ widget level handlers respond to the event, and will fire for every `keyPress` event, not just those triggered by some specific key or key-combination.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| key | [KeyIdentifier](#type-keyidentifier) | false | — | key name or identifier object. |
| action | [String](#type-string) | false | — | Action to fire when key is pressed. This can be a string of script to evaluate or a javascript function.  
This action will be passed 2 parameters: The name of the key pressed will be available as the first parameter or `key` keyword. The target passed into this method will be available as the second parameter or `target` keyword. |
| target | [Any](#type-any) | true | — | If specified this object will be made available to the action fired as a parameter. |

### Groups

- KeyRegistry

### See Also

- [Canvas.keyPress](Canvas.md#method-canvaskeypress)
- [Page.setEvent](#classmethod-pagesetevent)
- [Page.unregisterKey](#classmethod-pageunregisterkey)

---
## ClassMethod: Page.setAddVersionToSkinCSS

### Description
Setting this to true will cause [Page.loadStyleSheet](#classmethod-pageloadstylesheet) to append an "isc\_version" parameter to the end of the url when loading a stylesheet.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| addVersionToSkinCss | [Boolean](#type-boolean) | false | — | pass in true to turn on automatic adding of version parameter to css urls. |

### Groups

- skins
- files

---
## ClassMethod: Page.getSkinDir

### Description
Return the directory for media that's part of the skin

### Returns

`[String](#type-string)` — base URL for skin media

### Groups

- files
- images

---
## ClassMethod: Page.getHeight

### Description
Get the height of the visible portion of the window, not including browser chrome or the scrollbar area.

See also [Page.getOrientation](#classmethod-pagegetorientation).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| wd | [Object](../reference.md#type-object) | true | — | the window object |

### Returns

`[number](#type-number)` — height of the page

### Groups

- sizing

---
## ClassMethod: Page.updateViewport

### Description
This method only applies to browsers that support the special viewport meta tag, such as Mobile Safari running on the iPhone.

This method will dynamically change the viewport configuration, allowing you to set an initial size or scale level and enable / disable user-scaling. Typically this method will be called with a value for scale, width or height rather than passing in values for all three properties.

See Apple's Safari Web Content Guide on configuring the viewport for more information: [https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariWebContent/UsingtheViewport/UsingtheViewport.html](https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariWebContent/UsingtheViewport/UsingtheViewport.html)

_Note:_ Modifying the width/height or initial scale of the viewport has two user-visible effects:

*   HTML elements may reflow to fit the specified size (or the implied size calculated from the specified scale level and the native device size).
*   If the user has not scaled the application explicitly, and no other scaling or sizing attributes were specified via a viewport meta tag for this page, the application will zoom to specified scale level (or the scale level required to fit the specified viewport size to the device's screen).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| scale | [float](../reference.md#type-float) | true | — | Desired scale level where 1 indicates no scaling (each css pixel will be displayed using 1px on the physical device). Pass in null to avoid setting this property. |
| width | [Integer](../reference_2.md#type-integer) | true | — | Desired viewport width in pixels. This indicates how many pixels should fit within the device screen. Pass in null to avoid setting this property. |
| height | [Integer](../reference_2.md#type-integer) | true | — | Desired viewport height in pixels. This indicates how many pixels should fit within the device screen. Pass in null to avoid setting this property. |
| scalable | [Boolean](#type-boolean) | true | — | Should the user be able to scale the application (using pinch gestures, double tapping, rotating the device, etc.)? Pass in null to avoid setting this property. |

### Groups

- mobileDevelopment

### See Also

- [mobileDevelopment](../kb_topics/mobileDevelopment.md#kb-topic-mobile-application-development)

---
## ClassMethod: Page.getToolsImgDir

### Description
Return the images directory used by Isomorphic-supplied tools.

### Returns

`[String](#type-string)` — ToolsImgDir URL.

### Groups

- files

---
## ClassMethod: Page.getScrollTop

### Description
Get the amount that the browser window has been scrolled vertically.

### Returns

`[number](#type-number)` — vertical scroll amount

### Groups

- sizing

---
## ClassMethod: Page.getScrollHeight

### Description
Get the height of the window contents as they have been drawn. If the page scrolls, this may be larger than the [Page.getHeight](#classmethod-pagegetheight).

### Returns

`[number](#type-number)` — height of the page as drawn

### Groups

- sizing

---
## ClassMethod: Page.setEvent

### Description
Register to be called whenever a given type of event occurs, at the page level.

This includes events that also occur on widgets (like "click") and events that only occur at the page level ("resize" and "load").

For events that also occur on widgets, page level event registrations will fire BEFORE the event handlers on Canvases. If your action returns `false`, this will prevent the event from getting to the intended Canvas.

Capturing events on widgets can be done by setting one of the event methods available on Canvas (and hence available to all widget classes). See [widgetEvents](../reference.md#kb-topic-widgetevents).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| eventType | [PageEvent](../reference_2.md#type-pageevent) | false | — | event type to register for ("mouseDown", "load", etc) |
| action | [String](#type-string) | false | — | string to be eval'd when event fires (function) function to be executed when event fires (object) an object to call on which a method named "page" + eventType will be called |
| fireStyle | [FireStyle](../reference_2.md#type-firestyle) | true | — | Flag to set automatic removal of the event after it fires one or more times |
| functionName | [String](#type-string) | true | — | optional - if an object was passed in as the second parameter, this is a name of a method to call on that object. |

### Returns

`[number](#type-number)` — ID number of this event, may be used to remove the event later via a call to `Page.clearEvent()`

### Groups

- EventRegistry

### See Also

- [EventHandler](EventHandler.md#class-eventhandler)
- [EventHandler.getX](EventHandler.md#classmethod-eventhandlergetx)
- [EventHandler.getY](EventHandler.md#classmethod-eventhandlergety)

---
## ClassMethod: Page.observe

### Description
Method to set up a static [observation](Class.md#method-classobserve) on some target object. This allows developers to perform some action every time a particular method is invoked on a target object.

This method returns a unique observation identifier string. To cancel the observation, pass this identifier to [Page.ignore](#classmethod-pageignore).

If multiple observations are set up for the same target object and method, the notification actions will be fired in the order in which they were registered.

This method is available as `isc.Page.observe()` or just `isc.observe()`

Note _\[potential memory leak\]_: If the target object is a simple JavaScript object (not an instance of a SmartClient class), developers should always call [Page.ignore](#classmethod-pageignore) to stop observing the object if an observation is no longer necessary.  
This ensures that if the object is subsequently allowed to go out of scope by application code, the Page level observation system will not retain a reference to it (so the browser can reclaim the allocated memory).  
While cleaning up observations that are no longer required is always good practice, this memory leak concern is not an issue if the target object is an instance of a SmartClient class. In that case the observation is automatically released when the target is [destroyed](Class.md#method-classdestroy).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| object | [Object](../reference.md#type-object) | false | — | Object to observe. This may be any JavaScript object with the specified target method, including native arrays, and instances of SmartClient classes such as [Canvas](Canvas.md#class-canvas). |
| methodName | [String](#type-string) | false | — | Name of the method to observe. Every time this method is invoked on the target object the specified action will fire (after the default implementation completes). |
| action | [Function](#type-function)|[String](#type-string) | false | — | Action to take when the observed method is invoked.  
If `action` is a string to execute, certain keywords are available for context:

*   `observed` is the target object being observed (on which the method was invoked).
*   `returnVal` is the return value from the observed method (if there is one)
*   For functions defined with explicit parameters, these will also be available as keywords within the action string

If `action` is a function, the arguments for the original method will also be passed to this action function as arguments. If developers need to access the target object being observed from the action function they may use native javascript techniques such as [javascript closure](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) to do so. The return value from the observed method is not available to the action function. |

### Returns

`[String](#type-string)` — Identifier for the observation. Pass this to [Page.ignore](#classmethod-pageignore) to stop observing the method in question.

---
## ClassMethod: Page.waitForMultiple

### Description
Wait for methods to fire on multiple objects.

`waitForMultiple` is similar to [Page.waitFor](#classmethod-pagewaitfor), except that it does not fire its callback until all of the provided methods have fired.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| objects | [Array](#type-array) | false | — | an array of objects, each of which consists of two properties:  
"object": any SmartClient object, eg a ListGrid  
"method": name of a method on that object |
| callback | [Function](#type-function) | false | — | Callback to fire when all observed methods have fired |
| timeout | [Number](#type-number) | true | — | Optional timeout period (in milliseconds). If you want a timeout, you must also provide a timeoutCallback |
| timeoutCallback | [Function](#type-function) | true | — | Callback to fire if the timeout period elapses before all observed methods have fired |

### Returns

`[boolean](../reference.md#type-boolean)` — whether observation succeeded. Observation may fail due to null objects, non-existent methods or similar bad parameters

---
## ClassMethod: Page.checkBrowserAndRedirect

### Description
Check whether the browser is supported by the Isomorphic SmartClient system. Behavior depends upon the value of [Page.unsupportedBrowserAction](#classattr-pageunsupportedbrowseraction):

*   `"continue"` Load the page without notifying the user of potential issues
*   `"confirm"` Notify the user via a standard confirm dialog that their browser is not supported. Provide options to continue anyway, or redirect to another page. Text of the confirm dialog is retrieved by calling [Page.getUnsupportedBrowserPromptString](#classmethod-pagegetunsupportedbrowserpromptstring).
*   `"redirect"` Automatically redirect to the another URL

If redirecting to another page is necessary, and no explicit URL is provided we will use [Page.defaultUnsupportedBrowserURL](#classattr-pagedefaultunsupportedbrowserurl).

This method is commonly called as part of the [skinning](../kb_topics/skinning.md#kb-topic-skinning--theming) logic after page load.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| URL | [String](#type-string) | true | — | URL of redirect page. May include Isomorphic special directories such as \[SKIN\]. |

### Groups

- browserSupport

### See Also

- [Page.unsupportedBrowserAction](#classattr-pageunsupportedbrowseraction)
- [Page.getUnsupportedBrowserPromptString](#classmethod-pagegetunsupportedbrowserpromptstring)
- [Page.defaultUnsupportedBrowserURL](#classattr-pagedefaultunsupportedbrowserurl)

**Deprecated**

---
## ClassMethod: Page.resizeTo

### Description
Resize the outer portion of the window to a specific width and height.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [number](#type-number) | false | — | new width for the window |
| height | [number](#type-number) | false | — | new height for the window |

### Groups

- sizing

---
## ClassMethod: Page.setSkinDir

### Description
Specify the URL for media that's part of the skin

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| URL | [String](#type-string) | true | — | New skinDir URL |

### Groups

- skins
- files
- images

---
## ClassMethod: Page.getAppDir

### Description
Returns the base URL of the application, which is the page URL minus the last non-directory path component. For example, if the page is loaded from `http://foo.com/bar/zoo.jsp`, appDir will be `http://foo.com/bar/`.

If other page-wide URLs such as [Page.setIsomorphicDir](#classmethod-pagesetisomorphicdir) are specified as relative paths, they are considered relative to this URL.

### Returns

`[String](#type-string)` — URL for page-specific files.

### Groups

- files

---
## ClassMethod: Page.setSampleThumbnailDir

### Description
Specify the dir for skin-specific sample-thumbnails in the product Showcase.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| URL | [String](#type-string) | true | — | New URL for Showcase sample thumbnails |

### Groups

- files

---
## ClassMethod: Page.getScrollLeft

### Description
Get the amount that the browser window has been scrolled horizontally.

### Returns

`[number](#type-number)` — horizontal scroll amount

### Groups

- sizing

---
## ClassMethod: Page.getUnsupportedBrowserPromptString

### Description
Returns the text for the prompt shown to user from [Page.checkBrowserAndRedirect](#classmethod-pagecheckbrowserandredirect) if they are accessing this page in an unsupported browser and [Page.unsupportedBrowserAction](#classattr-pageunsupportedbrowseraction) is set to `"confirm"`. May be overridden to return a different message.

### Returns

`[String](#type-string)` — Unsupported browser message.

### Groups

- i18nMessages
- browserSupport

### See Also

- [Page.checkBrowserAndRedirect](#classmethod-pagecheckbrowserandredirect)

---
## ClassMethod: Page.setSamplePhotoDir

### Description
Specify the dir for skin-specific sample-photos in the product Showcase.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| URL | [String](#type-string) | true | — | New URL for Showcase sample-photos |

### Groups

- files

---
## ClassMethod: Page.getScreenWidth

### Description
Get the width of the user's screen, in pixels.

### Returns

`[number](#type-number)` — width of the user's screen

---
## ClassMethod: Page.setIsomorphicToolsDir

### Description
Specify the root directory for Isomorphic-supplied tools. Typicall tools/ under webRoot.

Note that this property is commonly specified directly in the bootstrap HTML file by setting `window.isomorphicToolsDir` before loading the SmartClient library files. If unset, it defaults to $isomorphicDir/../tools/

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| URL | [String](#type-string) | true | — | New IsomorphicToolsDir URL. |

### Groups

- files

---
## ClassMethod: Page.setSampleImgDir

### Description
Specify the dir for Showcase-sample images which differ by skin.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| URL | [String](#type-string) | true | — | New URL for Showcase-sample images in the current skin |

### Groups

- files

---
