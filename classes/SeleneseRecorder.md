# SeleneseRecorder Documentation

[← Back to API Index](../main.md)

---

## Class: SeleneseRecorder

*Inherits from:* [VLayout](../main.md#class-vlayout)

### Description
Selenese Recorder is a tool that can automatically record browser interaction as Selenese Commands, or play back Selenese previously recorded by launching a separate browser using Selenium APIs. Rather than creating your own instance of the recorder, you can also use it from the the [Developer Console](../kb_topics/debugging.md#kb-topic-debugging), which avoids having to integrate it with your application.

#### Initial Setup

To enable the Selenium Recorder to play back your Selenese, you must first configure the server with the location of the Gecko (Firefox) and/or Chrome driver on your system. To do this, edit the [server properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file) file to uncomment the following lines and define the associated properties to point at your driver executables:

```
 #system.setProperty.webdriver.gecko.driver: /usr/local/bin/geckodriver
 #system.setProperty.webdriver.chrome.driver: /usr/local/bin/chromedriver
 #system.setProperty.webdriver.edge.driver: /usr/local/bin/msedgedriver
```
This will also make the "Recorder" tab visible in the [Developer Console](../kb_topics/debugging.md#kb-topic-debugging), to allow you to use its Selenium Recorder targeting your main browser window without having to create or manage a `SeleneseRecorder` widget in your app.

If you want Selenium to launch from a different server than your page is loaded from, you can set [seleneseRunnerActionURL](#attr-seleneserecorderseleneserunneractionurl) to the desired URL (or set the server property `DeveloperConsole.webdriver.actionURL` to affect the Developer Console's Recorder tab). This will allow you to run Selenium locally and open a browser directly on your machine, even if your primary SmartClient server is remote.

#### Recording Selenese

To record Selenese against the target page, make sure that the "Capture Commands" checkbox at the bottom of the tool is checked, and then interact normally with the target page. Your clicks and typing will automatically be converted into Selenese commands and appear in the grid in the tool's main window. Recorded commands will appear on a delay to allow double clicks and other complex interaction to be properly captured.

After you capture Selenese from such interaction, you can edit commands, reorder them, or even delete one or more commands from the grid as needed. Options to copy and paste an existing command or add a new custom command to the script are available by context-clicking. You can also "mass edit" certain fields for a set of selected Selenese command records via context click.

To save your script, type something in the "Test Name" box (or accept the default), and click "Export". This will cause your browser to save the script as a downloaded file. Depending on your browser configuration, you may be prompted for where to save the script.

**Note:** support for recording is currently limited, with automatic command creation only working for clicks and typing.

#### Playing back Selenese

You can play back the current recorded script, or one you load via the tool's "Choose File" button. To start playback, click the "Run" button. This will open a new browser instance and begin to run the script in that browser. While it's running, you can click the "Stop" button to abort execution, or "Pause" (the changed title of the "Run" button), to pause execution and allow for stepping. In stepping mode, click "Step" to advance foward by one command so you can debug any issues or hand-modify the widget state or browser data. When you're done, click "Go" to resume automatic execution of the script. Use the "Settings" dialog accessible via the same-titled button to modify the base URL for your script or select which browser to run (Chrome/Firefox/MS Edge/IE).

As the script executes, each command in the grid will be highlighted green if the command succeeds, or red if it fails. The output of each command also gets stored into the "Output" grid column where you can easily check it. When the script is done, the circular indicator icon on the bottom right of the tool will be set green to indicate that the script succeeded, or red to indicate that it failed, and you can download or view a report by clicking on the "Get Report" button.

For each command, you can configure whether it will stop the entire script if it fails, or the failure ignored (but still indicated in the highlighting and history), or the failing command reattempted. The maximum number of tries can be set globally from the "Settings" dialog by changing "Max Retry Attempts". The "screenshot" (three state) checkbox allows you to configure whether a screenshot is always taken for that command (checked), never taken (unchecked), or taken only upon failure (filled). Screenshots can be downloaded by clicking on the icon in the record (if present) to the right of the "Output" column.

As each script command executes, an implicit Selenium "waitFor..." command is automatically run by default to wait for the target canvas or canvii to become ["ready"](AutoTest.md#classmethod-autotestissystemdone), meaning that the target is not queued for redrawing, has no pending fetch or scroll, server communications, etc. You can modify this behavior (if you know it's not needed for one or more commands) by unchecking the "Wait For" grid column. The default global behavior can also be configured via the "Settings" dialog.

#### Running a Test Suite

While the Selenese Recorder only supports a single Selenese script, you can run a Selenium suite file using the [SeleneseRunner](https://smartclient.com/smartgwtee-latest/server/javadoc/com/isomorphic/webdriver/SeleneseRunner.html) command line tool. To see usage information, invoke the `SeleneseRunner` main Java class, picking up the provided Isomorphic and thirdy-party JARS:

```
 java -cp "../lib/*" com.isomorphic.webdriver.SeleneseRunner
```
To run a suite file that targets a locally-deployed SmartClient Showcase, for example, you can then issue the following command line, modifying the browser driver path as per your local installation:
```
 java -Dwebdriver.gecko.driver=/usr/bin/local/geckodriver -cp "../lib/*" com.isomorphic.webdriver.SeleneseRunner http://localhost:8080/ -j report.xml suite.html
```
where `suite.html` is the suite to run, and `report.xml` is the name of file into which the output should be reported in XML format.

### Groups

- experimental

---
## Attr: SeleneseRecorder.seleneseRunnerActionURL

### Description
URL of the SmartClient server to use to launch and run Selenium. Left unset, the recorder will attermpt to run on the server from which the framework was loaded.

### See Also

- [RPCManager.actionURL](RPCManager.md#classattr-rpcmanageractionurl)

**Flags**: IR

---
## Attr: SeleneseRecorder.sizeToControlsOverflow

### Description
Whether to always expand the command grid horizontally to match any overflow in the recorder toolbar. To look good when the tool is placed inside an app, this is enabled by default, but it can be turned off if the tool occupies the entire browser width, where you might prefer that viewport overflow only clips the toolbar, and not the grid.

**Flags**: IR

---
## Attr: SeleneseRecorder.widgetsToIgnore

### Description
Canvii that you want to ignore when capturing Selenese. Any canvas from this list, or one of its descendants or menus, as determined by the locator parent chain, will be excluded. This allows you integrate the recorder into a page without having interaction with the tool itself generate unwanted recording.

The tool widget itself and dialogs it spawns will be automatically ignored, so this is required only to specify additional widgets to ignore, such as a window that contains the tool, related forms, a launch button, etc.

**Flags**: IR

---
