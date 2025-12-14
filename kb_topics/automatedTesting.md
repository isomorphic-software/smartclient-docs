# Automated Testing

[← Back to API Index](../reference.md)

---

## KB Topic: Automated Testing

### Description
SmartClient supports automated testing with a variety of tools.

#### Selenium / Selenese

SmartClient includes free support for [Selenium](https://docs.seleniumhq.org/) for robust recording and playback of tests, including the ability to record on one browser and play back on others, via [Selenese](https://www.seleniumhq.org/docs/02_selenium_ide.jsp#selenium-commands-selenese) enhanced with SmartClient-specific locators and commands that provide a stable means of locating SmartClient widgets and ensuring they're ready for interaction.

To write Selenese, we recommend Selenium IDE 2.9, which is compatible with [Firefox 52 ESR](https://www.mozilla.org/en-US/firefox/organizations/), and can directly load our user extensions, located in the `smartclientSDK/tools/selenium/` directory. A user guide explaining how to create and interactively run selenese with the IDE can be found [here](usingSelenium.md#kb-topic-using-selenium-scripts-selenese). Selenium IDE 3, which requires Firefox Quantum, has just released support for plugins that should allow the eventual migration of our user extensions, but for now only Selenium IDE 2.9 can load SmartClient locator and command extensions.

**SeleneseRunner**

For automated testing, SmartClient provides [SeleneseRunner](server/javadoc/com/isomorphic/webdriver/SeleneseRunner.html), a tool that executes SmartClient-enhanced Selenese created by Selenium IDE via emulation, since Selenium 3 no longer supports the Selenium RC APIs and thus can't execute Selenese that requires custom user extensions. Internally, `SeleneseRunner` makes use of the APIs in our WebDriver wrappers to resolve locators properly and execute SmartClient-enhanced Selenese.

`SeleneseRunner` can be used to:

*   execute Selenese directly from the command line
*   execute Selenese from inside a Java program (eg, as part of a JUnit test)
*   convert a Selenese test to Java code (as a JUnit test)

See the server-side JavaDoc linked above for more information on how to use these features.

#### TestRunner

[TestRunner](testRunner.md#kb-topic-testrunner) is a system for automatically running a suite of Selenium tests, commiting the results to a database, and reporting any regressions (or fixes) via email.

#### Selenium WebDriver

WebDriver, supported since Selenium 2, uses a different basic architecture in which a driver is added to each browser to enable Selenium interaction, instead of doing so from JavaScript.

Support for WebDriver-based testing for SmartClient is now available with the same custom locator strategies and custom commands as we provide for Selenese. **However, we continue to recommend Selenese rather than WebDriver-based Selenium, because Webdriver requires Java programming skills.** Tests created in Selenium IDE and stored in Selenese can be executed by a variety of tools without requiring Java skills, including our own [testRunner](testRunner.md#kb-topic-testrunner). Most ways of running WebDriver tests involve Java coding skills or at least the ability to work with a Java IDE. This tends to mean that all QA personnel must either have Java skills or drain the time of Java developers on repetitive tasks.

Ultimately, our current recommendation is to use Selenium IDE and Selenese exclusively or at least primarily. If there are critically important tests that you can only build via WebDriver, use WebDriver for those tests only, or use manual testing for those tests.

**WebDriver Usage**

When using WebDriver, we recommend using Selenum IDE as a starting point to record and store tests. You can then call `SeleneseRunner` to convert that Selenese to Java code that uses SmartClient locators and invokes the appropriate APIs on our WebDriver wrappers.

Once you become familiar with what code is generated for common interactions, you may want to write tests directly without using Selenium IDE. In this case, you can retrieve locators for specific elements in a couple of ways. The [AutoTest.installLocatorShortcut](../classes/AutoTest.md#classmethod-autotestinstalllocatorshortcut) method allows developers to retieve a locator for the element under the mouse via a simple key-combo plus click. Alternatively you can use [AutoTest](../classes/AutoTest.md#class-autotest) APIs, such as [AutoTest.getLocator](../classes/AutoTest.md#classmethod-autotestgetlocator), which takes a [Canvas](../classes/Canvas.md#class-canvas) or DOM element, to get the locators you need. These can be invoked by evaluating script while a SmartClient page is loaded (from the [Developer Console](debugging.md#kb-topic-debugging) or from the native browser console).

**NOTE:** Selenium IDE has an option to export tests as WebDriver-compatible code. **Do not use** this feature, it exports useless code that doesn't understand custom commands, custom locators, or other key features of Selenium IDE. Use `SeleneseRunner` instead.

**WebDriver Classes overview**

Storing and executing Selenese tests recorded in the Selenium IDE is recommended as the primary approach for using WebDriver. However, for certain rare tests it can make sense to use WebDriver Java support directly.

SmartClient support for WebDriver is based around 3 different Java classes:

1.  [ByScLocator](server/javadoc/com/isomorphic/webdriver/ByScLocator.html): This implements the ability to find WebElements or WebDriver "By" objects using SmartClient Locator strings. See [usingSelenium](usingSelenium.md#kb-topic-using-selenium-scripts-selenese) for more background on Locator strings and how to obtain them. Given a locator String, example usage is:
    ```
     ByScLocator.scLocator("//ListGrid[ID=\"countryList\"]/body/row[countryCode=US||0]/col[fieldName=countryCode||0]")
    ```
    
2.  [SmartClientWebDriver](server/javadoc/com/isomorphic/webdriver/SmartClientWebDriver.html): This is an abstract class which provides a number of different methods for interacting with the browser, such as:
    
    *   open a browser at a particular URL
    *   find the element or elements which match a given "By" object (either ByScLocator, or a standard WebDriver locator)
    *   perform events and operations (click, drag, select etc)
    *   perform custom SmartClient validations / state checks, such as whether a grid has loaded data
    
    Three concrete implementations of SmartClientWebDriver are provided: SmartClientFireFoxDriver, SmartClientChromeDriver and SmartClientIEDriver. There is also a SmartClientRemoteWebdriver class which allows the injection of a manually configured RemoteWebDriver instance. This might be necessary, for example, for use with Selenium Grid.
    
3.  [ScActions](server/javadoc/com/isomorphic/webdriver/ScActions.html): a SmartClient-specific version of the standard WebDriver "Action" class, providing a builder pattern to create a sequence of operations which can then be perform()ed.

These classes are packaged in the library isomorphic\_webdriver.jar, which can be found in the directory WEB-INF/lib-WebDriverSupport (along with several 3rd-party supporting libraries).

General information regarding WebDriver can be found [here](http://docs.seleniumhq.org/docs/03_webdriver.jsp#introducing-webdriver). Setup for WebDriver is more complex than for classic Selenium. Drivers can be downloaded for [Firefox](https://github.com/mozilla/geckodriver/), [Google Chrome](https://sites.google.com/chromium.org/driver/), [Internet Explorer](https://www.seleniumhq.org/download/), and [MS Edge](https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/).

**JUnit + WebDriver**

Explore [JUnit + Selenium WebDriver](jUnitWebDriver.md#kb-topic-junit--selenium-webdriver), where we walk through a JUnit test targeting a SmartClient Showcase sample.

**File Upload Example Test**

As discussed above, one advantage which WebDriver does have over Classic Selenium is the ability to test file upload. It is still limited in that if a click is triggered on the file selection button an OS native file selection dialog will be triggered in which case the test will be suspended until the file is manually selected. To avoid this, the sendKeys() method can be used to enter the file location.

Sample code:

```
    /**
     * The following test runs against localhost and requires a small (< 5mb) image to be in /tmp/image.jpg
     */
    public void fileUploadSC() throws Exception {
        SmartClientWebDriver driver = new SmartClientFirefoxDriver();
        driver.setBaseUrl("http://localhost:8080/showcase/");
        driver.get("#upload");

        final int origSize = driver.findElements(ByScLocator.scLocator("//TileGrid[ID=\"mediaTileGrid\"]/tile")).size();

        By titleInput = ByScLocator.scLocator("//DynamicForm[ID=\"uploadForm\"]/item[name=title||title=Title||index=0|"
                                             +"|Class=TextItem]/element");
        driver.click(titleInput);
        driver.sendKeys(titleInput, "test image: " + origSize);
        
        By uploadForm = ByScLocator.scLocator("//DynamicForm[ID=\"uploadForm\"]/");
        WebElement form = driver.findElement(uploadForm);
        WebElement findElement = form.findElement(By.xpath("//input[@type='FILE']"));
        /*
         * The following causes a native dialog to be created which prevents further progress. Do NOT uncomment!
         * We just have to sendKeys() to it
         */
        //findElement.click(); 
        
        findElement.sendKeys("/tmp/image.jpg"); // A local file. Please change accordingly

        By saveButton = ByScLocator.scLocator(
                             "//DynamicForm[ID=\"uploadForm\"]/item[title=Save||index=2||Class=ButtonItem]/button/");
        driver.waitForElementClickable(saveButton);
        driver.click(saveButton);
        /*
         * Note the following fails once the grid contains more than 3 rows of data
         * as the index becomes inconsistent as tiles scrolled out of site are removed
         * and the indices change
         */                                                        
        By tile = ByScLocator.scLocator("//TileGrid[ID=\"mediaTileGrid\"]/tile[Class=SimpleTile||index="
                         +(origSize)+"||length="+(origSize+1)+"||classIndex="+(origSize)+"||classLength="+(origSize+1)+"]/");
        driver.waitForElementClickable(tile);
        WebElement tile1 = driver.findElement(tile);
        assertEquals("test image: " + origSize, tile1.getText());
        assertEquals(origSize + 1, driver.findElements(ByScLocator.scLocator("//TileGrid[ID=\"mediaTileGrid\"]/tile")).size());
        driver.close();
        driver.quit();
    }
 
```

**WebDriver Troubleshooting**

There is a known issue that [native events do not work with IE in Windows 8/8.1](https://code.google.com/p/selenium/issues/detail?id=4403) that may manifest in WebDriver as clicks having no effect. One potential workaround is to disable native events:

```
    DesiredCapabilities caps = DesiredCapabilities.internetExplorer();
    caps.setCapability("nativeEvents",false);
    SmartClientWebDriver driver = new SmartClientIEDriver(caps);
```
It's also been reported that changing the second line above to:
```
    caps.setCapability("requireWindowFocus", true);
```
also resolves the issue, with the side effect that WebDriver then moves the mouse cursor.

In some versions of Internet Explorer, it's been reported that you must add the URL targeted by WebDriver to the "Trusted Sites" under Internet Options >> Security in order to allow the browser to communicate properly with Selenium. A discussion of the setup needed to use WebDriver's InternetExplorerDriver can be found [here](https://github.com/SeleniumHQ/selenium/wiki/InternetExplorerDriver).

**Other tools**

SmartClient supports a special JavaScript API to allow other test tools to integrate in the same manner as Selenium and WebDriver. This API allows the test tool to record an abstract "locator" string representing the logical name for an interactive DOM element, and then during test playback, retrieve a DOM element given a locator.

This is critical because, like many modern Ajax systems, SmartClient generates different DOM elements in different browsers, in different skins, and in different versions of SmartClient. Testing tools that try to directly record the generated SmartClient DOM produce extremely brittle tests because they are effectively recording undocumented internals.

Using the "locator" API allows you to record or write tests that will run in any browser supported by SmartClient, in any version of SmartClient, and in any skin. It also makes tests more readable and easier to understand and maintain.

Different testing tools vary in how easily they can be configured to use the locator API, and in some older tools it can be a large effort. We highly recommend using our Selenium extensions - it often makes sense to use them even if you have to use them in parallel with another, older testing tool. If you are forced to use another tool exclusively:

*   Read the [documentation for the locator system](../classes/AutoTest.md#class-autotest)
*   Read over the source code of our Selenium extensions to get a clear understanding of how the Selenium integration works, because this will be analogous to the work you'll need to do
*   Search the [forums](http://forums.smartclient.com/) for other developers who are trying to use the same test tool with SmartClient, and share efforts

---
