# Integration with PhoneGap

[← Back to API Index](../reference.md)

---

## KB Topic: Integration with PhoneGap

### Description
PhoneGap documentation, quick start information, and programming guides are available at [http://phonegap.com](http://phonegap.com).

PhoneGap exposes a Contacts API which allows one to find, create and remove contacts from the device's contacts database. Unlike Titanium, which provides many native UI components, PhoneGap relies on 3rd party frameworks for UI components. Additionally, PhoneGap provides no transitions or other animation effects normally accessible in native applications.

_In the following guide, the name "MyMobileApp" refers to a SmartClient mobile application. The instructions are intended to be general, and applicable to other apps by simply substituting the application name and the few other app-specific details._

#### Installing PhoneGap
Beginning with PhoneGap 2.9.0, PhoneGap is an NPM (Node.js Packager Manager) package. You will need to install Node.js first in order to install PhoneGap. (**Tip for Mac users:** [Homebrew](http://brew.sh) is a simple and easy way to install the latest version of Node.js and npm: `brew install node`)

Once Node.js is installed, see [http://phonegap.com/install/](http://phonegap.com/install/) for instructions on installing PhoneGap.

#### Creating the PhoneGap Project
Use the [`phonegap` command line utility](http://docs.phonegap.com/en/edge/guide_cli_index.md.html) to create a new folder containing the project files:
```
phonegap create --id com.mycompany.apps.MyMobileApp --name "MyMobileApp" path/to/project_folder
```

The project ID and name should be changed for your app.

#### General Instructions
Within the project folder, PhoneGap creates a special `www/` folder which contains the application JavaScript code and other assets. Within this folder, only `config.xml` is needed. All other files of the default "Hello PhoneGap" app can be deleted.

You will need to open the application's main HTML file in a text editor to make a few changes:

*   Change the DOCTYPE to the HTML5 DOCTYPE: `<!DOCTYPE html>`
*   Add a ``<script>`` tag to the ``<head>`` element to load `cordova.js`:
    ```
    <script type="text/javascript" charset="UTF-8" src="cordova.js"></script>
    ```
    
    **NOTE:** The `www/` folder should not contain `cordova.js`. In other words, don't try to copy `cordova.js` into the `www/` folder. PhoneGap automatically adds the appropriate version of this script, which is different for each platform.
    
*   Ensure that the following ``<meta>`` tags are used, also in the ``<head>`` element:
    ```
    <meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
    <meta name="format-detection" content="telephone=no">
    <meta name="viewport" content="initial-scale=1, width=device-width, user-scalable=no, minimum-scale=1, maximum-scale=1">
    ```
    

After making those changes, you will need to defer starting the application until the `[deviceready](http://docs.phonegap.com/en/edge/cordova_events_events.md.html#deviceready)` event has fired, particularly if your application invokes any PhoneGap API function. In SmartClient, deferring the application can be accomplished by wrapping all application code within a 'deviceready' listener:

```
<script type="text/javascript">
document.addEventListener("deviceready", function onDeviceReady() {
    // application code goes here
}, false);
</script>
```
#### iOS Platform (iPhone & iPad)

1.  Open **Terminal**, `cd` into the project folder, and run:
    ```
    phonegap build ios
    ```
    
2.  Within the newly-created `platforms/ios/` folder, open the Xcode project `MyMobileApp.xcodeproj`.
3.  In Xcode, set the active scheme to **MyMobileApp > iPhone Retina (4-inch) > iOS 7.0** or some other simulator destination. Then click the **Run** button. Xcode will start the iPhone Simulator and run the app.
4.  When you are finished testing the application in the simulator, click the **Stop** button.

It is helpful to pay attention to the output window when testing the app within iOS Simulator. The output window contains all logs to `[window.console](https://developer.mozilla.org/en-US/docs/Web/API/console)` and messages from the Cordova framework itself. One common issue is `ERROR whitelist rejection: url='SOMEURL'`, which means that SOMEURL has not been added to ``<access origin="..."/>`` in `config.xml`. Refer to the [Domain Whitelist Guide](http://docs.phonegap.com/en/edge/guide_whitelist_index.md.html#Domain%20Whitelist%20Guide) for more information.

Once you have completely tested the application within the simulator, you should test the app on real hardware. Refer to Apple's [App Distribution Guide](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/Introduction/Introduction.html) for complete instructions on provisioning the app for testing devices, in particular, the section titled [Beta Testing Your iOS App](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/TestingYouriOSApp/TestingYouriOSApp.html#//apple_ref/doc/uid/TP40012582-CH8-SW1).

Apple has deprecated UIWebView and we recommend switching to the officially supported [WKWebView](https://github.com/apache/cordova-plugin-wkwebview-engine) plugin to resolve momentum scrolling issues and obtain more Safari-like behavior.

#### Android Platform
To begin targeting Android devices, follow the instructions on the [Android Platform Guide](http://docs.phonegap.com/en/edge/guide_platforms_android_index.md.html).

It is helpful to monitor the LogCat view in Eclipse to verify that your application is working correctly. Common errors include:

*   `Application Error The protocol is not supported. (gap://ready)`
    
    This means that the incorrect `cordova.js` script is being used. You must use the `cordova.js` for Android.
    
    Try updating the 'android' platform to fix the problem:
    
    ```
    phonegap platform update android
    ```
    
*   `Data exceeds UNCOMPRESS_DATA_MAX`
    
    In older versions of Android (pre-2.3.3), there is a 1 Megabyte limit on the size of individual Android app assets. This error message means that one asset file exceeds this limit. You should see a popup alert dialog containing the name of the problematic file, and then the app will crash.
    
    The "Data exceeds UNCOMPRESS\_DATA\_MAX" error can be seen if, for example, the SmartGWT.mobile application was compiled in DETAILED or PRETTY mode.
    

#### Samples

The SmartClient SDK package has a sample application called MyContacts which demonstrates how to work with the PhoneGap API in a SmartClient app. The main SmartClient code is located in `smartclientSDK/examples/phonegap/MyContacts`. An Xcode project used to package the app for iOS devices is located at `smartclientSDK/examples/phonegap/MyContacts-iOS`. An Eclipse project used to package the app for Android devices is located at `smartclientSDK/examples/phonegap/MyContacts-Android`.

---
