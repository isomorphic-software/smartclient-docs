# Automated Testing

[← Back to API Index](../reference.md)

---

## KB Topic: Automated Testing

### Description
SmartClient supports automated testing with a variety of tools. See the [AutoTest](../classes/AutoTest.md#class-autotest) class for information about how to generate and resolve [AutoTestLocators](../reference_2.md#type-autotestlocator) and other utilities within the SmartClient framework related to generating automated tests.

#### Playwright
SmartClient applications work smoothly with [Playwright](https://playwright.dev/).

The SDK package provides an example `commands.js` file that defines [Playwright fixtures and helpers](https://playwright.dev/docs/test-fixtures) designed to locate and interact with SmartClient components, automatically handle asynchronous operations, record performance data, and more. For step-by-step guidance on using Playwright with SmartClient, see [Integrating SmartClient with Playwright](smartClientPlaywright.md#kb-topic-integrating-smartclient-with-playwright).

#### Cypress
SmartClient applications integrate seamlessly with [Cypress](https://www.cypress.io/).

The SDK package includes a sample `commands.js` configuration file with custom [cypress commands](https://docs.cypress.io/api/cypress-api/custom-commands) to identify and interact with SmartClient components, seamlessly wait for asynchronous operations, recording timing data and more. See the [Cypress integration overview](smartClientCypress.md#kb-topic-integrating-smartclient-with-cypress) for details on how to use Cypress with SmartClient.

#### Selenese

Selenese is a simple HTML table-based test format that can be authored without programming skills. SmartClient provides enhanced Selenese commands and locators for reliable interaction with SmartClient widgets.

**Playwright-based Selenese Runner (Recommended)**

The recommended approach for executing Selenese tests is the Playwright-based `selenese-runner.js`, located in `tools/playwright/`. This runner requires only Node.js and Playwright (no Java or Selenium installation), automatically waits for SmartClient system quiescence after each command, and outputs JUnit XML for CI/CD integration.

**Java-based SeleneseRunner**

For Java-based environments, SmartClient provides [SeleneseRunner](server/javadoc/com/isomorphic/webdriver/SeleneseRunner.html), which executes Selenese via WebDriver. This runner can also convert Selenese to Java/JUnit code.

**Recording Selenese**

Selenese tests can be recorded using Selenium IDE. See [Using\\n Selenium](usingSelenium.md#kb-topic-using-selenium-scripts-selenese) for setup instructions. Note that while Selenium IDE 2.9 (with Firefox 52 ESR) provides the best recording experience with SmartClient extensions, recorded tests can be executed via the Playwright runner without any Selenium installation.

#### TestRunner

[TestRunner](testRunner.md#kb-topic-testrunner) is a system for automatically running a suite of Selenium tests, commiting the results to a database, and reporting any regressions (or fixes) via email.

#### Selenium WebDriver

WebDriver uses browser-specific drivers to enable Selenium interaction. SmartClient provides WebDriver support with the same custom locator strategies and commands as Selenese.

For most use cases, we recommend Playwright or Cypress over WebDriver, as they provide a more modern development experience. WebDriver remains useful for teams with existing Java/Selenium infrastructure or specific integration requirements.

**WebDriver Usage**

You can use Selenium IDE to record tests, then use `SeleneseRunner` to convert the Selenese to Java code that uses SmartClient locators and our WebDriver wrappers.

To retrieve locators for hand-written tests, use [AutoTest.installLocatorShortcut](../classes/AutoTest.md#classmethod-autotestinstalllocatorshortcut) (key-combo plus click) or [AutoTest.getLocator](../classes/AutoTest.md#classmethod-autotestgetlocator) from the [Developer Console](debugging.md#kb-topic-debugging).

**NOTE:** Do not use Selenium IDE's built-in WebDriver export feature; it doesn't support custom commands or locators. Use `SeleneseRunner` instead.

**WebDriver Classes overview**

For certain tests it can make sense to use WebDriver Java support directly.

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

### Related

- [EventStream.getAsSeleneseHTML](../classes/EventStream.md#method-eventstreamgetasselenesehtml)
- [EventStream.getAsSeleneseCommands](../classes/EventStream.md#method-eventstreamgetasselenesecommands)

---
