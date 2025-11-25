# DataSource and Component XML Localization

[← Back to API Index](../main.md)

---

## KB Topic: DataSource and Component XML Localization

### Description
DataSources can be created in [several ways](dataSourceDeclaration.md#kb-topic-creating-datasources). DataSources created directly in JavaScript can be internationalized via the techniques described in the main [i18n article](i18n.md#kb-topic-internationalization-and-localization). DataSources which are declared in XML (.ds.xml files) and are read by the SmartClient server, which are normally loaded into a .jsp page via the `<isomorphic:loadDS>` JSP tag, can instead be internationalized using an approach similar to the internationalization of JSP files with JSTL tags. This approach is also supported for screens defined using [Component XML](componentXML.md#kb-topic-component-xml).

**Note:** The tags we use for internationalizing SmartClient XML files look like standard JSTL tags; this is intentional, simply because developers are familiar with JSTL. However, the tags are being processed by SmartClient code, **not** JSTL, so only the specific tags documented here are supported.

Given the following DataSource located in /shared/ds/supplyItem.ds.xml:

```
 <DataSource ID="supplyItem">
     <fields>
         <field name="itemName">
             <title>Item Name</title>
             <validators>
                 <Validator type="lengthRange" max="40">
                     <errorMessage>Must be 40 characters or less.</errorMessage>
                 </Validator>
             </validators>
         </field>
     </fields>
 </DataSource>
 
```
To localize the title and validator error string of the `itemName` field, change the DataSource definition as follows:
```
 <DataSource ID="supplyItem" xmlns:fmt="WEB-INF/">
     <fields>
         <field name="itemName">
             <title><fmt:message key="itemTitle"/></title>
             <validators>
                 <Validator type="lengthRange" max="40">
                     <errorMessage><fmt:message key="itemLengthRangeValidator"/></errorMessage>
                 </Validator>
             </validators>
         </field>
     </fields>
 </DataSource>
 
```
This will cause SmartClient Server to look for a [ResourceBundle](http://docs.oracle.com/javase/8/docs/api/java/util/ResourceBundle.html#getBundle-java.lang.String-java.util.Locale-) called "supplyItem", containing keys "itemTitle" and "itemLengthRangeValidator", and replace the `<fmt:message>` tags with the values from the resource bundle in the expected way. It obtains the user's `Locale` from the servlet request, but you can override this if you want to force an application-specific locale, regardless of the user's operating system settings. To do this, either specify a "locale" attribute in the `<loadDS>` tag, like this:  
``<loadDS ID="myDataSource" locale="es" />``

or specify a "locale" parameter on HTTP requests to the `DataSourceLoader` and `IDACall` servlets (the latter is typically done via [RPCManager.actionURL](../classes/RPCManager.md#classattr-rpcmanageractionurl)).

In both of these cases, the locale parameter should be an underscore-separated string conforming to the rules described in [this article](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html) on Java internationalization. For example, "fr" (French language) or "en\_US" (English language, US location).

As mentioned, SmartClient Server will look for a `ResourceBundle` called "supplyItem" in this case because it defaults to the name of the DataSource. It is possible to override this default at both the DataSource and field levels:

*   Specify `<fmt:bundle>` as a top-level DataSource tag, like this:  
    ```
       <DataSource  xmlns:fmt="WEB-INF/" ID="supplyItem">
          <fmt:bundle basename="com.isomorphic.test.i18n" />
          ...
     </DataSource>
    ```
    
*   Specify the bundle name in the individual `<fmt:message>` tags, like this:  
    ```
       <title><fmt:message key='title1' bundle="com.mycompany.MyProperties" /></title>
    ```
    

When you name a resource bundle manually like this, if you qualify the name it influences where we expect to find that resource bundle. In the above example, we would look in the `com.mycompany` package. For unqualified names (including the default of the DataSource name that we use in the absence of an override), we look in the so-called "default package", which corresponds to the root of your classes directory or the root of a .JAR file.

Note that the `xmlns:fmt` attribute in the DataSource definition is required by the XML parser if you intend to use our `fmt:message` features. However, the actual value you use is unimportant as long as it is present.

Although these examples don't show it, note that it is also possible to internationalize DataSource-level values in the same way as field-level values - for example:

```
   <DataSource  xmlns:fmt="WEB-INF/" ID="i18nTest"> 
     <title><fmt:message key="dsTitle" /></title>
      ...
 </DataSource>
 
```

Any property on a DataSource or on a UI component that is documented to be of "String" type or any derived type (such as "URL") supports the `fmt:message` tags.

Note that any amount of whitespace around `<fmt>` tag is ignored, unless there is also some text, then whitespace becomes significant as well. A declaration like this one:

```
   <DataSource  xmlns:fmt="WEB-INF/" ID="i18nTest"> 
     <title>
         Some text <fmt:message key="dsTitle" />
     </title>
      ...
 </DataSource>
 
```
.. will cause linefeed / carriage return characters to be embedded in your title as well as the text. This can be useful in situations where you want to embed small amounts of static text in a localized attribute, but most of the time, you will want the `<fmt>` tag on one line with the surrounding tag (eg "title").

If any HTML tags are needed around a `<fmt>` value, you can place them into the resource bundle or use the _CDATA section_ to escape them in the XML file:

```
  <DataSource  xmlns:fmt="WEB-INF/" ID="i18nTest"> 
     <title><![CDATA[<b>]]><fmt:message key="dsTitle" /><![CDATA[</b>]]></title>
      ...
 </DataSource>
 
```
#### Unicode support
The Java language insists that `.properties` files be encoded with ISO-8859-1 - in other words, that they be plain ASCII files. This means that any non-ASCII characters have to be escaped, like so: **\\u1234**. For languages like Russian or Japanese, that are based on completely non-ASCII character sets, this obviously leads to `.properties` files that are entirely escaped references, and are not human-readable. Although the `nativetoascii` tool is provided with Java to make the creation of these escaped files less tedious, it is still inconvenient that this "compilation step" is required.

SmartClient avoids the need for this when localizing DataSources and Component XML by directly supporting `.properties` files encoded with UTF-8. To make use of this:

*   Encode your `.properties` file with UTF-8, preferably without a BOM (Byte Order Marker). SmartClient Server will simply ignore the BOM in a `.properties` file if it is present, but you may see odd behavior from other software if the BOM is present in other types of file - for example, JSP snippets that are included in other pages. The BOM has no meaning in a UTF-8 file anyway, so we recommend just omitting it from all your UTF-8 files (though note that doing this may confuse some editing software, particularly on Windows)
*   Encode your bootstrap file(s) in UTF-8 and set headers or meta tags to inform the browser that the file is UTF-8 encoded, as described in [this article](i18n.md#kb-topic-internationalization-and-localization)
*   In your `<fmt:bundle>` tag, specify an `encoding` attribute. There are only two supported values for this attribute: "utf-8" and "iso-8859"
*   You can also override the encoding in individual `<fmt:message>` tags, just like to can override the bundle to use. Again, just specify an `encoding` attribute
*   You can make UTF-8 encoding the global default by setting attribute `i18n.resourceBundle.parse.utf-8` to true in your `server.properties` file. This prevents you from having to explicitly specify `encoding="utf-8"` in all your `.ds.xml` and `.ui.xml` files
*   Note that `.properties` files are located and parsed by SmartClient framework code when `encoding="utf-8"` is in force. Our parsing code only supports the naming conventions explained in the article linked to above; specifically, it does not support the additional "script" and "extension" elements introduced in Java 7. File names must be of the form "basename\_language\_COUNTRY\_VARIANT", where "COUNTRY" and "VARIANT" are optional. Examples: "fr", "en\_US", "en\_GB\_POSIX"

#### Component XML
All of the above applies similarly for localizing screens defined using [Component XML](componentXML.md#kb-topic-component-xml). For example:
```
 <isomorphicXML xmlns:fmt="WEB-INF/">
   <fmt:bundle basename="com.isomorphic.test.i18n.test" />
   <Window ID="testWin1">
     <title><fmt:message key='title1' /></title>
   </Window>
 </isomorphicXML>
 
```
Note the following differences between localizing `.ds.xml` (DataSource) files and localizing `.ui.xml` (component XML) files:

*   The ``<isomorphicXML>`` tag, which is ordinarily only used to wrap multiple widget definitions to give a valid XML file, is required if you are using this internationalization technique.
*   Because there is no concept of an "ID" associated with a `.ui.xml` file, there is no default bundle like there is with DataSource definitions. Instead, you have to specify the bundle by hand, either by adding a `<fmt:bundle>` tag as an immediate child of the ``<isomorphicXML>`` tag, or by specifying `bundle` attributes in your individual `<fmt:message>` tags.
*   Locale can be overridden, as described for DataSources above, by specifying a "locale" parameter on HTTP requests to the `ScreenLoaderServlet` (this is done for you when you pass a locale to the [RPCManager.loadScreen](../classes/RPCManager.md#classmethod-rpcmanagerloadscreen) method).

#### Custom localization provider support
Custom localization providers can be configured for the entire framework or for specific DataSource and Component XML instances based on their names. For more details see javadoc for `com.isomorphic.util.LocaleMessageProviderRegistry` server-side API.
#### Troubleshooting
If something went wrong, we use fmt string as a value: `<fmt:message key="message_key">`. Getting similar value instead of localized message means that either `bundle` could not be found or the `key` is incorrect, look for warnings in server logs for specific details.

---
