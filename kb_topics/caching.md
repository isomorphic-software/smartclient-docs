# Caching

[← Back to API Index](../reference.md)

---

## KB Topic: Caching

### Description
Standard web browsers can cache server responses, associating the locally-cached files with the URLs (including query parameters) that were used to fetch the files from the server. Each file may be assigned an explicit expiration time. Requests for the associated URL will always be served from the local cache, without accessing the server, until the file expires.

The recommended approach is to move as much content as possible into cacheable assets (these can be images, html, css, and js) and tell the browser to cache those for as long as possible (ideally indefinitely). Clearly, most things can't simply be cached permanently - new versions of the application will often require changes to these assets. To allow for this, the pages that direct the loading of the cached assets should be dynamic and should create version-specific URLs to these cacheable assets. This can be done by tacking the version number as a query parameter or as a path component. Here's an example of loading a javascript file versioned with a query parameter:

```
 <script src='/foo/bar.js?version=13'></script>
 
```
A URL for the same resource including a path component (in this case `"v13"`) might look like this:
```
 <script src='/v13/foo/bar.js'></script>
 
```
The server would of course need to resolve this URL to the appropriate resource.

Note: SmartClient dynamically assembles URLs to retrieve images and CSS from the [current skin](skinning.md#kb-topic-skinning--theming). It's not possible to pervasively apply a version query parameter to these dynamically assembled URLs, so if you want to use versioned URLs to ensure that new versions of skin resources are requested when the SmartClient version changes, versioned URLs must be applied with a path component.

For developers using the [SmartClient server](iscServer.md#kb-topic-smartclient-server-summary), the [loadISC JSP tag](loadISCTag.md#kb-topic-isomorphicloadisc) automatically generates version-specific URLs for loading SmartClient resources, and can be configured to use either URL-parameters or path segments. The SmartClient server can automatically resolve URLs including SmartClient version path segments to the approprirate target resources via the FileDownload servlet or the dedicated VersionedURLFilter.

The [server_properties](server_properties.md#kb-topic-serverproperties-file) configuration can be used to configure default versioning behavior for SmartClient JSP tags, and to enable or disable stripping these URL segments when processing URLs.

Developers do not need to use the SmartClient server to apply or resolve version-specific URLs of course.

It's trivial to apply a versioned URL to the ``<script src=...>`` tags used to load SmartClient framework modules and the `load_skin.js` file for your skin. If you included a version-specific path segment in the script tag to retrieve `load_skin.js` the [skin directory](../classes/Page.md#classmethod-pagesetskindir) will automatically pick this up, meaning all requests for dynamically loaded skin media will also include the path segment.

For more control you can also specify a custom [isomorphicDir](../classes/Page.md#classmethod-pagesetisomorphicdir) or [skinDir](../classes/Page.md#classmethod-pagesetskindir). For example:

```
 isc.Page.setSkinDir('/version/13/isomorphic/skins/SmartClient/');
 
```
You can then either deploy the resources under the versioned directory above or use a URL rewriting engine such as mod\_rewrite for Apache to map all such versions into a single deploy directory.

Generally the version number in a versioned URL wouldn't be hard-coded into a dynamic page, but would instead pick up the value of a variable, such that you can simply bump up the value in one configuration file and have all versioned URLs change dynamically.

**Expires headers**

To actually tell the browser to cache files for a longer length of time than the browser session, you need to set the HTTP 'Expires' header. If you're not using the SmartClient Java back-end there are several caching solutions available, depending on your server of choice. Microsoft's IIS has built-in caching capability, please check the reference manual for details. If you're using Apache, you can use [mod\_expires](http://httpd.apache.org/docs/2.0/mod/mod_expires.html). Some servlet containers also natively support the setting of caching headers.

The SmartClient Java back-end supports setting caching headers via the FileDownload service on a per-mimetype basis. To use it, first register the FileDownload servlet in your web.xml as follows:

```
     <servlet>
       <servlet-name>FileDownload</servlet-name>
       <init-param>
           <param-name>expires</param-name>
           <param-value>text/javascript:3600,image/gif:86400</param-value>
       </init-param>
       <servlet-class>com.isomorphic.servlet.FileDownload</servlet-class>
     </servlet>
 
```
The expires parameter controls the expiration time in seconds. In the block above, javascript files are set to expire in 1 hour and gif images are set to expire in 1 day from the time they are served to the browser. If you don't set explicit expires mappings, all images and css files will be set to expire in 1 day and javascript files will expire in 1 hour, by default.

Next, map any resource that you want to serve with caching headers to the FileDownload servlet in your web.xml. Typically, you'll want to serve the SmartClient modules and all skin images with caching headers. You can do so by adding the following servlet-mapping directives to your web.xml:

```
     <servlet-mapping>
       <servlet-name>FileDownload</servlet-name>
       <url-pattern>/isomorphic/system/modules/*</url-pattern>
     </servlet-mapping>
 
     <servlet-mapping>
       <servlet-name>FileDownload</servlet-name>
       <url-pattern>/isomorphic/skins/*</url-pattern>
     </servlet-mapping>
 
```

---
