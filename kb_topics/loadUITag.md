# <isomorphic:loadUI>

[← Back to API Index](../reference.md)

---

## KB Topic: <isomorphic:loadUI>

### Description
_produces:_ JavaScript

This tag converts SmartClient UI components declaratively specified in an XML "UI" file to JavaScript for execution in the browser.

The XML->JS translation works just like with [xmlTag](xmlTag.md#kb-topic-isomorphicxml), except the XML is read from an external file instead of from the body of the tag.

Note that this JSP tag must be surrounded by `<SCRIPT>` tags in the JSP because it generates JavaScript code. Like other tags that generate JavaScript code, this tag can be used in a JSP that is included from your main page in order to create separate cacheability. For example:

```
 <SCRIPT SRC="myUIDefinitions.jsp"></SCRIPT>
 
```

**Tag Attributes:**

**name**  
_value format_: String - name of UI file to load (minus extension)  
_default value_: NONE

This attribute specifies the name of the file that contains the UI components to translate. UI files are located in `[webroot]/shared/ui` by default. This location is changeable in `[webroot]/WEB-INF/classes/server.properties` by setting the config parameter `project.ui` to the directory where your UI files are located. We recommend that for prototyping, at least, you use the default directory.

For example:

```
 <isomorphic:loadUI name="test"/>
 
```
Would translate declarative XML in the file `[webroot]/shared/ui/test.ui.xml` to JavaScript and output the results into the JSP output stream at the location of the tag.

### See Also

- [loadProjectTag](loadProjectTag.md#kb-topic-isomorphicloadproject)
- [xmlTag](xmlTag.md#kb-topic-isomorphicxml)

---
