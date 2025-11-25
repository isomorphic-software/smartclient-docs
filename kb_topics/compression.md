# Compression

[← Back to API Index](../main.md)

---

## KB Topic: Compression

### Description
Compression helps reduce the sizes of various data fetched from the server. Most modern web browsers can handle compressed responses of certain content types. The time it takes to decompress these responses on a client system is negligible compared to the time saved by reducing the number of bits on the wire, especially for slow connections.

If you're not using the SmartClient Java back-end, there are several compression solutions available, depending on your server of choice. Microsoft's IIS has built-in compression capability, please check the reference manual for details. If you're using Apache, you can use [mod\_gzip](http://sourceforge.net/projects/mod-gzip/) or use [mod\_deflate](http://httpd.apache.org/docs/2.0/mod/mod_deflate.html). Some servlet containers also natively support dynamic compression.

The SmartClient Java back-end supports three types of response compression:

*   Pre-compressed static content served via the ISC FileDownload servlet.
*   On-the-fly compression of arbitrary content using the CompressionFilter.
*   Automatic on-the-fly compression of DSRequest, RPCRequest and DataSourceLoader responses.

Serving pre-compressed files

To serve pre-compressed static content via FileDownload, register the FileDownload servlet in your web.xml as follows:

```
     <servlet>
       <servlet-name>FileDownload</servlet-name>
       <servlet-class>com.isomorphic.servlet.FileDownload</servlet-class>
     </servlet>
 
```
Then map any resource that you want to serve compressed to the FileDownload servlet in your web.xml. Typically, you'll want to serve all SmartClient modules compressed. You can do so by adding the following servlet-mapping directive to your web.xml:
```
     <servlet-mapping>
       <servlet-name>FileDownload</servlet-name>
       <url-pattern>/isomorphic/system/modules/*</url-pattern>
     </servlet-mapping>
 
```
Finally, you'll need to create pre-compressed versions of your files alongside the uncompressed versions. If you're using the FileAssembler mechanism, it can create pre-compressed files for you automatically. For all other files, you can use any program that uses the gzip encoding. The compressed file must have exactly the same filename as the uncompressed version, with a '.gz' extension. Note that it's important that both the compressed and uncompressed versions be present alongside each other because there are cases where serving compressed content is not possible (for example HTTP 1.0 requests) - for those situations it's important that the uncompressed files be available to be served to the client. The FileDownload filter automatically detects whether or not compression is possible.

Dynamic Compression

Dynamic Compression requires the optional Network Performance module. To use Dynamic Compression, register the CompressionFilter filter in your web.xml as follows:

```
     <filter>
         <filter-name>CompressionFilter</filter-name>
         <filter-class>com.isomorphic.servlet.CompressionFilter</filter-class>
     </filter>
 
```
Then map any resource that you want dynamically compressed to this filter. Note that the CompressionFilter knows the mime types that are compressible and will automatically ignore any stream that sets a content-encoding header, and it automatically figures out if the current request is an include or forward (and doesn't compress in that case), so it's safe to simply map it to all resources as follows:
```
     <filter-mapping>
         <filter-name>CompressionFilter</filter-name>
         <url-pattern>/*</url-pattern>
     </filter-mapping>
 
```
You can register the CompressionFilter anywhere in your filter chain, but be aware that if any filters in front wrap and inspect the HttpServletResponse output stream, they will be inspecting the compressed response. Filters are typically applied in the order in which they are listed in web.xml and it is advised to keep them that way, otherwise it may result in unexpected behavior. For example, if CompressionFilter would be listed after the JSSyntaxScannerFilter, the last one would stop working, since it relies on uncompressed data.

Automatic Compression of DSRequest, RPCRequest and DataSourceLoader responses

By default, SmartClient Server compresses the responses to all [DSRequest](../main_2.md#object-dsrequest)s, [RPCRequest](../main.md#object-rpcrequest)s and `DataSourceLoader` requests, whether or not the `CompressionFilter` is registered. If you want to switch off this automatic compression, add the following line to your `server.properties` file:

```
    servlet.compress: false
 
```
Compressible mime types and compatibility

The FileDownload servlet and CompressionFilter filter can serve the following mime-types compressed: text/html, text/xml, application/x-javascript, text/javascript, text/ecmascript, image/svg+xml, application/javascript, application/json. If your files are not being compressed, make sure your servlet container has a mime type mapping that identifies it as one of the above file types.

Compression for the mime types listed above is supported on all browsers supported by SmartClient. There is one exception: compression of javascript files for IE versions older than IE6 Service Pack 2 requires that the CompressionFilter be registered to dynamically compress the page that loads these javascript files.

---
