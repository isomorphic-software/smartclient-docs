# <isomorphic:loadProject>

[← Back to API Index](../reference.md)

---

## KB Topic: <isomorphic:loadProject>

### Description
See [jspTags](../reference.md#kb-topic-smartclient-jsp-tags)

_produces:_ JavaScript

This tag inserts JavaScript to load the screens that are part of the project.

Note that this JSP tag must be surrounded by `<SCRIPT>` tags in the JSP because it generates JavaScript code. Like other tags that generate JavaScript code, this tag can be used in a JSP that is included from your main page in order to create separate cacheability. For example:

```
 <SCRIPT SRC="myUIDefinitions.jsp"></SCRIPT>
 
```

**Tag Attributes:**

**name**  
_value format_: String - comma separated list of Project files to load (minus extensions)  
_default value_: NONE

This attribute specifies the name(s) of the project file(s) that contains any screens that should be loaded into the browser. Project files are located in `[webroot]/shared/ui` by default. This location is changeable in `[webroot]/WEB-INF/classes/server.properties` by setting the config parameter `project.project` to the directory where your Project files are located. We recommend that for prototyping, at least, you use the default directory.

For example:

```
 <isomorphic:loadProject name="test"/>
 
```
Would create JavaScript that loads the screens listed in the project file `[webroot]/shared/ui/test.proj.xml` and output it into the JSP output stream at the location of the tag.

**currentScreenName**  
_value format_: String - name of screen to initially draw  
_default value_: the currentScreenName defined in the project file. In the case where more than one project is specified by the `name` attribute, the default value is taken from the first project only.

This attribute specifies the name of the screen within the project to draw after loading. Drawing of the screen can be suppressed by including the "drawFirstScreen" attribute.

**screenNames**  
_value format_: String - comma-separated list of screen names.  
_default value_: NONE

This attribute specifies the names of screens within the project that should be loaded.

**drawFirstScreen**  
_value format_: boolean - acceptable values: "true" or "false"  
_default value_: "true"

This attribute determines whether the "currentScreenName" screen is drawn after the project screens have been loaded.

**locale**  
_value format_: String - name of locale to load _default value_: NONE

Use this attribute to specify a locale to load. The default value of null omits locale loading, which effectively means the framework default "en" locale is used.

**ownerId**  
_value format_: String - name of project owner _default value_: NONE

Use this attribute to specify a project owner. Only applicable if project source supports owner identification.

### See Also

- [loadUITag](loadUITag.md#kb-topic-isomorphicloadui)

---
