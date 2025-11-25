# <isomorphic:XML>

[← Back to API Index](../main.md)

---

## KB Topic: <isomorphic:XML>

### Description
See [jspTags](../main.md#kb-topic-smartclient-jsp-tags)

_produces:_ JavaScript

This tag converts SmartClient UI components declaratively specified in the body of the tag to JavaScript for execution in the browser.

The XML->JS translation works just like with [loadUITag](loadUITag.md#kb-topic-isomorphicloadui), but the XML is read from the body of the tag. If you wish, you can also specify an external filename, and XML will be read from that file, in addition to any XML encountered in the body of the tag. If you do specify that an external file should be read, it is read from a path starting in your webroot (as opposed to the ``<loadUI>`` tag, which looks in `shared/ui`)

Note that this JSP tag must be surrounded by `<SCRIPT>` tags in the JSP because it generates JavaScript code. Like other tags that generate JavaScript code, this tag can be used in a JSP that is included from your main page in order to create separate cacheability. For example:

```
 <SCRIPT SRC="myUIDefinitions.jsp"></SCRIPT>
 
```

Example of using this tag :

```
 <isomorphic:XML>
 <Canvas backgroundColor="black"/>
 </isomorphic:XML>
 
```
Would output the following JavaScript code:
```
 Canvas.create({
   backgroundColor: "black"
 });
 
```

**Tag Attributes:**

**filename**  
_value format_: String - name of XML file to load (including the "XML" extension)  
_default value_: NONE

This optional attribute specifies the name of an XML file to read and convert.

An example that specifies both a filename and some XML in the tag body:

```
 <isomorphic:XML filename="test.xml">
   <Canvas backgroundColor="red"/>
 </isomorphic:XML>
 
```

### See Also

- [loadUITag](loadUITag.md#kb-topic-isomorphicloadui)

---
