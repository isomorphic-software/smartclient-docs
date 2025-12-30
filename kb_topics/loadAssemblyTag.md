# <isomorphic:loadAssembly>

[← Back to API Index](../reference.md)

---

## KB Topic: <isomorphic:loadAssembly>

### Description
_produces:_ HTML

This tag emits the files listed under a single FileAssemblyEntry in your [fileAssembly](fileAssembly.md#kb-topic-file-assembly) config file. Note that as stated in the [fileAssembly](fileAssembly.md#kb-topic-file-assembly) docs, you can always include a file assembly by writing out a properly formatted `<script>` or `<link>` HTML tag and referencing the same URI as listed in the FileAssemblyEntry that you wish to include, but the `<loadAssembly>` JSP tag provides a useful mechanism to easily switch between development and production mode (via the **assemble** attribute - see below) as well as a few other control points.

**Tag Attributes:**

**URI**  
_value format_: A URI that exactly matches one of the FileAsemblyEntry URIs in your [fileAssembly](fileAssembly.md#kb-topic-file-assembly) configuration file.  
_default value_: NONE

This attribute selects the specific assembly that you wish to include from the file assembly config file and is required.

**assemble**  
_value format_: boolean - acceptable values: "true" or "false"  
_default value_: "true"

This attribute controls the manner in which the files listed in your FileAssemblyEntry are emitted onto the page. When set to "true" (the default), the loadAssembly tag simply emits a `<script>` or `<link>` HTML tag (depending on the extension) and references the URI you specified. This is what you want for production deployment.

When set to "false", the loadAssembly tag emits separate `<script>` or `<link>` HTML tags for each file listed under the FileAssemblyEntry. This is what you frequently want for development because it allows browser tools like Firebug and native browser debuggers to properly report line numbers for errors in a manner that is easily traceable to the source file and location.

The recommended best practice is to parametrize the value of the assemble attribute based on the deployment target and use a rewrite mechanism either in your packaging script (e.g. Ant) or the deployment tool to conditionally set this value such that it is set to "false" in development and "true" in production. For example, like so with Ant:

```
 assemble="<%=\"prd\" == \"@app.server.target@\"%>"
 
```
Note that you then need corresponding logic in your Ant build.xml that does something like:
```
 <property name="app.server.target" value="prd"/>
 <replace file="${war.dir}/your.jsp" token="@app.server.target@" value="\${app.server.target}"/>
 
```

**locale**  
_value format_: valid locale string - see [dataSourceLocalization](dataSourceLocalization.md#kb-topic-datasource-and-component-xml-localization) for more details and examples.  
_default value_: as set by the OS/JVM defaults

**media**  
_value format_: any valid value of the media attribute of the HTML `<link>` element.  
_default value_: NONE

This attribute is valid only for FileAssembly entries with a URI that ends with ".css". When set, the value of this attribute is output as the value of the `media` attribute of the `<link>` element that is emitted onto the page. See e.g. [http://www.w3schools.com/tags/att\_link\_media.asp](http://www.w3schools.com/tags/att_link_media.asp) for valid values of the `media` attribute and a discussion of when/how to use them.

**configFile**  
_value format_: Path to [fileAssembly](fileAssembly.md#kb-topic-file-assembly) configuration file exactly as it would be supplied to the servlet config via the `configFile` init-param.  
_default value_: Automatically derived from [fileAssembly](fileAssembly.md#kb-topic-file-assembly) servlet configuration.

This attribute enables an explicit override of the [fileAssembly](fileAssembly.md#kb-topic-file-assembly) config file use to match the URI entries. Providing this value is not required - it is auto-derived automatically from the settings you provide on the [fileAssembly](fileAssembly.md#kb-topic-file-assembly) servlet. But in rare instances (certain non-compliant servlet containers and/or extremely tight java security settings) this auto-derivation can fail and you can use this attribute to provide an explicit setting.

---
