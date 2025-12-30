# Mobile Application Development

[← Back to API Index](../reference.md)

---

## KB Topic: Mobile Application Development

### Description
SmartClient is designed to automatically adapt to smaller screen sizes and the lower accuracy of touch-based interfaces.

In general, a SmartClient application written with complete ignorance of mobile development will still be highly usable on tablet or handset-sized touch devices. This topic explains all the automatic behaviors that make this possible, and the few areas developers need to consider in order to optimize the mobile experience, the most important being:

*   read about potential issues created by the automatically shown and hidden browser toolbars in Safari on iOS7+, discussed under "minimal-ui" below. SmartClient automatically handles this, but most applications will want to create a non-interactive banner to fill the blank screen area that is rendered unusable by iOS' behavior
*   read about "Automatic touch scrolling" below - if your application does not already have alternative UIs for performing drag operations (as is required anyway for [accessibility reasons](accessibility.md#kb-topic-accessibility--section-508-compliance)), this section discusses options for controlling drag scrolling vs dragging of data
*   review your application for the rare screen that has a fixed, very wide width and doesn't allow scrolling. Such screens would already be unusable for narrow desktop browsers but are more of a problem for fixed-size mobile screens. The section "Exceptionally wide screens" below explains strategies for dealing with this.

#### Supported Browsers

*   Safari on iOS devices (iPad, iPhone, iPod Touch)
*   Android's default (WebKit-based) browser **\***
*   Windows Phone default browser, latest release only **\*\***
*   Blackberry 10+ default (WekKit-based) browser **\*\***

**\***: Android issues that occur _exclusively_ on rare devices (under a certain percent of market share) will not normally be covered by a Support plan. This is a necessity because highly customized versions of Android are used for a variety of niche devices (even microsatellites)  
**\*\***: These browsers generally work and bug reports are accepted, but they do not yet fall under the normal Enterprise+ Support guarantee of fixing every confirmed bug

If you would like to check whether a specific device falls under normal Support, or would like a quote for a Support plan that would include a specific device or platform, [contact Isomorphic here](http://smartclient.com/company/contact.jsp).

#### Adaptive Components

Many SmartClient components automatically change their behavior and/or appearance when used with touch devices in general, or tablets and handsets specifically. There are too many adaptations to comprehensively list, but some of the more obvious behaviors are listed below:

*   [SelectItem](../classes/SelectItem.md#class-selectitem) and [ComboBoxItem](../classes/ComboBoxItem.md#class-comboboxitem) controls automatically fill the entire screen or a major portion of the screen when activated, and add a control to dismiss the full-screen interface. See [ComboBoxItem.pickListPlacement](../classes/ComboBoxItem.md#attr-comboboxitempicklistplacement) for details
*   [Menu](../classes/Menu.md#class-menu) components likewise fill the entire screen or a major portion, and offer submenu navigation via a slide-in animation and back button instead of displaying the origin menu and submenu simultaneously
*   [Calendar](../classes/Calendar.md#attr-calendarminimalui) eliminates the tabs normally used to switch between Day, Week and Month view, instead using device pivot to switch between Day and Week views and offering a compact link to Month view
*   Windows and Dialogs fill the screen by default and remove rounded edges to save space
*   many controls implement an expanded hit area for clicks or drags so that finger touches that are technically outside of the drawn area of the control still activate the control. This accomodates the imprecision of finger touches as compared to mouse clicks, while still showing the same compact appearance as is used for desktop interfaces. This includes the [Slider](../classes/Slider.md#class-slider) thumb, [Window.headerControls](../classes/Window.md#attr-windowheadercontrols), [edge-based resizing](../classes/Canvas.md#attr-canvasresizefrom), and many other controls.
*   [SpinnerItem](../classes/SpinnerItem.md#class-spinneritem) switches to side-by-side +/- controls instead of the very small, vertically stacked +/- control typical of desktop interfaces
*   [AdaptiveMenu](../classes/AdaptiveMenu.md#class-adaptivemenu) can either display menu items inline, or in a drop-down, or mix the two modes according to available space.

In addition to automatic behavior, SmartClient offers Adaptive Layout whereby a [Layout](../classes/Layout.md#class-layout) member may be _designed_ to render itself at multiple possible sizes, in order to fit into the amount of space available in the Layout. Unlike simply indicating a flexible size on a member, setting an adaptive width or height indicates that the member has two (or more) different _ways_ of rendering itself with different _discrete_ sizes, but does not have the ability to use every additional available pixel.

For more guidance, see the documentation under [Canvas.canAdaptWidth](../classes/Canvas.md#attr-canvascanadaptwidth) and the *Inlined Menu Mobile* and *Adaptive Menu* samples.

#### Finger / touch event handling

Mobile and touch devices support "touch events" that correspond to finger actions on the screen. By default, SmartClient simply sends touch events to UI components as normal mouse events. Specifically:

*   a finger tap gesture will trigger mouseDown, mouseUp and click events
*   a touch-and-slide interaction will trigger drag and drop, firing the normal SmartClient sequence of dragStart, dragMove, and dragStop
*   a touch-and-hold interaction will trigger a contextMenu event, and will trigger a hover if no contextMenu is shown

This means that most applications that are written with mouse interaction in mind will function with a touch-based UI without special efforts. Some interfaces which rely heavily on mouse hovers may want to display instructions to explicitly tell the user that they have to touch a given element to see more information.

#### Automatic touch scrolling

Components that normally show scrollbars on desktop browsers will, by default, hide scrollbars and allow scrolling via finger dragging instead.

If you are using drag and drop features such as [ListGrid.canReorderRecords](../classes/ListGrid_1.md#attr-listgridcanreorderrecords), this obviously conflicts with using finger drags for scrolling. There are two options:

1.  Leave touch scrolling active for the grid, but provide additional controls, such as buttons, that enable users to perform the drag operation in a different way. Optionally display scrollbars _in addition to_ leaving touch scrolling active by setting [Canvas.alwaysShowScrollbars](../classes/Canvas.md#attr-canvasalwaysshowscrollbars) to `true`.
2.  Set [useTouchScrolling](../classes/Canvas.md#attr-canvasusetouchscrolling) to `false` on the component. Scrollbars will be shown, and finger drags will no longer cause scrolling, so that finger drags can now be used for the drag and drop operation configured on the component

Option #1 above is generally preferred, since it is also considered an [accessibility](accessibility.md#kb-topic-accessibility--section-508-compliance) violation if drag and drop is the sole way to trigger an operation (keyboard-only users cannot use drag and drop), and also because scrollbars are not usually found in touch interfaces.

If your application is not required to be keyboard accessible, and you prefer to show scrollbars and use finger drags for normal drag operations, you can use [Canvas.disableTouchScrollingForDrag](../classes/Canvas.md#attr-canvasdisabletouchscrollingfordrag) to make this choice system-wide or on a per-component-type basis.

#### Exceptionally wide screens / forms

If you have designed a screen for desktop use and it is too wide to fit on a handset or tablet-sized screen, there are several possible strategies:

*   **use [SplitPane](../classes/SplitPane.md#class-splitpane)**: any time you have two or more panes where a choice in one pane decides what is displayed in the other. See the "SplitPane" section further down for details
*   **rely on horizontal scrolling**: if you have something like a [DynamicForm](../classes/DynamicForm.md#class-dynamicform) that has 3 columns of input fields, as long as the form itself or some parent has [overflow:"auto"](../classes/Canvas.md#attr-canvasoverflow) set, horizontal touch scrolling will be available to reach fields that initially render offscreen. Most of the time, there is already an `overflow:"auto"` parent component as a result of default framework behaviors or application settings that also make sense for desktop mode, so nothing needs to be done.
    
    However, consider whether scrolling is already in use for other purposes: if you have a grid plus an adjacent component to the right, if the adjacent component is entirely offscreen, attempting touch scrollng on the grid will just scroll the grid as such and won't reveal the adjacent component. In this kind of situation, you can:
    
    *   _use [SplitPane](../classes/SplitPane.md#class-splitpane)_ as described above, a grid with something adjacent is frequently a good candidate for conversion to `SplitPane`
    *   _make the scrolling component smaller or flexible size_. Whether it's a grid or other scrollable component on the left, this situation usually arises because an inappropriately large fixed size has been set, instead of a [flexible size](../classes/Canvas.md#attr-canvaswidth).
    *   _leave some blank space_ above or below the grid - this gives the user somewhere to use touch scrolling to move both the grid and adjacent component
    *   _force scrollbars to appear_ by setting [useTouchScrolling](../classes/Canvas.md#attr-canvasusetouchscrolling) to false. This is another way to give the user a place they can touch in order to scroll the both the grid and adjacent component together
*   **use [FlowLayout](../reference.md#class-flowlayout)**: a `FlowLayout` can automatically take two side-by-side elements and switch them to vertical stacking when the screen is narrow

#### SplitPane

The [SplitPane](../classes/SplitPane.md#class-splitpane) component implements the common pattern of rendering two or three panes simultaneously on desktop machines and on tablets in landscape orientation, while switching to showing a single pane for handset-sized devices or tablets in portrait orientation.

Use `SplitPane` anywhere you have two or more panes in your application where a choice in one pane decides what is displayed in the other pane. For example, you may have a list of Records where details of a single selected Record are shown next to the list. A `SplitPane` is well-suited to this interface since it provides automatic "Back" navigation and a place to show the title of the selected record when only the detail view is showing.

Note that you do not need to use a `SplitPane` as your top-level component containing the whole application, and it _does_ makes sense to use multiple `SplitPane` components in a single application. For example, your top-level container component might be a [TabSet](../classes/TabSet.md#class-tabset), and a [SplitPane](../classes/SplitPane.md#class-splitpane) would be used to manage components in tabs which normally show 2 panes side-by-side on desktop browsers.

#### Device type and overriding

In most cases SmartClient will correctly detect the device running your application, and set the flags [Browser.isTouch](../classes/Browser.md#classattr-browseristouch), [Browser.isHandset](../classes/Browser.md#classattr-browserishandset), [Browser.isTablet](../classes/Browser.md#classattr-browseristablet) and [Browser.isDesktop](../classes/Browser.md#classattr-browserisdesktop) appropriately.

For any uncommon device for which these variables are not set correctly, you can use [Browser.setIsTablet](../classes/Browser.md#classmethod-browsersetistablet), [Browser.setIsHandset](../classes/Browser.md#classmethod-browsersetishandset) and [Browser.setIsTouch](../classes/Browser.md#classmethod-browsersetistouch) to override the auto-detected settings. If you use these APIs, call them **before** creating or drawing any SmartClient components or using any other SmartClient APIs.

Note that the various automatic behaviors triggered by flags on the [Browser](../classes/Browser.md#class-browser) class can be overriden at a fine-grained level on individual components. For example, [SplitPane](../classes/SplitPane.md#class-splitpane) will use 2-pane display when a tablet is detected, however, for a particularly large, high-resolution tablet device, you could instead use 3-pane display by setting [SplitPane.deviceMode](../classes/SplitPane.md#attr-splitpanedevicemode) to "desktop".

#### Mobile look and feel

We recommend using either the Tahoe, Stratus or Obsidian skins for applications that support mobile (or a custom skin based on one of these skins). These skins make maximum use of CSS3 to minimize the number of images that need to be loaded and the number of DOM elements used to create components.

We also do **not** recommend attempting to mimic the native UI of each particular mobile platform, because:

*   if users access the same application via desktop and mobile browsers, consistent appearance and behavior between the desktop and mobile rendering of the application is more important for familiarity than looking similar to other applications on the mobile device
*   mobile platform design overhauls, such as the major changes from iOS6 to iOS7, can easily invalidate efforts to look like native applications on the device
*   there is no single consistent appearance across Android devices because different manufacturers customize the platform a great deal, so efforts to closely mimic any one device won't yield any real consistency

#### iOS 7, browser toolbars and "minimal-ui" setting

Safari in iOS 7.0 will automatically hide and show browser toolbars as the user scrolls around a normal web page, pivots, or touches near edges of the screen. This creates serious problems for web applications, partly because notifications are not reliably fired when toolbars are shown and hidden, and partly because it introduces "dead zones" where an application cannot place interactive controls, since touching there shows browser toolbars instead.

iOS 7.1 introduces a "minimal-ui" setting on the viewport `meta` tag which eliminates most of these problems, by requiring that the user specifically touch the URL bar to reveal browser toolbars. Even with this setting, the top 20px of space _in landscape orientation only_ is still a "dead zone".

SmartClient automatically uses the minimal-ui setting whenever iOS is detected, and also sets [Canvas.defaultPageSpace](../classes/Canvas.md#classattr-canvasdefaultpagespace) to 20px in landscape orientation to avoid components being placed in the dead zone. These default behaviors can be disabled by defining the `isc_useMinimalUI` global variable with the value `false` before the framework is loaded:

```
 <script type="text/javascript">
 window.isc_useMinimalUI = false;
 </script>
```

Whether minimal-ui is used or not, it is recommend to place some kind of non-interactive widget or content in the dead zones created by browser toolbars, for example, a [Label](../classes/Label.md#class-label) showing your company name or application name. When using [Canvas.defaultPageSpace](../classes/Canvas.md#classattr-canvasdefaultpagespace) to have all components avoid a dead zone at the top of the page, you can set [leavePageSpace:0](../classes/Canvas.md#attr-canvasleavepagespace) to allow individual components to place themselves in a dead zone.

#### Configuring the viewport

When a SmartClient application loads, by default a viewport `<meta>` tag is added to the page which, on touch devices, fixes the page zoom to 100% and disables the pinch-zoom gesture. This is usually the expected behavior of a touch-enabled web application because it makes the application look and feel more like a native app. This default setting can be disabled by defining the `isc_useDefaultViewport` global variable with the value `false` before the framework is loaded:

```
 <script type="text/javascript">
 window.isc_useDefaultViewport = false;
 </script>
```
For more information on the mobile device viewport, see:

*   [Configuring the Viewport - Safari Web Content Guide](http://developer.apple.com/safari/library/documentation/AppleApplications/Reference/SafariWebContent/UsingtheViewport/UsingtheViewport.html)
*   [Using the viewport meta tag to control layout on mobile browsers - MDN](https://developer.mozilla.org/en-US/docs/Mozilla/Mobile/Viewport_meta_tag)

#### Orientation Change & Screen Size

When orientation changes, this is treated identically to resizing the browser on a desktop machine. If you've already created a UI that fills the browser and makes good use of available screen space for desktop browsers, the same behaviors will automatically apply when your application runs on mobile devices and the device is pivoted.

If you want to build specialized interfaces that respond to device orientation, the [Page.getOrientation](../classes/Page.md#classmethod-pagegetorientation) API may be used to determine the current orientation of the application, and [the page orientationChange event](../reference.md#type-pageevent) will fire whenever the user rotates the screen allowing applications or components to directly respond to the user pivoting their device.

#### Launching native helper apps (phone, facetime, maps..)

Generally, all that's required to launch native mobile apps is to create an ordinary HTML hyperlink (``<a>`` tag) with a special prefix for the URL specified in the `href` attribute. For example, the following HTML link will place a call when the user finger-taps it:

```
   <a href="tel:8675309">Call Jenny</a>
```
You can provide HTML like this as [HTMLFlow.contents](../classes/HTMLFlow.md#attr-htmlflowcontents). Or use a field of [type:"link"](../reference.md#type-fieldtype) to cause various [DataBoundComponents](../reference.md#interface-databoundcomponent) to render a DataSourceField value as a clickable URL.

The URL prefixes that are valid for iOS are documented [at Apple.com](https://developer.apple.com/library/ios/featuredarticles/iPhoneURLScheme_Reference/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007899-CH1-SW1). Typically, the same prefixes also work for Android, Windows Phone and others.

#### Configure the soft keyboard

[TextItem.browserInputType](../classes/TextItem.md#attr-textitembrowserinputtype) can be set to various values such as "email" or "tel" (telephone number) to hint to mobile devices to use a different software keyboard with specialized keys appropriate for entering certain types of data values.

#### Note on mobile platform performance

When the first modern smartphones were released, it was necessary to use tiny, mobile-specific frameworks to get adequate performance for mobile web applications.

The situation is now completely different: through a combination of hardware improvements, optimizations in mobile browsers and vastly improved network speeds, typical mobile devices are easily able to run applications built with full-featured web platforms like SmartClient. For an application that supports both desktop and mobile interfaces, the worst case scenario for platform performance is often **not** a mobile phone, but an older desktop machine running Internet Explorer.

Unfortunately, there is a lot of out-of-date advice on the web about mobile web development that still advises using ultra-light, feature-poor frameworks for performance reasons. Carefully consider the source and recency of any such advice - the reality is that using such feature-poor frameworks means you will under-deliver with both your desktop _and_ mobile interfaces.

For more background on choosing the right technologies for mobile and desktop web applications, see the [Mobile Strategy Page](http://smartclient.com/product/mobileStrategy.jsp) at smartclient.com.

#### Offline Operation

SmartClient applications support "offline" operation (continuing to work without network access).

Permanent caching of resources such as .js, .css files and images are handled via the standard [HTML5 Manifest](https://www.google.com/search?q=html5+manifest) - just list all the static files your application needs in a manifest file and mobile browsers will cache those resources.

Dynamic data is handled via the [Offline](../classes/Offline.md#class-offline) APIs as well as special DataSource support enabled by [DataSource.useOfflineStorage](../classes/DataSource.md#attr-datasourceuseofflinestorage).

The end result is that you can bookmark a SmartClient application to a phone's home screen and use it offline with cached data, much like an installed native application.

## Packaging as a native application

Via "packaging" technologies such as PhoneGap/Cordova and Titanium, a SmartClient web application can be packaged as an installable native application that can be delivered via the "App Store" for the target mobile platform. Applications packaged in this way have access to phone-specific data and services such as contacts stored on the phone, or the ability to invoke the device's camera.

Both Titanium and PhoneGap provide access to the underlying native device APIs such as the accelerometer, geolocation, and UI. Both frameworks enable application development using only JavaScript, CSS and HTML. Additionally they provide development environments that work across a wide variety of devices.

PhoneGap has good support for native device APIs as noted [here](http://www.phonegap.com/about/feature). Titanium has similar support. There are differences between the two environments and how they expose their APIs, though both provide Xcode-compatible projects that can be compiled and run from the Xcode IDE. See [Integration with Titanium](titaniumIntegration.md#kb-topic-integration-with-titanium) and [Integration with PhoneGap](phonegapIntegration.md#kb-topic-integration-with-phonegap) for more information.

### Related

- [Page.getOrientation](../classes/Page.md#classmethod-pagegetorientation)
- [Page.updateViewport](../classes/Page.md#classmethod-pageupdateviewport)

---
