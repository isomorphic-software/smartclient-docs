# SmartClient JSP Tags

[← Back to API Index](../reference.md)

---

## KB Topic: SmartClient JSP Tags

### Description
The SmartClient Java Server component ships with a number of custom JSP tags designed to make development with SmartClient easier. The custom tags are defined in `[webroot]/WEB-INF/iscTaglib.xml` in the SDK package. To make use of these tags, you can use the standard JSP taglib directive with the uri as distributed (which requires no additional configuration):
```
 <%@ taglib uri="http://www.smartclient.com/taglib" prefix="isomorphic" %>
 
```
or you can choose some other uri value if you have reason to - e.g., the following is still supported:
```
 <%@ taglib uri="/WEB-INF/iscTaglib.xml" prefix="isomorphic" %>
 
```
but in that case you'll also need to make sure you have the following entry in your web.xml
```
 <taglib>
     <taglib-uri>isomorphic</taglib-uri> 
     <taglib-location>/WEB-INF/iscTaglib.xml</taglib-location> 
 </taglib>
 
```

All SmartClient JSP tags produce either HTML or JavaScript output, so you can easily see what any given tag is generating by doing a "View->Source" in your browser after browsing to the JSP that contains your tag. Tags that produce HTML must be located in the HTML BODY context in your JSP - that is, outside of any ``<SCRIPT>`` tags and inside ``<BODY>`` tags. Tags that produce JavaScript must be located inside ``<SCRIPT>`` tags.

---
