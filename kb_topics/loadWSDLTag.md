# <isomorphic:loadWSDL>

[← Back to API Index](../reference.md)

---

## KB Topic: <isomorphic:loadWSDL>

### Description
See [jspTags](../reference.md#kb-topic-smartclient-jsp-tags)

_produces:_ JavaScript

Load a WSDL file and create an instance of [WebService](../classes/WebService.md#class-webservice) that allows invoking operations and binding DataSources to web service operations. This tag works just like [XMLTools.loadWSDL](../classes/XMLTools.md#classmethod-xmltoolsloadwsdl), except it's synchronous and the result is server-cacheable.

Note that this JSP tag must be surrounded by `<SCRIPT>` tags in the JSP because it generates JavaScript code. Like other tags that generate JavaScript code, this tag can be used in a JSP that is included from your main page in order to create separate cacheability. For example:

```
 <SCRIPT SRC="myWebServiceDefinition.jsp"></SCRIPT>
 
```

**Tag Attributes:**

**url**  
_value format_: URL or URI _default value_: NONE

This attribute specifies the URL or URI of the WSDL file to fetch and translate. This can be either a remote URL - e.g: `http://host:port/wsdlFile.wsdl` or a relative or absolute URI to a file local to this container - e.g: `/some/wsdlFile.wsdl` or `../some/wsdlFile.wsdl`. If the url is a remote URL, then an HTTP request will be made for the file. If it is local, it will be fetched from disk using standard Servlet APIs (`ServletContext.getResourceAsStream()`).

**cache**  
_value format_: Integer (number of seconds to cache result) _default value_: 3600 (1 hour)

This attribute specifies the number of seconds for which the fetched WSDL is cacheable on the server. Fetching a WSDL file from a remote server can cause a significant delay in JSP processing, and WSDL files rarely change outside of a development environment. Set this value to zero to disable caching.

### See Also

- [wsdlBinding](wsdlBinding.md#kb-topic-wsdl-binding)
- [XMLTools.loadWSDL](../classes/XMLTools.md#classmethod-xmltoolsloadwsdl)

---
